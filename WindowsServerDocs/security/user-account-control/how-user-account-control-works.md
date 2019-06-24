---
title: 使用者帳戶控制的運作方式
description: Windows Server 安全性
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tpm
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da83ddb2-6182-417c-aa8e-0b47b2e17d13
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 7f5ad234959ebfe0687b8bc10f9e43f2092252f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823549"
---
# <a name="how-user-account-control-works"></a>使用者帳戶控制的運作方式

>適用於：Windows Server （半年通道），Windows Server 2016

使用者帳戶控制 (UAC) 有助於防止惡意程式 (又稱為惡意程式碼) 破壞電腦，還可以幫助組織部署最佳管理桌面。 使用 UAC，應用程式和作業一律在非系統管理員帳戶的資訊安全內容下執行，除非系統管理員特別授與系統的系統管理員層級存取權。 UAC 可以封鎖未經授權應用程式的自動安裝，以及防止意外變更系統設定。

## <a name="uac-process-and-interactions"></a>UAC 處理程序和互動
每一個需要系統管理員存取權杖的應用程式，必須向系統管理員顯示提示以取得同意。 其中一個例外狀況是父系處理程序和子處理程序間存在的關係。 子處理程序會繼承父系處理程序的使用者存取權杖。 不過，父系和子處理程序二者的整合層級必須相同。 Windows Server 2012 來標記它們的完整性層級保護程序。 整合層級的衡量依據是信任。 「高」整合應用程式負責執行修改系統資料的工作，例如磁碟分割應用程式，「低」整合應用程式則負責執行可能破壞作業系統的工作，例如網頁瀏覽器。 整合層級較低的應用程式無法修改整合層級較高的應用程式資料。 當標準使用者嘗試執行的應用程式需要系統管理員存取權杖，UAC 會要求使用者提供有效的系統管理員認證。

若要深入了解此程序發生請務必檢閱 Windows Server 2012 的登入程序的詳細資料。

### <a name="windows-server-2012-logon-process"></a>Windows Server 2012 Logon Process
下圖說明系統管理員及標準使用者的登入程序有何不同：

![示範如何將系統管理員身分登入程序不同於標準使用者的登入程序圖](../media/How-User-Account-Control-Works/UACWindowsLogonProcess.gif)

根據預設值，標準使用者和系統管理員會在標準使用者的資訊安全內容中存取資源以及執行應用程式。 當使用者登入電腦後，系統會為使用者建立存取權杖。 存取權杖包含授與使用者的存取權層級相關資訊，其中包括特定安全性識別碼 (SID) 以及 Windows 權限。

當系統管理員登入後，會為使用者建立兩個獨立的存取權杖：一個是標準使用者存取權杖，另一個是系統管理員存取權杖。 標準使用者存取權杖和系統管理員存取權杖包含相同的使用者特定資訊，但不包含 Windows 系統管理權限和 SID。 標準使用者存取權杖是用來啟動那些不執行系統管理工作的應用程式 (標準使用者應用程式)。 標準使用者存取權杖之後會再用來顯示桌面 (Explorer.exe)。 Explorer.exe 是父系處理程序，所有其他使用者啟動的處理程序都會繼承其存取權杖。 因此，除非使用者同意或者提供認證來核准應用程式使用完整的系統管理存取權杖，否則所有應用程式會以標準使用者的身分執行。

使用者是 Administrators 群組的成員可以登入、 瀏覽網頁，並閱讀電子郵件使用標準使用者存取權杖。 當系統管理員需要執行的工作需要系統管理員存取權杖，而 Windows Server 2012 自動提示取得使用者核准。 這個提示稱為提高權限提示，使用本機安全性原則嵌入式管理單元 (Secpol.msc) 或群組原則，即可設定其行為。

> [!NOTE]
> 詞彙 「 提高 」 用來參考，會提示使用者同意或認證，使用完整系統管理員存取權杖的 Windows Server 2012 中的程序。

