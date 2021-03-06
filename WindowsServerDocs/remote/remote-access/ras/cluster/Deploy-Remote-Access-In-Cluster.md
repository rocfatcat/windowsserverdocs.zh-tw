---
title: 在叢集中部署遠端存取
description: 本主題是在 Windows Server 2016 的叢集中部署遠端存取指南的一部分。
manager: dougkim
ms.topic: article
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c1d0a9490a2b2ef6efbd15f39ec95f1b482efd5e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944168"
---
# <a name="deploy-remote-access-in-a-cluster"></a>在叢集中部署遠端存取

>適用於：Windows Server (半年度管道)、Windows Server 2016

Windows Server 2016 和 Windows Server 2012 將 DirectAccess 和遠端存取服務 \( RAS \) VPN 合併成一個遠端存取角色。 您可以在許多企業案例中部署遠端存取。 本總覽提供企業案例的簡介，以在使用 Windows 網路負載平衡 \( NLB \) 或外部負載平衡器 \( ELB （ \) 如 F5 Big \- IP）平衡的叢集中部署多部遠端存取服務器。

## <a name="scenario-description"></a><a name="BKMK_OVER"></a>案例描述
叢集部署會將多部遠端存取服務器收集成單一單位，然後使用遠端存取叢集的外部虛擬 IP VIP 位址，透過 DirectAccess 或 VPN 連線到內部公司網路的遠端用戶端電腦，將其作為單一連絡人點 \( \) 。  叢集的流量會使用 Windows NLB 或外部負載平衡器 \( （例如 F5 Big IP）進行負載 \- 平衡 \) 。

## <a name="prerequisites"></a>必要條件
開始部署這個案例之前，請先檢閱這份重要需求清單：

-   預設透過 Windows NLB 的負載平衡。

-   支援的外部負載平衡器。

-   單點傳播模式是預設和建議使用的 NLB 模式。

-   不支援在 DirectAccess 管理主控台以外或使用 PowerShell Cmdlet 來變更原則。

-   使用 NLB 或外部負載平衡器時，無法將 IPHTTPS 首碼變更為59以外的任何專案 \/ 。

-   負載平衡節點必須在相同的 IPv4 子網路中。

-   在 ELB 部署中，如果需要向外管理，則 DirectAccess 用戶端無法使用 &nbsp; Teredo。 只有 IPHTTPS 可以用於端 \- 對 \- 端通訊。

-   請確定 \/ 已安裝所有已知的 NLB ELB 修補程式。

-   不支援公司網路中的 ISATAP。 如果您使用 ISATAP，則應該將它移除，然後使用原生的 IPv6。

## <a name="in-this-scenario"></a>在這個案例中
叢集部署案例包含一些步驟：

1.  [使用 Advanced 選項部署 Always ON VPN 伺服器](../../vpn/always-on-vpn/deploy/always-on-vpn-adv-options.md)。 在設定叢集部署之前，必須先部署具有 advanced settings 的單一遠端存取服務器。

2.  [規劃遠端存取叢集部署](plan/Plan-a-Remote-Access-Cluster-Deployment.md)。 若要從單一伺服器部署建立叢集，需要一些額外的步驟，包括準備叢集部署的憑證。

3.  [設定遠端存取](configure/Configure-a-Remote-Access-Cluster.md)叢集。 這包含幾個設定步驟，包括準備適用于 Windows NLB 或外部負載平衡器的單一伺服器、準備額外的伺服器以加入叢集，以及啟用負載平衡。

## <a name="practical-applications"></a><a name="BKMK_APP"></a>實際應用
將多個伺服器納入叢集中，可以提供以下優點：

-   延展性。 一部遠端存取服務器提供有限等級的伺服器可靠性和可擴充的效能。 將兩部或更多伺服器編列成單一叢集後，您就可以有更多能力接納更多使用者以及提供更高的輸送量。

-   高可用性。 叢集為 always on 存取提供高可用性 \- 。 如果叢集中有一部伺服器當機，遠端使用者可以透過叢集中的其他伺服器，繼續連接公司網路。 叢集中的所有伺服器都有一組相同的叢集虛擬 IP \( VIP \) 位址，同時仍會為每部伺服器維護唯一的私人 IP 位址。

-   易於 \- \- 管理。 叢集可讓多部伺服器做為單一實體進行管理。 共用的設定可以輕鬆設定到叢集中的每一部伺服器。 您可以從叢集中的任何伺服器管理遠端存取設定，或使用遠端伺服器管理工具 RSAT 從遠端進行管理 \( \) 。 此外，整個叢集可以從單一「遠端存取管理」主控台進行監視。

## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>這個案例包含的角色與功能
下表列出本案例必備的角色和功能：

