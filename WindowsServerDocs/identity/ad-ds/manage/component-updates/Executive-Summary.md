---
ms.assetid: 85ca191c-0cc7-4453-a72c-42060ddf2ea2
title: 執行摘要
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: a3eecec9d47f91bb6a9ba549abc3bf62482b2f49
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863279"
---
# <a name="executive-summary"></a>執行摘要

>適用於：Windows Server 2012

>[!IMPORTANT] 
>下列文件以 2013年所撰寫，並供追溯歷程之用。  目前我們檢閱這份文件，而且很有可能變更。  它可能不會反映目前的最佳作法。

沒有任何組織的資訊技術 (IT) 基礎結構免受攻擊，但如果適當的原則、 流程和控制項實作來保護組織的運算基礎結構的重要片段，它可能可以防止入侵事件成長批發危害的運算環境。  
  
此摘要被要供作為獨立文件摘要文件的內容，其中包含可協助組織提升其 Active Directory 安裝的安全性建議。 藉由實作這些建議，組織將能夠識別並排定優先順序的安全性活動、 保護其組織的運算基礎結構的重要片段，並建立可大幅降低的可能性的控制項成功攻擊的 IT 環境的重要元件的詳細資訊。  
  
雖然本文件將討論 Active Directory 與因應對策，以減少受攻擊面最常見的攻擊，它也會包含在完整的入侵事件時復原的建議。 唯有復原 Active Directory 的危害時，就是發生前備妥以遭到入侵。  
  
這份文件的主要區段如下：  
  
-   危及系統安全的途徑  
  
-   減少 Active Directory 的攻擊面  
  
-   監視 Active Directory 遭到危害的徵兆  
  
-   規劃危害因應措施  
  
## <a name="avenues-to-compromise"></a>危及系統安全的途徑  
本節提供部分最常套用漏洞攻擊者用來危害客戶的基礎結構的相關資訊。 它包含弱點，以及他們一開始滲入客戶的基礎結構、 洩露散佈額外的系統，及最終目標 Active Directory 和網域控制站，以取得完整的使用方式的一般的類別組織的樹系的控制項。 它不會提供有關解決每一種弱點，特別是在區域中的弱點不會以直接鎖定 Active Directory 的詳細的建議。 不過，每個弱點類型，我們提供用以開發因應對策，以及降低組織的受攻擊面的其他資訊的連結。  
  
包括下列主題：  
  
-   **初始入侵目標**-一次啟動與小型的組織基礎結構通常一或兩個系統遭到入侵的大部分資訊安全性漏洞。 這些初始事件或進入點的網路，通常會利用弱點可能已獲得修正，但沒有。 常見的漏洞就是：  
  
    -   防毒和反惡意程式碼部署中的間距  
  
    -   不完整修補  
  
    -   過時的應用程式和作業系統  
  
    -   設定不正確  
  
    -   缺少的安全的應用程式開發做法  
  
-   **吸引人的帳戶認證竊取**-認證竊取攻擊是指攻擊者一開始取得 特殊權限的存取權的網路上的電腦並接著會使用免費的工具擷取的其他工作階段的認證登入的帳戶。   
    此章節包含的如下所示：  
  
    -   **增加入侵可能性的活動**-因為高特殊權限的網域帳戶和 「 非常重要的 person 」，認證竊取目標通常是很重要的系統管理員 (VIP) 帳戶增加的認證竊取攻擊成功的可能性的活動。 這些活動包括：  
  
        -   不安全的電腦，使用具有特殊權限的帳戶登入  
  
        -   瀏覽網際網路具有高特殊權限的帳戶  
  
        -   設定本機的特殊權限的帳戶，在系統中相同的認證  
  
        -   Overpopulation 和過度使用的特殊權限的網域群組  
  
        -   沒有足夠的網域控制站的安全性管理。  
  
    -   **權限提高權限和傳用**-特定帳戶、 伺服器和基礎結構元件通常是 Active Directory 的攻擊的主要目標。 這些帳戶是：  
  
        -   永久特殊權限的帳戶  
  
        -   VIP 帳戶  
  
        -   「 特殊權限連結 」 的 Active Directory 帳戶  
  
        -   網域控制站  
  
        -   其他會影響身分識別、 存取和組態管理，例如公開金鑰基礎結構 (PKI) 伺服器和系統管理伺服器的基礎結構服務  
  