### <a name="the-uac-user-experience"></a>UAC 使用者體驗
啟用 UAC 之後，標準使用者與管理員核准模式下的系統管理員，會有不同的體驗。 執行 Windows Server 2012 的更安全的建議方法是將您主要的使用者帳戶的標準使用者帳戶。 以標準使用者身分執行有助於大幅提升受管理環境的安全性。 使用內建的 UAC 提高權限元件，標準使用者可以輸入本機 Administrator 帳戶的有效認證，輕鬆執行系統管理工作。 標準使用者的預設內建 UAC 提高權限元件，就是指認證提示。

如果不想使用標準使用者身分執行，可以管理員核准模式下的系統管理員身分執行。 使用內建的 UAC 提高權限元件，本機 Administrators 群組的成員可以輕鬆執行系統管理工作提供核准。 管理員核准模式下，系統管理員的預設內建 UAC 提高權限元件，稱為同意提示。 使用本機安全性原則嵌入式管理單元 (Secpol.msc) 或群組原則，可以設定 UAC 提高權限提示行為。

**同意和認證提示**

啟用 UAC 之後，使用 Windows Server 2012 提示使用者同意，或啟動的程式或工作需要完整系統管理員存取權杖之前會提示輸入有效的本機系統管理員帳戶的認證。 此提示可以確保惡意軟體無法進行無訊息安裝。

**同意提示**

當使用者嘗試執行需要使用者系統管理存取權杖的工作時，就會顯示同意提示。 以下是 UAC 同意提示的螢幕擷取畫面。

![UAC 同意提示的螢幕擷取畫面](../media/How-User-Account-Control-Works/UACConsentPrompt.gif)

**認證提示**

當標準使用者嘗試執行需要使用者系統管理存取權杖的工作時，就會顯示認證提示。 您可以使用本機安全性原則嵌入式管理單元 (Secpol.msc) 或群組原則，設定此標準使用者預設提示行為。 系統管理員也必須提供其認證，藉由設定 使用者帳戶控制：將值設定為提示字元中，認證管理員核准模式原則中的系統管理員的提高權限提示行為。

以下是 UAC 認證提示範例的螢幕擷取畫面。

![顯示 UAC 認證提示的範例螢幕擷取畫面](../media/How-User-Account-Control-Works/UACCredentialPrompt.gif)

**UAC 提高權限提示**

UAC 提高權限提示會依應用程式標示不同顏色，讓您可以立即識別應用程式的潛在安全性風險。 當應用程式嘗試以系統管理員的完整存取權杖執行時，Windows Server 2012 首先會分析可執行檔，判斷其發行者。 應用程式第一次可分成三個可執行檔的 「 發行者 」 為基礎的類別：Windows Server 2012，驗證的發行者 （帶正負號），以及未驗證發行者 （不帶正負號）。 下圖說明 Windows Server 2012 如何決定向使用者顯示哪個色彩提高權限提示。

以下是提高權限提示的色彩編碼：

-   紅色背景加上紅色保護盾圖示：應用程式群組原則封鎖或封鎖的發行者。

-   藍色背景加藍色和金色保護盾圖示：應用程式是 Windows Server 2012 管理應用程式，例如控制台項目。

-   藍色背景加藍色保護盾圖示：應用程式由使用 Authenticode 簽署，並在本機電腦信任。

-   黃色背景加黃色保護盾圖示：在應用程式是不帶正負號或帶正負號，但尚未信任由本機電腦。

**保護盾圖示**

部分控制台項目，如 [日期和時間內容]，包含系統管理員和標準使用者作業的結合。 標準使用者可以查看時鐘以及變更時區，不過要想變更本機系統時間，就需要完整系統管理員存取權杖。 以下是 [日期和時間內容] 控制台項目的螢幕擷取畫面。

![螢幕擷取畫面顯示 * * 的日期和時間內容 控制台項目](../media/How-User-Account-Control-Works/UACShieldIcon.gif)

[變更日期和時間] 按鈕上的保護盾圖示代表該處理程序需要完整的系統管理員存取權杖，而且會顯示 UAC 提高權限提示。

**保護提高權限提示**

