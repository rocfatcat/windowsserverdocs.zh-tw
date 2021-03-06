---
title: 部署 BranchCache 託管快取模式
description: 本指南提供的指示說明如何在執行 Windows Server 2016 和 Windows 10 的電腦上，以託管快取模式部署 BranchCache。
manager: brianlic
ms.topic: article
ms.assetid: 4235231c-4732-4ea9-9330-2a8c8a616d39
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8f82e6e42201a1c68c2b2c62bb933887f3d8de77
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997109"
---
# <a name="deploy-branchcache-hosted-cache-mode"></a>部署 BranchCache 託管快取模式

>適用於：Windows Server (半年通道)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

《 Windows Server 2016 核心網路指南》提供在新樹系中規劃和部署全功能網路和新 Active Directory 網域所需之核心元件的指示 &reg; 。

本指南說明如何藉由提供指示，在一或多個分公司中以託管快取模式部署 BranchCache， \- 其中用戶端電腦執行的是 windows &reg; 10、Windows 8.1 或 Windows 8，並已加入網域。

>[!IMPORTANT]
>如果您打算部署或已部署執行 Windows Server 2008 R2 的 BranchCache 託管快取伺服器，請勿使用本指南。 本指南提供的指示說明如何使用執行 Windows Server &reg; 2016、Windows server 2012 R2 或 Windows server 2012 的託管快取伺服器來部署託管快取模式。

本指南涵蓋下列各節。

