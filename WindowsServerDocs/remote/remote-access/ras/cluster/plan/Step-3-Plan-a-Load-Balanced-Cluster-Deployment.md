---
title: 步驟3：規劃負載平衡叢集部署
description: 本主題是在 Windows Server 2016 的叢集中部署遠端存取指南的一部分。
manager: brianlic
ms.topic: article
ms.assetid: 7540c17b-81de-47de-a04f-3247afa26f70
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 6c590fd99715e49034592358f65c468c6a46dfb9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963884"
---
# <a name="step-3-plan-a-load-balanced-cluster-deployment"></a>步驟3：規劃負載平衡叢集部署

>適用於：Windows Server (半年度管道)、Windows Server 2016

下一步是規劃負載平衡設定和叢集部署。

|Task|描述|
|----|--------|
|3.1 規劃負載平衡|決定是否要使用 Windows 網路負載平衡 (NLB) 或外部負載平衡器 (ELB) 。|
|3.2 規劃 IP-HTTPS|如果未使用自我簽署憑證，則遠端存取服務器需要叢集中每部伺服器的 SSL 憑證，才能驗證 IP-HTTPS 連線。|
|3.3 規劃 VPN 用戶端連接|請注意 VPN 用戶端連線的需求。|
|3.4 規劃網路位置伺服器|如果網路位置伺服器網站裝載于遠端存取服務器上，且未使用自我簽署憑證，請確定叢集中的每部伺服器都具有伺服器憑證，以驗證網站的連線。|

## <a name="31-plan-load-balancing"></a><a name="bkmk_2_1_Plan_LB"></a>3.1 規劃負載平衡
遠端存取可以部署在單一伺服器或遠端存取服務器的叢集上。 對叢集的流量可進行負載平衡，為 DirectAccess 用戶端提供高可用性和擴充性。 有兩個負載平衡選項：

-   **WINDOWS nlb**-windows Nlb 是 windows server 功能。 若要使用它，您不需要額外的硬體，因為叢集中的所有伺服器都負責管理流量負載。 Windows NLB 在「遠端存取」叢集中最多支援八部伺服器。

-   **外部負載平衡器**-使用外部負載平衡器時，需要外部硬體來管理遠端存取叢集伺服器之間的流量負載。 此外，使用外部負載平衡器，在叢集中最多支援32部遠端存取服務器。 設定外部負載平衡時，請記住下列幾點：

    -   系統管理員必須確定透過 [遠端存取] 負載平衡 wizard 設定的虛擬 Ip，會在外部負載平衡器上使用 (例如 F5 Big Tcp/ip 本機流量管理員系統) 。 啟用外部負載平衡時，外部和內部介面上的 IP 位址將會升級為虛擬 IP 位址，而且必須在負載平衡器上進行檢測。 這麼做是為了讓系統管理員不需要變更叢集部署公用名稱的 DNS 專案。 此外，IPsec 通道端點也衍生自伺服器 Ip。 如果系統管理員提供個別的虛擬 Ip，則用戶端將無法連接到伺服器。 請參閱 3.1.1 External Load Balancer 設定範例中的使用外部負載平衡設定 DirectAccess 的範例。

    -   許多外部負載平衡器 (包括 F5) 不支援6to4 和 ISATAP 的負載平衡。 如果遠端存取服務器是 ISATAP 路由器，則 ISATAP 函式應該移至另一部電腦。 此外，當 ISATAP 函式位於不同的電腦上時，DirectAccess 伺服器必須具有與 ISATAP 路由器的原生 IPv6 連線能力。 請注意，在設定 DirectAccess 之前，應該要有此連線能力。

    -   針對外部負載平衡，如果必須使用 Teredo，所有遠端存取服務器都必須有兩個連續的公用 IPv4 位址作為專用的 IP 位址。 叢集的虛擬 Ip 也必須有兩個連續的公用 IPv4 位址。 對於 Windows NLB 而言，只有叢集的虛擬 Ip 必須有兩個連續的公用 IPv4 位址才是如此。 如果未使用 Teredo，則不需要兩個連續的 IP 位址。

    -   系統管理員可以從 Windows NLB 切換到外部負載平衡器，反之亦然。 請注意，如果外部負載平衡器部署中有8部以上的伺服器，系統管理員就無法從外部負載平衡器切換至 Windows NLB。

### <a name="311-external-load-balancer-configuration-example"></a><a name="ELBConfigEx"></a>3.1.1 外部 Load Balancer 設定範例
本節說明在新的遠端存取部署上啟用外部負載平衡器的設定步驟。 使用外部負載平衡器時，遠端存取叢集可能如下圖所示，其中遠端存取服務器會透過內部網路上的負載平衡器連線到公司網路，並透過連線到外部網路的負載平衡器連接到網際網路：

![外部 Load Balancer 設定範例](../../../../media/Step-3-Plan-a-Load-Balanced-Cluster-Deployment/ELBDiagram-URA_Enterprise_NLB-.png)

##### <a name="planning-information"></a>規劃資訊