將提示導向安全桌面，可以進一步保護提高權限處理程序。 根據預設，Windows Server 2012 中，同意和認證提示會顯示在安全桌面上。 只有 Windows 處理程序可以存取安全桌面。 較高的層級的安全性，我們建議您繼續**使用者帳戶控制：提示提高權限時切換到安全桌面**啟用的原則設定。

可執行檔要求提高權限時，互動式桌面 (又稱為使用者桌面) 會切換至安全桌面。 安全桌面會將使用者桌面變暗，並顯示提高權限提示，您必須先回應該提示，才能繼續後續動作。 當使用者按一下 [是]，或不可以，桌面會切換回使用者桌面。

惡意程式碼會模仿安全桌面，但是使用者帳戶控制：在原則設定為提示要求同意的管理員核准模式的系統管理員的提高權限提示的行為，惡意程式碼不會得到提高權限如果使用者按一下 [是]，在仿造。 如果原則設定設為 提示認證，模仿認證提示的惡意程式碼可以從使用者蒐集認證。 不過，惡意程式碼不會得到提高後的權限而且系統會採取其他保護措施，讓惡意程式碼即使使用蒐集到的密碼也無法控制使用者介面。

雖然惡意程式碼會模仿安全桌面，不過除非使用者以前將惡意程式碼安裝到電腦上，否則不會發生這種問題。 由於啟用 UAC 之後，需要系統管理員存取權杖的處理程序就無法進行無訊息安裝，因此使用者必須按一下 [是]，或提供系統管理員認證，明確表示同意安裝該處理程序。 UAC 提高權限提示的具體行為，取決於群組原則的設定。

## <a name="uac-architecture"></a>UAC 架構
下圖提供 UAC 架構的詳細資訊。

![詳述 UAC 架構的圖表](../media/How-User-Account-Control-Works/UACArchitecture.gif)

若要進一步了解每個元件，請檢閱下表：