## <a name="reducing-the-active-directory-attack-surface"></a>減少 Active Directory 的攻擊面  
本節著重於技術的控制項，以減少 Active Directory 安裝的受攻擊面。 本節包括下列主題：  
  
-   **特殊權限的帳戶和 Active Directory 中的群組**一節說明最高特殊權限的帳戶及群組在 Active Directory 與特殊權限的帳戶受到保護的機制。 Active Directory，內三個內建群組都是最高的權限群組 （Enterprise Admins、 Domain Admins 和系統管理員） 的目錄中，不過其他群組和帳戶的數目也應加以保護。  
  
-   **實作最低權限系統管理模型**節著重於用來識別除了提供建議，以使用高特殊權限的帳戶對於日常管理工作提供的風險降低風險。  
  
過多的權限不只在中找到 Active Directory 遭洩露的環境。 當組織所開發授與比所需的權限的習慣時，它通常可找到整個基礎結構：  
  
-   在 Active Directory 中  
  
-   在成員伺服器上  
  
-   在工作站上  
  
-   在應用程式  
  
-   在 資料存放庫  
  
-   **實作安全的系統管理主機**一節將說明安全的系統管理主機，也就是設定為支援的 Active Directory 與已連線的系統管理的電腦。 這些主控件專用於系統管理功能，並不會執行軟體，例如電子郵件應用程式、 網頁瀏覽器或生產力軟體 （例如 Microsoft Office)。  
  
此章節包含的如下所示：  
  
-   **建立安全的系統管理主機的原則**-一般原則，要牢記在心：  
  
    -   永遠不會管理受信任的系統從信任度較低的主機。  
  
    -   請勿依賴單一認證要素時執行特殊權限的活動。  
  
    -   請記得當設計和實作安全的系統管理主機的實體安全性。  
  
-   **保護網域控制站針對攻擊**-該使用者如果惡意使用者取得特殊權限的存取權的網域控制站，可以修改、 損毀，並終結 Active Directory 資料庫，並由延伸模組的所有系統和帳戶受 Active Directory。  
  
本節包括下列主題：  
  
-   **網域控制站的實體安全性**-包含提供資料中心、 分公司和遠端位置中的網域控制站實體安全性的建議。  
  
-   **網域控制站作業系統**-包含保護網域控制站作業系統的建議。  
  
-   **保護設定的網域控制站**-原生和免費組態工具] 和 [設定可用來建立安全性的後續由群組原則物件 （強制執行的網域控制站的設定基準Gpo)。  
  
## <a name="monitoring-active-directory-for-signs-of-compromise"></a>監視 Active Directory 遭到危害的徵兆  
本節提供有關舊版的稽核類別和稽核原則子類別目錄 （這在 Windows Vista 和 Windows Server 2008 中推出），以及進階稽核原則 （Windows Server 2008 R2 中引進） 的資訊。 也提供事件的相關資訊，並監視該物件可能表示嘗試危害環境與某些其他參考資料，可以用來建構完整的稽核原則的 Active Directory。  
  
本節包括下列主題：  
  
-   **Windows 稽核原則**-Windows 安全性事件記錄檔具有類別目錄，並判斷哪些安全性事件的子類別目錄會追蹤和記錄。  
  
-   **稽核原則建議**-本節描述 Windows 預設稽核原則設定、 稽核原則設定建議的 Microsoft 及組織更積極的建議，用以稽核重要的伺服器和工作站。  
  
## <a name="planning-for-compromise"></a>規劃危害因應措施  
此章節包含將有助組織做好遭到入侵，發生前的建議、 實作控制，可以偵測入侵事件之前發生完整的缺口，並提供在其中的情況下回應並進行復原的指導方針目錄的危害，攻擊者即可達成。 本節包括下列主題：  
  
-   **重新思考方法**-包含原則和指導方針，建立安全的環境，組織可以在其中放置其最重要的資產。 這些指導方針如下所示：  
  
    -   識別用於隔離和保護重要資產的原則  
  
    -   定義有限的、 以風險為基礎的移轉計劃  
  
    -   在必要時，利用 「 nonmigratory 」 移轉  
  
    -   實作 「 creative 解構"  
  
    -   隔離舊版系統和應用程式  
  
    -   為使用者簡化安全性  
  
