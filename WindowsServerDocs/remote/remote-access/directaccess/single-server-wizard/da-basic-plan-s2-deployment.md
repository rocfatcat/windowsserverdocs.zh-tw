---
title: 步驟2規劃基本 DirectAccess 部署
description: 本主題是使用適用于 Windows Server 2016 的消費者入門 Wizard 部署單一 DirectAccess 伺服器指南的一部分
manager: brianlic
ms.topic: article
ms.assetid: 7ddcb162-dd92-406c-acab-d3de7239c644
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 832e9eb7621a6ca17edc4fcd8c7450ca558159e1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970305"
---
# <a name="step-2-plan-the-basic-directaccess-deployment"></a>步驟2規劃基本 DirectAccess 部署

>適用於：Windows Server (半年度管道)、Windows Server 2016

規劃 DirectAccess 基礎結構之後，在具有基本設定的單一伺服器上部署 DirectAccess 的下一步，就是規劃消費者入門 Wizard 的設定。

|Task|描述|
|----|--------|
|規劃用戶端部署|根據預設，消費者入門 Wizard 會藉由將 WMI 篩選器套用至用戶端設定 GPO，將 DirectAccess 部署到網域中的所有膝上型電腦和筆記本電腦|
|規劃 DirectAccess 伺服器部署|規劃如何部署 DirectAccess 伺服器。|

## <a name="planning-for-client-deployment"></a><a name="bkmk_2_1_client"></a>規劃用戶端部署
規劃用戶端部署時要進行兩個決策：

1.  DirectAccess 將僅供攜帶型電腦使用，或是可供任何電腦使用？

    當您在消費者入門 Wizard 中設定 DirectAccess 用戶端時，您可以選擇只允許指定之安全性群組中的行動電腦使用 DirectAccess 進行連接。 如果您限制存取行動電腦，DirectAccess 會自動設定 WMI 篩選器，以確保 DirectAccess 用戶端 GPO 僅適用于指定安全性群組中的行動電腦。 DirectAccess 系統管理員需要建立或修改群組原則 WMI 篩選器的許可權，才能啟用此設定。

2.  哪些安全性群組將包含 DirectAccess 用戶端電腦？

    DirectAccess 設定包含在 DirectAccess 用戶端 GPO 中。 GPO 會套用到屬於您在消費者入門 wizard 中指定之安全性群組的電腦。 您可以指定在任何支援的網域中所包含的安全性群組。 設定 DirectAccess 之前，應該先建立安全性群組。 完成 DirectAccess 部署之後，您可以將電腦新增到安全性群組，但請注意，如果您將位於不同網域的用戶端電腦新增到安全性群組，用戶端 GPO 將不會套用到這些用戶端。 例如，如果您在網域 A 中建立 SG1 做為 DirectAccess 用戶端，之後新增網域 B 的用戶端到此群組，用戶端 GPO 將不會套用到網域 B 中的用戶端。若要避免這個問題，請為每個包含用戶端電腦的網域建立新的用戶端安全性群組。 或者，如果您不想要建立新的安全性群組，請執行 Add-DAClient Cmdlet，加上新網域的新 GPO 名稱。

## <a name="planning-for-directaccess-server-deployment"></a><a name="bkmk_2_2_server"></a>規劃 DirectAccess 伺服器部署
規劃部署 DirectAccess 伺服器時，有幾項決定要做：

-   **網路拓撲**-部署 DirectAccess 伺服器時，有兩種可用的拓撲：

    -   **兩張適配**卡-有兩張網路介面卡，DirectAccess 可以設定一個直接連線到網際網路的網路介面卡，另一個則連線到內部網路。 或者，伺服器安裝在邊緣裝置 (例如防火牆或路由器) 後面。 在此設定中，一張網路介面卡連線到周邊網路，另一張連線到內部網路。

    -   **單一網路介面卡**-在此設定中，DirectAccess 伺服器會安裝在邊緣裝置（例如防火牆或路由器）後方。 網路介面卡會連線到內部網路。

-   **網路介面卡**-directaccess wizard 會自動偵測 directaccess 伺服器上設定的網路介面卡。 您可以確認已從 [**審查**] 頁面選取正確的介面卡。

-   **Ip-HTTPs 憑證**-由於此部署中沒有必要的 PKI，因此，如果沒有任何憑證存在) ，嚮導會自動為 Ip-HTTPs 和網路位置 (伺服器布建自我簽署憑證，並自動啟用 Kerberos proxy。 此 wizard 也會針對僅 IPv4 環境中的通訊協定轉譯啟用 NAT64 和 DNS64。 精靈套用設定成功完成之後，按一下 [關閉]****。

-   **Windows 7 用戶端**-您無法從消費者入門 Wizard 啟用 windows 7 用戶端的支援。 您可以從 [Advanced 安裝精靈] 啟用此功能。 如需詳細資訊，請參閱[使用 Advanced Settings 部署單一 DirectAccess 伺服器](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)。

-   **Vpn**設定-設定 DirectAccess 之前，請決定是否要提供遠端用戶端的 VPN 存取權。 如果您的組織中有不支援 DirectAccess 連線的用戶端電腦，您應該提供 VPN 存取 (可能是因為它們未受管理，或未執行) 不支援 DirectAccess 的作業系統。 消費者入門 Wizard 會使用 DHCP 設定 VPN IP 位址指派，並設定 VPN 用戶端使用 Active Directory 進行驗證。

-   **強制通道**-如果您打算使用強制通道，或未來可能會新增它，您應該使用 [使用[Advanced Settings 部署單一 DirectAccess 伺服器](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)] 來部署兩個通道設定。 基於安全性考慮，不支援在單一通道設定中強制通道。

## <a name="previous-step"></a><a name="BKMK_Links"></a>上一個步驟

-   [步驟 1：規劃基本 DirectAccess 基礎結構](da-basic-plan-s1-infrastructure.md)