|Component|描述|
|-------|--------|
|**使用者**||
|使用者執行需要權限的作業|如果作業變更了檔案系統或登錄，則會呼叫  Virtualization 。 所有其他作業會呼叫 ShellExecute。|
|ShellExecute|ShellExecute 會呼叫 CreateProcess。 ShellExecute 會從 CreateProcess 尋找 ERROR_ELEVATION_REQUIRED 錯誤。 如果收到錯誤，ShellExecute 便會呼叫應用程式資訊服務，試著藉由提高權限提示來執行要求的工作。|
|CreateProcess|如果應用程式需要提高權限，CreateProcess 會使用  ERROR_ELEVATION_REQUIRED 拒絕要求。|
|**System**||
|應用程式資訊服務|一種系統服務，可以協助啟動那些需要一或多個提高的權限或使用者權限才能執行的應用程式，例如本機系統管理作業，以及需要更高整合層級的應用程式。 當需要提高權限且使用者同意 (取決於群組原則) 啟動這類應用程式後，應用程式資訊服務會使用系統管理使用者完整存取權杖為應用程式建立新的處理程序，幫助啟動應用程式。|
|提高權限的 ActiveX 安裝|如果未安裝 ActiveX，系統會檢查 UAC 滑桿等級。 如果已安裝 ActiveX，**使用者帳戶控制：提示提高權限時切換到安全桌面**核取群組原則設定。|
|檢查 UAC 滑桿等級|UAC 現在有 4 個通知等級可以選擇，還有一個用於選擇通知等級的滑桿：<br /><br /><ul><li>高<br /><br />    如果滑桿設定為 [一律通知]，系統會檢查是否已經啟用安全桌面。</li><li>中等<br /><br />    如果滑桿設定為**預設通知程式嘗試變更我的電腦時，才我**，則**使用者帳戶控制：僅提高經簽署及驗證的可執行檔**核取原則設定：<br /><br /><ul><li>如果啟用該原則設定，在允許執行指定的可執行檔之前，會先強制執行公開金鑰基礎架構 (PKI) 憑證路徑驗證。</li><li>如果沒有啟用該原則設定 (預設值)，在允許執行指定的可執行檔之前，不會強制執行 PKI 憑證路徑驗證。 **使用者帳戶控制：提示提高權限時切換到安全桌面**核取群組原則設定。</li></ul></li><li>低<br /><br />    如果滑桿是設定成 [程式嘗試變更我的電腦時才通知我 (不要將桌面變暗)]，則會呼叫 CreateProcess。</li><li>不要通知<br /><br />    如果滑桿設定為**不要通知我時**，UAC 提示將永遠不會通知程式會嘗試安裝，或嘗試在電腦上進行任何變更時。 **重要事項：**   不建議使用這項設定。 這個設定等同於設定**使用者帳戶控制：在管理員核准模式的系統管理員的提高權限提示行為**原則設定，以**提高權限，而不提示**。</li></ul>|
|安全桌面已啟用|**使用者帳戶控制：提示提高權限時切換到安全桌面**核取原則設定：<br /><br />-如果啟用安全桌面，則所有提高權限要求會移至安全桌面，無論系統管理員和標準使用者的提示行為原則設定。<br />-如果未啟用安全的桌面，則所有提高權限要求會傳送至互動式使用者桌面，並會使用系統管理員和標準使用者的每個使用者設定。|
|CreateProcess|CreateProcess 會呼叫 AppCompat、融合以及安裝程式偵測，評估應用程式是否需要提高權限。 然後會檢查可執行檔，判斷它要求的執行層級 (儲存在可執行檔的應用程式資訊清單中)。 如果資訊清單中指定之要求的執行層級與存取權杖不符，CreateProcess 就會失敗，並將錯誤 (ERROR_ELEVATION_REQUIRED) 傳回 ShellExecute。 |
|AppCompat|AppCompat 資料庫儲存應用程式的相容性更正項目資訊。|
|融合|融合資料庫儲存描述應用程式之應用程式資訊清單的資訊。 系統會更新資訊清單架構描述，以增加新要求的執行層級欄位。|
|安裝程式偵測|安裝程式偵測會偵測安裝程式可執行檔，有助於防止在使用者不知情且未同意的情況下執行安裝。|
|**核心**||
|虛擬化|虛擬化技術可以確保不相容的應用程式不會無訊息失敗，或者在不明情況下失敗。 UAC 也會為要在受保護區域中寫入資料的應用程式，提供檔案和登錄模擬以及紀錄功能。|
|檔案系統和登錄|每個使用者檔案和登錄模擬都會將每部電腦登錄和檔案寫入要求，重新導向到對等的每個使用者位置。 讀取要求會先重新導向到虛擬化的每個使用者位置，然後再到每部電腦位置。|

沒有從 Windows 上的舊版 Windows Server 2012 uac 變更。 新的滑桿將永遠不會將 UAC 完全關閉。 將新的設定：

-   保留 UAC 服務執行。

-   原因所有提高權限要求會自動核准而不會顯示 UAC 提示的系統管理員所起始。

-   自動拒絕所有標準使用者的提高權限要求。

> [!IMPORTANT]
> 您必須停用原則才能完全停用 UAC**使用者帳戶控制：以系統管理員核准模式中執行所有系統管理員**。

> [!WARNING]
> 量身打造的應用程式無法在 Windows Server 2012 時停用 UAC。

### <a name="virtualization"></a>虛擬化
企業環境中的系統管理員為了保護系統，所以很多特定業務 (LOB) 應用程式都設計為只能使用標準使用者存取權杖。 如此一來，IT 系統管理員不需要執行 Windows Server 2012 啟用 uac 時取代大部分的應用程式。

 Windows Server 2012 包含應用程式，UAC 不相容，以及需要系統管理員存取權杖，才能正確執行的檔案及登錄虛擬化技術。 虛擬化可確保即使 UAC 不相容的應用程式與 Windows Server 2012 相容。 與 UAC 不相容的系統管理應用程式嘗試在受保護的目錄 (例如 Program Files) 寫入資料時，UAC 會針對要嘗試變更的資源，提供該應用程式專屬的虛擬化檢視。 虛擬化複本會保留在使用者設定檔中。 此策略會針對執行不相容之應用程式的每個使用者建立個別的虛擬化檔案複本。