-   **維護更安全的環境**-包含要做的指導方針，以用來開發不只有效的安全性，但有效的生命週期管理的高階建議。 本節包括下列主題：  
  
    -   **Active directory 中建立以商務為中心的安全性作法**-若要有效地管理使用者、 資料、 應用程式和系統管理的 Active Directory 的生命週期，請遵循這些原則。  
  
        -   **將商務擁有權指派給 Active Directory 資料**-指派擁有權的基礎結構元件 IT; 新增至 Active Directory 網域服務 (AD DS) 以支援業務，比方說，新的員工、 新的應用程式的資料和新的資訊存放庫、 指定的商務單位或使用者應該是與資料相關聯。  
  
        -   **實作 Business-Driven 生命週期管理**-生命週期管理應該實作 Active Directory 中的資料。  
  
        -   **所有的 Active Directory 資料分類**-企業擁有者應提供 Active Directory 中資料的分類。 在資料分類模型中，應該包含下列的 Active Directory 資料的分類：  
  
            -   **系統**-分類 server 母體擴展，其作業系統其角色，以及 IT 上執行的應用程式和企業擁有者的記錄。  
  
            -   **應用程式**-分類功能、 使用者基底，和其作業系統的應用程式。  
  
            -   **使用者**-中最有可能會成為攻擊目標的 Active Directory 安裝的帳戶應該標記，並監視。  
  
## <a name="summary-of-best-practices-for-securing-active-directory-domain-services"></a>保護 Active Directory 網域服務的最佳做法的摘要  
下表提供本文件中提供來保護 AD DS 安裝建議的摘要。 一些最佳作法的本質屬策略性，並需要完整的規劃和實作專案的專案。有些則是戰術，並著重於特定的 Active Directory 及相關基礎結構的元件。  
  
作法所述的優先順序，該是近似的順序，較低的數字表示較高的優先順序。 位置適用的最佳做法會識別為預防或偵測的本質。 所有這些建議應該徹底測試並修改視需要針對貴組織的特性和需求。  
  
  
||**最佳作法**|**戰術或策略**|**預防或偵測**|  
|-|-|-|-|  
|1|修補程式的應用程式。|戰術|預防|  
|2|修補程式的作業系統。|戰術|預防|  
|3|部署並立即在所有系統和嘗試移除或停用它來監視更新防毒軟體和反惡意程式碼軟體。|戰術|兩者|  
|4|監視機密的 Active Directory 物件的修改嘗試和 Windows 的事件，可能表示嘗試的入侵。|戰術|偵測|  
|5|保護和監視的機密資料的存取權的使用者帳戶|戰術|兩者|  
|6|功能強大的帳戶會防止未經授權的系統上使用。|戰術|預防|  
|7|排除高特殊權限的群組中的永久成員資格。|戰術|預防|  
|8|實作控制項，以授與時所需的權限群組中的暫時成員資格。|戰術|預防|  
|9|實作安全的系統管理主機。|戰術|預防|  
|10|使用應用程式允許清單的網域控制站、 系統管理的主機和其他機密的系統上。|戰術|預防|  
|11|識別重要資產，並設定其安全性的優先順序和監視。|戰術|兩者|  
|12|實作的目錄，其支援基礎結構，並加入網域的系統管理的最低權限的角色型存取控制。|策略|預防|  
|13|隔離舊版系統和應用程式。|戰術|預防|  
|14|解除委任舊有系統和應用程式。|策略|預防|  
|15|實作自訂的應用程式的安全性開發生命週期程式。|策略|預防|  
|16|實作組態管理、 定期檢閱合規性以及用於評估每個新的硬體或軟體版本的設定。|策略|預防|  
|17|將重要資產移轉至原有的樹系中，以嚴格的安全性和監視需求。|策略|兩者|  
|18|簡化使用者的安全性。|策略|預防|  
|19|使用主機型防火牆來控制及安全通訊。|戰術|預防|  
|20|修補程式的裝置。|戰術|預防|  
|21|實作業務為核心的生命週期管理的 IT 資產。|策略|N/A|  
|22|建立或更新事件的復原計劃。|策略|N/A|  
  