1.  用戶端將用來連線到遠端存取) 的外部 Vip (Ip 已決定為131.107.0.102，131.107.0.103

2.  外部網路上的負載平衡器-131.107.0.245 (Internet) ，131.107.1.245

    周邊網路 (也稱為非軍事區域和 DMZ) 是在外部網路上的負載平衡器與遠端存取服務器之間。

3.  周邊網路上遠端存取服務器的 IP 位址-131.107.1.102、131.107.1.103

4.  ELB 網路上遠端存取服務器的 IP 位址 (也就是在遠端存取服務器與內部網路上的負載平衡器之間) -30.11.1.101，2006:2005:11:1::101

5.  內部網路自我 Ip 上的負載平衡器-30.11.1.245 2006:2005:11:1::245 (ELB) 、30.1.1.245 2006:2005:1:1::245 (公司網路) 

6.  內部 Vip (用於用戶端網路探查和網路位置伺服器的 IP 位址，如果安裝在遠端存取服務器上) 已決定為30.1.1.10，2006:2005:1:1::10

##### <a name="steps"></a>步驟

1.  設定遠端存取服務器的外部網路介面卡 (連線到周邊網路) ，其位址為131.107.0.102，131.107.0.103。 DirectAccess 設定需要此步驟，才能偵測正確的 IPsec 通道端點。

2.  設定遠端存取服務器的內部網路介面卡 (，其會使用 web 探查/網路位置伺服器 IP 位址 (30.1.1.10，2006:2005:1:1::10) 連線到 ELB 網路) 。 這是允許用戶端存取 web 探查 IP 的必要步驟，因此網路連線助理會正確指出 DirectAccess 的連接狀態。 如果 DirectAccess 伺服器上已設定網路位置伺服器，此步驟也會允許其存取。

    > [!NOTE]
    > 請確定可以使用此設定，從遠端存取服務器連線到網域控制站。

3.  在遠端存取服務器上設定 DirectAccess 單一伺服器。

4.  啟用 DirectAccess 設定中的外部負載平衡。 使用131.107.1.102 作為外部私人 IP 位址 (DIP)  (131.107.1.103 會自動選取) ，請使用30.11.1.101，2006:2005:11:1::101 做為內部 Dip。

5.  使用131.107.0.102 和131.107.0.103 位址，設定外部負載平衡器上 (VIP) 的外部虛擬 Ip。 此外，在具有位址30.1.1.10 和2006:2005:1:1::10 的外部負載平衡器上設定內部 Vip。

6.  遠端存取服務器現在會設定為已規劃的 IP 位址，而叢集的外部和內部 IP 位址則會根據規劃的 IP 位址進行設定。

## <a name="32-plan-ip-https"></a><a name="bkmk_2_2_NLB"></a>3.2 規劃 IP-HTTPS

1.  **憑證需求**-在部署單一遠端存取服務器時，您選取要使用公開或內部憑證授權單位單位所發出的 ip-HTTPs 憑證 (CA) 或自我簽署憑證。 針對叢集部署，您必須在遠端存取叢集的每個成員上使用相同類型的憑證。 也就是說，如果您使用公用 CA 所發行的憑證 (建議) ，您必須在叢集的每個成員上安裝公用 CA 所發行的憑證。 新憑證的主體名稱應該與您的部署中目前使用的 ip-HTTPs 憑證主體名稱相同。 請注意，如果您使用自我簽署憑證，則會在叢集部署期間，于每部伺服器上自動設定。

2.  **前置詞需求**-遠端存取可讓您以 SSL 為基礎的流量和 DirectAccess 流量進行負載平衡。 若要對所有以 IPv6 為基礎的 DirectAccess 流量進行負載平衡，遠端存取必須檢查所有轉換技術的 IPv4 通道。 因為 IP-HTTPS 流量已加密，所以不可能檢查 IPv4 通道的內容。 若要讓 IP-HTTPS 流量達到負載平衡，您必須配置足夠的 IPv6 首碼，讓不同的 IPv6/64 首碼可以指派給每個叢集成員。 您最多可以在負載平衡叢集中設定32部伺服器;因此，您必須指定/59 前置詞。 此首碼必須可路由傳送至遠端存取叢集的內部 IPv6 位址，並在 [遠端存取服務器安裝程式] 中設定。

    > [!NOTE]
    > 前置詞需求僅適用于已啟用 IPv6 的內部網路， (僅限 IPv6 或 IPV4 + IPv6) 。 在僅 IPv4 的公司網路中，會自動設定用戶端首碼，而且系統管理員無法變更它。

## <a name="33-plan-for-vpn-client-connections"></a><a name="BKMK_3.3"></a>3.3 規劃 VPN 用戶端連接
VPN 用戶端連線有數個考慮：

-   如果使用 DHCP 配置 VPN 用戶端位址，VPN 用戶端流量就無法進行負載平衡。 需要靜態位址集區。

-   您可以在已部署 DirectAccess 的負載平衡叢集上啟用 RRAS，使用 [遠端存取管理] 主控台的工作窗格上的 [**啟用 VPN** ]。

-   在 [路由及遠端存取管理] 主控台中完成的任何 VPN 變更 (rrasmgmt) 必須以手動方式複寫到叢集中的所有遠端存取服務器。

-   若要讓 VPN IPv6 用戶端流量達到負載平衡，您必須指定59位 IPv6 首碼。

## <a name="34-plan-the-network-location-server"></a><a name="BKMK_nls"></a>3.4 規劃網路位置伺服器
如果您是在單一遠端存取服務器上執行網路位置伺服器網站，則在部署期間，您選擇使用由內部憑證授權單位單位所發行的憑證 (CA) 或自我簽署憑證。  請注意：

1.  「遠端存取」叢集的每個成員都必須有網路位置伺服器的憑證，而該伺服器會對應到網路位置伺服器網站的 DNS 專案。

2.  每個叢集伺服器的憑證都必須以與單一遠端存取服務器目前網路位置伺服器憑證上的憑證相同的方式來發出。 例如，如果您使用由內部 CA 所發行的憑證，您必須在叢集的每個成員上安裝由內部 CA 所發出的憑證。

3.  如果您使用自我簽署憑證，則會在叢集部署期間為每部伺服器自動設定自我簽署憑證。

4.  憑證的主體名稱不得與遠端存取部署中任何伺服器的名稱相同。