大部分應用程式工作都可以使用虛擬化功能正常運作。 雖然虛擬化可讓大部分應用程式順利執行，但這只是短期的修復，而非長期解決之道。 應用程式開發人員應該修改他們的應用程式是與 Windows Server 2012 標誌計劃，盡相容，而不是依賴檔案、 資料夾與登錄虛擬化。

虛擬化不適用於下列案例：

1.  虛擬化不適用於以完整系統管理存取權杖提升權限並執行的應用程式。

2.  虛擬化僅支援 32 位元的應用程式。 未提高權限的 64 位元應用程式嘗試取得 Windows 物件的控制碼 (唯一識別碼) 時，只會收到拒絕存取訊息。 原生 Windows 64 位元應用程式必須與 UAC 相容並將資料寫入正確位置。

3.  如果應用程式包含具有要求之執行層級屬性的應用程式資訊清單，則會停用應用程式的虛擬化。

### <a name="request-execution-levels"></a>要求執行層級
應用程式資訊清單是一種 XML 檔案，描述以及識別應用程式在執行階段應繫結的共用以及私用並排組件。 在 Windows Server 2012，應用程式資訊清單包含 UAC 應用程式相容性的項目。 在應用程式資訊清單中包含項目的系統管理應用程式，會提示使用者提供存取使用者存取權杖的權限。 雖然大部分系統管理應用程式在應用程式資訊清單中沒有相關的項目，但是還是可以使用應用程式相容性修正執行，且不需進行修改。 應用程式相容性修正是資料庫項目，讓 UAC 不相容才能正常使用 Windows Server 2012 的應用程式。

所有與 UAC 相容的應用程式都應該在應用程式資訊清單中加入要求的執行層級。 如果應用程式需要系統的系統管理存取權，將應用程式要求的執行層級標示為「需要系統管理員」，可以確保系統將此程式識別為系統管理應用程式，然後執行必要的提高權限步驟。 要求的執行層級會指定應用程式所需的權限。

### <a name="installer-detection-technology"></a>安裝程式偵測技術
安裝程式是為了部署軟體而設計的應用程式。 大部分的安裝程式會寫入系統目錄以及登錄機碼。 在安裝程式偵測技術中，這些受保護的系統位置通常只有系統管理員才能寫入資料，這表示標準使用者沒有足夠的存取權可以安裝程式。 Windows Server 2012 會啟發式偵測安裝程式並要求系統管理員認證或系統管理員使用者核准，才能存取權限執行。 Windows Server 2012 也會啟發式偵測更新，以及解除安裝應用程式的程式。 UAC 的設計目標之一就是防止在使用者不知情和未同意的情況下執行安裝，因為安裝程式會在檔案系統與登錄的受保護區域寫入資料。

安裝程式偵測只適用於下列各項：

-   32 位元可執行檔。

-   不具備要求的執行層級屬性的應用程式。

-   以標準使用者身分執行且啟用 UAC 的互動式處理程序。

建立 32 位元處理程序之前，會檢查下列屬性以判斷是否為安裝程式：

-   檔案名稱包含如 install、setup 或 update 等關鍵字。

-   版本控制資源欄位包含下列關鍵字：廠商、 公司名稱、 產品名稱、 檔案描述、 原始檔名、 內部名稱，以及匯出名稱。

-   內嵌到可執行檔的並排資訊清單關鍵字。

-   可執行檔連結的特定 StringTable 項目關鍵字。

-   可執行檔連結的資源指令碼資料機碼屬性。

-   可執行檔中有目標位元組序列。

> [!NOTE]
> 關鍵字和位元組序列是從各種安裝程式技術觀察到的一般特性衍生而來。

> [!NOTE]
> 使用者帳戶控制：偵測應用程式安裝，並提示提高權限的原則設定必須啟用，安裝程式偵測才能偵測安裝程式。 這項設定預設為啟用，且可以使用本機安全性原則嵌入式管理單元 (Secpol.msc) 在本機進行設定，或使用群組原則 (Gpedit.msc) 為網域、OU 或特定群組進行設定。