|角色 \/ 功能|如何支援本案例|
|---------|-----------------|
|遠端存取角色|這個角色是利用伺服器管理員主控台安裝和解除安裝。 它同時包含 DirectAccess （先前是 Windows Server 2008 R2 中的功能）和路由及遠端存取服務 \( RRAS \) （先前是網路原則與存取服務 \( NPAS 伺服器角色下的角色服務） \) 。 遠端存取角色包含兩個元件：<p>-Always On VPN 和路由及遠端存取服務 \( RRAS \) VPN-DIRECTACCESS 和 VPN 會在 [遠端存取管理] 主控台中一起管理。<br />-RRAS 路由-在舊版路由及遠端存取主控台中管理 RRAS 路由功能。<p>相依性如下所示：<p>-Internet Information Services \( IIS \) Web 服務器-設定網路位置伺服器和預設 Web 探查時，需要這項功能。<br />-Windows 內部資料庫-用於遠端存取服務器上的本機帳戶處理。|
|遠端存取管理工具功能|這個功能的安裝方式如下：<p>-安裝遠端存取角色時，預設會將它安裝在遠端存取服務器上，並支援遠端管理主控台使用者介面。<br />-您可以選擇性地將它安裝在未執行遠端存取服務器角色的伺服器上。 在這種情況下，它是用於從遠端管理那些執行 DirectAccess 和 VPN 的遠端存取電腦。<p>遠端存取管理工具功能包含以下各項：<p>-遠端存取 GUI 和命令列工具<br />-適用于 Windows PowerShell 的遠端存取模組<p>依存項目包括：<p>-群組原則管理主控台<br />-RAS 連線管理員系統管理元件 \( CMAK\)<br />-Windows PowerShell 3。0<br />-圖形化管理工具與基礎結構|
|Network Load Balancing|這個功能利用 Windows NLB，提供叢集的負載平衡功能。|

## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>硬體需求
本案例需要的硬體如下所示：

-   至少兩部符合 Windows Server 2012 硬體需求的電腦。

-   針對外部 Load Balancer 案例，需要專用硬體， \( 例如 F5 BigIP \) 。

-   為了測試案例，您必須至少有一部執行 Windows 10 的電腦設定為 Always On VPN 用戶端。

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>軟體需求
本案例的一些需求：

-   部署單一伺服器時的軟體需求。 如需詳細資訊，請參閱[使用 Advanced Settings 部署單一 DirectAccess 伺服器](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)。 單一遠端存取) 。

-   除了單一伺服器的軟體需求之外，還有一些叢集 \- 特定需求：

    -   在每部叢集伺服器上，IP \- HTTPS 憑證主體名稱必須與 ConnectTo 位址相符。 叢集部署支援在叢集伺服器上混合使用萬用字元和非 \- 萬用字元憑證。

    -   如果網路位置伺服器安裝在遠端存取伺服器上，則在叢集中的每一部伺服器上，網路位置伺服器憑證必須要有相同的主體名稱。 此外，網路位置伺服器憑證的名稱不可以和 DirectAccess 部署中的任何伺服器名稱相同。

    -   IP \- HTTPS 和網路位置伺服器憑證必須使用與單一伺服器所發行之憑證相同的方法來發出。 例如，如果單一伺服器使用公開憑證授權單位單位 CA，則叢集中的 \( \) 所有伺服器都必須具有公用 CA 所發行的憑證。 或者，如果單一伺服器使用 IP HTTPS 的自我簽署憑證，則叢集中的 \- \- 所有伺服器都必須執行同樣的動作。

    -   指派給伺服器叢集 DirectAccess 用戶端電腦的 IPv6 首碼必須是 59 位元。 如果開通 VPN，則 VPN 首碼也必須設定成 59 位元。

## <a name="known-issues"></a><a name="KnownIssues"></a>已知問題
以下是設定叢集案例的已知問題：

-   在具有單一網路介面卡的 IPv4 部署中設定 DirectAccess 之後 \- ，在預設 DNS64 之後，會在 \( 網路介面卡上自動設定包含 "：3333：：" 的 IPv6 位址 \) ，而嘗試透過 \- 遠端存取管理主控台來啟用負載平衡，會導致提示使用者提供 ipv6 DIP。 如果提供 IPv6 DIP，設定會在按一下 [認可]**** 之後失敗，並發生錯誤：參數不正確。

    若要解決此問題：

    1.  從[備份和還原遠端存取設定](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6)下載備份和還原指令碼。

    2.  使用下載的腳本備份來備份您的遠端存取 Gpo \-RemoteAccess.ps1

    3.  嘗試啟用負載平衡，直到它失敗所在的步驟。 在 [啟用負載平衡] 對話方塊中，展開 [詳細資料] 區域，以滑鼠右鍵 \- 按一下 [詳細資料] 區域，然後按一下 [**複製腳本**]。

    4.  開啟 [記事本]，並貼上剪貼簿的內容。 例如：

        ```
        Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress @('10.244.4.19 /255.255.255.0','fdc4:29bd:abde:3333::2/128') -InternetVirtualIPAddress @('fdc4:29bd:abde:3333::1/128', '10.244.4.21 /255.255.255.0') -ComputerName 'DA1.domain1.corp.contoso.com' -Verbose
        ```

    5.  關閉任何開啟的 [遠端存取] 對話方塊，並關閉遠端存取管理主控台。

    6.  編輯貼上的文字，並移除 IPv6 位址。 例如：

        ```
        Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress @('10.244.4.19 /255.255.255.0') -InternetVirtualIPAddress @('10.244.4.21 /255.255.255.0') -ComputerName 'DA1.domain1.corp.contoso.com' -Verbose
        ```

    7.  在提升權限的 PowerShell 視窗中，執行前一步驟的命令。

    8.  如果 Cmdlet 在 \( 執行時因為輸入值不正確而失敗 \) ，請執行命令還原 \-RemoteAccess.ps1 並遵循指示，以確定已維護原始設定的完整性。

    9. 您現在可以重新開啟遠端存取管理主控台。