- [使用本指南的必要條件](#bkmk_pre)

- [關於本指南](#bkmk_about)

- [本指南中未提供的內容](#bkmk_not)

- [技術概覽](#bkmk_tech)

- [BranchCache 託管快取模式部署總覽](2-Bc-Hcm-Deploy-Overview.md)

- [BranchCache 託管快取模式部署規劃](3-Bc-Hcm-Plan.md)

- [BranchCache 託管快取模式部署](4-Bc-Hcm-Deployment.md)

- [其他資源](11-Bc-Hcm-additional-resources.md)

## <a name="prerequisites-for-using-this-guide"></a><a name="bkmk_pre"></a>使用本指南的必要條件

這是《 Windows Server 2016 核心網路指南》的附屬指南。 若要使用此指南部署託管快取模式的 BranchCache，您必須先執行以下作業：

- 使用《核心網路指南》在總公司部署核心網路，或是在您的網路上已經安裝《核心網路指南》中提供的技術且正常運作。 這些技術包括 [TCP \/ IP v4]、[DHCP]、[Active Directory Domain Services \( AD DS] 和 [DNS] \) 。

    > [!NOTE]
    > Windows server 2016[核心網路指南](../../core-network-guide.md)可在 windows Server 2016 技術文件庫中取得。

- 在您的總公司或雲端資料中心部署執行 Windows Server 2016、Windows Server 2012 R2 或 Windows Server 2012 的 BranchCache 內容伺服器。 如需有關如何部署 BranchCache 內容伺服器的詳細資訊，請參閱[其他資源](11-Bc-Hcm-additional-resources.md)。

- \( \) 使用虛擬私人網路 \( VPN \) 、DirectAccess 或其他連線方法，在您的分公司、總公司和您的雲端資源之間建立廣域網路絡 WAN 連線。

- 在分公司部署執行下列其中一種作業系統的用戶端電腦，提供支援背景智慧型傳送服務 (BITS) 、「超文字傳輸」通訊協定 (HTTP) 和伺服器訊息區 (SMB) 。
    - Windows 10 Enterprise
    - Windows 10 Education
    - Windows 8.1 Enterprise
    - Windows 8 企業版

> [!NOTE]
> 在下列作業系統中，BranchCache 不支援 HTTP 和 SMB 功能，但支援 BranchCache 位功能。
>     - 僅限 Windows 10 專業版，僅支援 BITS
>     - Windows 8.1 Pro，僅支援 BITS
>     - Windows 8 專業版，僅支援 BITS

## <a name="about-this-guide"></a><a name="bkmk_about"></a>關於本指南

本指南是針對已遵循《 Windows Server 2016 核心網路指南》或 Windows Server 2012 核心網路指南中的指示部署核心網路的網路和系統管理員所設計，適用于先前已部署「核心網路指南」中所包含之技術的使用者，包括 Active Directory Domain Services \( AD DS \) 、功能變數名稱服務 \( DNS \) 、動態主機設定通訊協定 \( DHCP \) 和 TCP \/ IP v4。

建議您檢閱此部署案例中所用每個技術的設計和部署指南。 這些指南可協助您判斷此部署案例是否提供貴組織的網路需要的服務與設定。

## <a name="what-this-guide-does-not-provide"></a><a name="bkmk_not"></a>本指南中未提供的內容

本指南未提供 BranchCache 的概念資訊，包括關於 BranchCache 模式和功能的資訊。

本指南未提供如何在分公司部署 WAN 連線或其他技術 (如 DHCP、RODC 或 VPN 伺服器) 的資訊。

此外，本指南未提供部署託管快取伺服器應使用之硬體的相關指引。 您可以在託管快取伺服器上執行其他服務和應用程式，但是您必須根據工作負載、硬體功能、分公司規模大小等因素進行判斷，是否要在特定電腦上安裝 BranchCache 託管快取伺服器，以及要為快取配置多少磁碟空間。
本指南未提供設定執行 Windows 7 之電腦的指示。 如果您的分公司中有執行 Windows 7 的用戶端電腦，則必須使用與本指南中所提供不同的程式來設定它們，而這些程式適用于執行 Windows 10、Windows 8.1 和 Windows 8 的用戶端電腦。

此外，如果您有執行 Windows 7 的電腦，就必須使用由用戶端電腦信任的憑證授權單位單位所發行的伺服器憑證來設定託管快取伺服器。 \(如果您的所有用戶端電腦都執行 Windows 10、Windows 8.1 或 Windows 8，則不需要以伺服器憑證設定託管快取伺服器。\)
> [!IMPORTANT]
> 如果您的託管快取伺服器執行 Windows Server 2008 R2，請使用 Windows Server 2008 R2 [BranchCache 部署指南](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649232(v=ws.10))（而非本指南），以託管快取模式部署 BranchCache。 將該指南中所述的群組原則設定，套用至執行 windows 7 到 Windows 10 之 Windows 版本的所有 BranchCache 用戶端。 無法使用本指南中的步驟來設定執行 Windows Server 2008 R2 的電腦。

## <a name="technology-overviews"></a><a name="bkmk_tech"></a>技術概覽

本附屬指南中，BranchCache 是您唯一需要安裝和設定的技術。 您必須在內容伺服器 (如 Web 和檔案伺服器) 上執行 Windows PowerShell BranchCache 命令，但您不需要以任何其他方式變更或重新設定內容伺服器。 此外，您必須在執行 Windows Server 2016、Windows Server 2012 R2 或 Windows Server 2012 AD DS 的網域控制站上，使用群組原則來設定用戶端電腦。

### <a name="branchcache"></a>BranchCache

BranchCache 是一種廣域網路 (WAN) 頻寬優化技術，其中包含在 Windows Server 2016 和 Windows 10 作業系統的某些版本中，以及某些 Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2 和 Windows 7 版本中。

若要在使用者存取遠端伺服器上的內容時優化 WAN 頻寬，BranchCache 會從總公司或託管雲端內容伺服器下載用戶端要求的內容，並在分公司位置快取內容，讓分公司的其他用戶端電腦可以在本機存取相同的內容，而不是透過 WAN。

當您部署託管快取模式的 BranchCache 時，必須在分公司將用戶端電腦設定為託管快取模式用戶端，然後必須在分公司部署託管快取伺服器。 本指南示範如何從您的 Web 和以檔案伺服器為基礎的內容伺服器，使用 prehashed 和預先載入的內容來部署託管快取伺服器 \- 。

### <a name="group-policy"></a>群組原則

Windows Server 2016、Windows Server 2012 R2 和 Windows Server 2012 中的群組原則是一種基礎結構，可用來將一或多個所需的設定或原則設定，傳遞並套用至 Active Directory 環境中的一組目標使用者和電腦。

此基礎結構包含群組原則引擎和多個 \- \( \) 負責讀取目標用戶端電腦上原則設定的用戶端延伸 cse。

此案例使用群組原則來設定處於 BranchCache 託管快取模式的網域成員用戶端電腦。

若要繼續進行本指南，請參閱[BranchCache 託管快取模式部署總覽](2-Bc-Hcm-Deploy-Overview.md)。