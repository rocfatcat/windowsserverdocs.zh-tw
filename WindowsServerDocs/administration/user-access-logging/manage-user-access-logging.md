---
title: 管理使用者存取記錄
description: 說明如何管理使用者存取記錄
ms.topic: article
ms.assetid: 4f039017-4152-47eb-838e-bb6ef730b638
author: brentfor
ms.author: brentf
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0c2380c27d6d08e788658cf946f92322c3a1eabb
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628133"
---
# <a name="manage-user-access-logging"></a>管理使用者存取記錄

>適用於：Windows Server (半年通道)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

本文件說明如何管理使用者存取記錄 (UAL)。

UAL 是一項功能，可協助伺服器系統管理員量化本機伺服器上角色和服務的唯一用戶端要求數量。

預設會安裝和啟用 UAL，並以幾乎即時的方式收集資料。 UAL 只有幾個設定選項。 本文件將說明這些選項以及其使用目的。

若要深入瞭解 UAL 的優點，請參閱 [開始的使用者存取記錄](get-started-with-user-access-logging.md)。

**本文件內容**

本文件涵蓋的設定選項包括：

-   停用和啟用 UAL 服務

-   收集和移除資料

-   刪除 UAL 記錄的資料

-   在高容量環境下管理 UAL

-   從損毀狀態中修復

-   啟用工作資料夾使用量授權追蹤

## <a name="disabling-and-enabling-the-ual-service"></a><a name="BKMK_Step1"></a>停用和啟用 UAL 服務
當您第一次安裝並啟動執行 Windows Server 2012 或更新版本的電腦時，預設會啟用並執行 UAL。 系統管理員可能要關閉並停用 UAL 才能符合隱私權需求或其他操作的需求。 您可以使用 [服務] 主控台、從命令列或使用 PowerShell Cmdlet 來關閉 UAL。 不過，若要確保下次電腦啟動時，UAL 不會再次執行，您也必須停用服務。 下列程式描述如何關閉和停用 UAL。

> [!NOTE]
> 您可以使用 `Get-Service UALSVC` PowerShell Cmdlet 來擷取 UAL 服務的相關資訊，包括 UAL 服務是執行中還是已停止，以及 UAL 服務是啟用還是停用狀態的資訊。

#### <a name="to-stop-and-disable-the-ual-service-by-using-the-services-console"></a>使用服務主控台來停止和停用 UAL 服務

1.  使用具有本機系統管理員權限的帳戶登入伺服器。

2.  在 [伺服器管理員] 中，指向 [工具]****，然後按一下 [服務]****。

3.  向下捲動並選取 **User Access Logging Service**。按一下 [停止服務]****。

4.  以滑鼠右鍵 \- 按一下服務名稱，然後選取 [ **屬性**]。 在 [一般]**** 索引標籤上，將 [啟動類型]**** 變更為 [已停用]****，然後按一下 [確定]****。

#### <a name="to-stop-and-disable-ual-from-the-command-line"></a>從命令列停止和停用 UAL

1.  使用具有本機系統管理員權限的帳戶登入伺服器。

2.  按 Windows 標誌 + R，然後輸入 **cmd** 以開啟命令提示字元視窗。

    > [!IMPORTANT]
    > 如果出現 [**使用者帳戶控制**] 對話方塊，請確認它所顯示的動作就是您所需的動作，然後按一下 [**是**]。

3.  輸入 **net stop ualsvc**，然後按 ENTER。

4.  輸入 **netsh ualsvc set opmode mode=disable**，然後按 ENTER。

下列 Windows PowerShell Cmdlet 執行與前述程序相同的功能。 在單一行中，輸入各個 Cmdlet (即使因為格式限制，它們可能會在這裡出現自動換行成數行)。

您也可以使用 Windows PowerShell 命令的 Stop-service 和 Disable-Ual 來停止和停用 UAL。

```
Stop-service ualsvc
```

```
Disable-ual
```

如果您稍後想要重新開機並重新啟用 UAL，您可以使用下列程式來執行此動作。

#### <a name="to-start-and-enable-the-ual-service-by-using-the-services-console"></a>使用服務主控台來啟動和啟用 UAL 服務

1.  使用具有本機系統管理員權限的帳戶登入伺服器。

2.  在 [伺服器管理員] 中，指向 [工具]****，然後按一下 [服務]****。

3.  向下捲動並選取 **User Access Logging Service**。按一下 [啟動服務]****。

4.  以滑鼠右鍵按一下服務名稱，然後選取 [內容]****。 在 [一般]**** 索引標籤上，將 [啟動類型]**** 變更為 [自動]****，然後按一下 [確定]****。

#### <a name="to-start-and-enable-ual-from-the-command-line"></a>從命令列啟動和啟用 UAL

1.  使用本機系統管理員認證登入伺服器。

2.  按 Windows 標誌 + R，然後輸入 **cmd** 以開啟命令提示字元視窗。

    > [!IMPORTANT]
    > 如果出現 [**使用者帳戶控制**] 對話方塊，請確認它所顯示的動作就是您所需的動作，然後按一下 [**是**]。

3.  輸入 **net start ualsvc**，然後按 ENTER。

4.  輸入 **netsh ualsvc set opmode mode=enable**，然後按 ENTER。

下列 Windows PowerShell Cmdlet 執行與前述程序相同的功能。 在單一行中，輸入各個 Cmdlet (即使因為格式限制，它們可能會在這裡出現自動換行成數行)。

您也可以使用 Windows PowerShell 命令的 Start-service 和 Enable-Ual 來啟動和重新啟用 UAL。

```
Enable-ual
```

```
Start-service ualsvc
```

## <a name="collecting-ual-data"></a><a name="BKMK_Step2"></a>收集 UAL 資料
除了上一節所述的 PowerShell Cmdlet，還可以使用12個額外的 Cmdlet 來收集 UAL 資料：

-   **Get-UalOverview**：提供已安裝產品和角色的 UAL 相關詳細資料和歷程記錄。

-   **Get-UalServerUser**：提供本機或目標伺服器的用戶端使用者存取資料。

-   **Get-UalServerDevice**：提供本機或目標伺服器的用戶端裝置存取資料。

-   **Get-UalUserAccess**：提供在本機或目標伺服器上安裝的每個角色或產品的用戶端使用者存取資料。

-   **Get-UalDeviceAccess**：提供在本機或目標伺服器上安裝的每個角色或產品的用戶端裝置存取資料。

-   **Get-UalDailyUserAccess**：提供一年中每一天的用戶端使用者存取資料。

-   **Get-UalDailyDeviceAccess**：提供一年中每一天的用戶端裝置存取資料。

-   **Get-UalDailyAccess**：提供一年中每一天的用戶端裝置和使用者存取資料。

-   **Get-UalHyperV**：提供與本機或目標伺服器相關的虛擬機器資料。

-   **Get-UalDns**：提供本機或目標 DNS 伺服器的 DNS 用戶端特定資料。

-   **Get-UalSystemId**：提供可唯一識別本機或目標伺服器的系統特定資料。

`Get-UalSystemId` 的目的在於提供伺服器的唯一設定檔，讓該伺服器的所有其他資料都可以與該設定檔關聯。如果伺服器在建立新設定檔的其中一個參數時遇到任何變更 `Get-UalSystemId` 。  `Get-UalOverview` 可為系統管理員提供伺服器上安裝和使用的角色清單。

> [!NOTE]
> 預設會安裝列印和檔服務和檔案服務的基本功能。 因此，系統管理員永遠會看到這些服務的相關資訊，就像是安裝了完整的角色一樣。由於 UAL 要為 Hyper-V 和 DNS 收集獨特的資料，因此另外提供有這些伺服器角色的 UAL Cmdlet。

UAL Cmdlet 的典型使用案例是讓系統管理員查詢 UAL 在某個日期範圍內的唯一用戶端存取。您可利用多種方法來完成這個動作。下列是查詢某一日期範圍內唯一裝置存取的建議方法。

```
PS C:\Windows\system32>Gwmi -Namespace "root\AccessLogging" -query "SELECT * FROM MsftUal_DeviceAccess WHERE LastSeen >='1/01/2013' and LastSeen <='3/31/2013'"

```

這會依 IP 位址傳回在該日期範圍內提出伺服器要求的所有唯一用戶端裝置的詳細資訊清單。

每個唯一用戶端的 ' ActivityCount ' 限制為每天65535。此外，只有依日期查詢時才需要從 PowerShell 呼叫 WMI。所有其他 UAL Cmdlet 參數皆可如預期般在 PS 查詢中使用，如下列範例所示：

```
PS C:\Windows\system32> Get-UalDeviceAccess -IPAddress "10.36.206.112"

ActivityCount    : 1
FirstSeen        : 6/23/2012 5:06:50 AM
IPAddress        : 10.36.206.112
LastSeen         : 6/23/2012 5:06:50 AM
ProductName      : Windows Server 2012 Datacenter
RoleGuid         : 10a9226f-50ee-49d8-a393-9a501d47ce04
RoleName         : File Server
TenantIdentifier : 00000000-0000-0000-0000-000000000000
PSComputerName

```

UAL 最多可保留兩年的歷程記錄。 若要在服務執行時允許系統管理員抓取 UAL 資料，UAL 會將使用中資料庫檔案的副本（目前的 .mdb）複製 *到每 24* 小時的檔案，以供 WMI 提供者使用。

UAL 會在一年中的第一天建立新的 *GUID.mdb*。 舊的 *GUID .mdb* 會保留為提供者使用的封存。  兩年之後，就會覆寫原始的 *GUID.mdb*。

> [!IMPORTANT]
> 只有進階使用者才能執行下列程序，通常是由開發人員在測試本身的 UAL 應用程式開發介面檢測時使用...

#### <a name="to-adjust-the-default-24-hour-interval-to-make-data-visible-to-the-wmi-provider"></a>調整預設的 24 小時間隔讓 WMI 提供者看到資料

1.  使用具有本機系統管理員權限的帳戶登入伺服器。

2.  按 Windows 標誌 + R，然後輸入 **cmd** 以開啟命令提示字元視窗。

3.  新增登錄值：  **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\WMI\AutoLogger\Sum\PollingInterval (REG_DWORD)**。

    > [!WARNING]
    > 不正確地編輯登錄可能會對系統造成嚴重的損害。 變更登錄之前，應先備份電腦上的重要資料。

    下列範例顯示如何新增兩分鐘的間隔 (不建議做為長期執行狀態) ： **REG add HKLM\System\CurrentControlSet\Control\WMI \\ AutoLogger\Sum/v POLLINGINTERVAL/T REG \_ DWORD/d 120000/f**

    時間值以毫秒為單位。 最小值是 60 秒，最大值是 7 天，預設是 24 小時。

4.  使用服務主控台停止和重新啟動 User Access Logging Service。

## <a name="deleting-data-logged-by-ual"></a>刪除 UAL 記錄的資料
UAL 並不是做為關鍵元件使用。 它的設計目的是為了在維護高度可靠性的同時，儘可能減少對本機系統作業的影響。 這也可讓系統管理員以手動方式刪除 \Windows\System32\LogFilesSUM\) 目錄中每個檔案 (的 UAL 資料庫和支援檔案，以符合營運需求。

#### <a name="to-delete-data-logged-by-ual"></a>刪除 UAL 記錄的資料

1. 停止 User Access Logging Service。

2. 開啟 [Windows 檔案總管]。

3. 移至**\Windows\System32\Logfiles\SUM \\ **。

4. 刪除資料夾中的所有檔案。

## <a name="managing-ual-in-high-volume-environments"></a>在高容量環境下管理 UAL
本節說明系統管理員在具有大量用戶端的伺服器上使用 UAL 時會遇到的情況：

UAL 可以記錄的存取數目上限為每天 65,535 個。不建議在直接連線到網際網路的伺服器上 (例如直接連線到網際網路的網頁伺服器)，或當伺服器的主要功能是提供極高效能的情況下 (例如在 HPC 工作負載環境) 使用 UAL。 UAL 主要是用在預期有高容量的小型、中型和企業內部網路案例中，但不能像在一般情況下提供網際網路對應流量的許多部署一樣高。

**記憶體中的 UAL**：因為 UAL 使用可延伸儲存引擎 (ESE) ，所以 UAL 的記憶體需求會隨著時間而增加 (或) 的用戶端要求數量增加。 但是當系統要求記憶體將對系統效能的影響降到最低時，將會釋放記憶體。

**磁片上的 UAL**： UAL 的硬碟需求大約如下所示：

-   0 個唯一用戶端記錄：22M

-   50,000 個唯一用戶端記錄：80 M

-   500,000 個唯一用戶端記錄：384M

-   1,000,000 個唯一用戶端記錄：729M

## <a name="recovering-from-a-corrupt-state"></a>從損毀狀態中修復
本節將討論 UAL 如何使用可延伸儲存引擎 (ESE) ，以及當 UAL 資料已損毀或無法復原時，系統管理員可以執行的動作。

UAL 使用 ESE 來最佳化系統資源的使用方式，並且防止資料損毀。  如需 ESE 優點的詳細資訊，請參閱 MSDN 上的 [可延伸儲存引擎](/windows/win32/extensible-storage-engine/extensible-storage-engine) 。

每次 UAL 服務啟動時，ESE 就會執行軟修復。 如需詳細資訊，請參閱 MSDN 上的 [可延伸儲存引擎檔案](/windows/win32/extensible-storage-engine/extensible-storage-engine-files) 。

如果軟修復發生問題，ESE 會執行損毀修復。 如需詳細資訊，請參閱 MSDN 上的 [JetInit 函式](/windows/win32/extensible-storage-engine/jetinit-function) 。

如果仍然無法使用現有的 ESE 檔案集來啟動 UAL，將會刪除 \Windows\System32\LogFiles\SUM\ 目錄中的所有檔案。 這些檔案刪除之後， User Access Logging Service 會重新啟動並建立新的檔案。 UAL 服務將會繼續執行，就像是在全新安裝的電腦上執行一樣。

> [!IMPORTANT]
> 絕對不能移除或修改 UAL 資料庫目錄中的檔案。 這樣做會起始修復步驟，包括本節所述的清理常式。 如果需要備份 \Windows\System32\LogFiles\SUM\ 目錄，則必須備份此目錄中的所有檔案，這樣還原操作才能如預期運作。

## <a name="enable-work-folders-usage-license-tracking"></a>啟用工作資料夾使用量授權追蹤
工作資料夾伺服器可以使用 UAL 來報告用戶端使用量。 不同於 UAL，工作資料夾記錄預設不會開啟。 您可以使用下列 regkey 變更來開啟它：

```
Reg add HKLM\Software\Microsoft\Windows\CurrentVersion\SyncShareSrv /v EnableWorkFoldersUAL /t REG_DWORD /d 1
```

加入 regkey 之後，您必須重新啟動伺服器上的 SyncShareSvc 服務，以啟用記錄。

啟用記錄之後，每當用戶端連線至伺服器時，2 個資訊事件會記錄到 Windows 記錄\應用程式通道。 對於「工作資料夾」，每個使用者可以有連線至伺服器的一或多個用戶端裝置，並且每 10 分鐘檢查資料更新。 如果伺服器有 1000 位使用者，每位使用者都有 2 個裝置的應用程式記錄檔將會每隔 70 分鐘覆寫，這樣會使疑難排解不相關的問題變得困難。 若要避免這種情況，您可以暫時停用使用者存取記錄服務，或增加伺服器 Windows Logs\Application 通道的大小。

## <a name="see-also"></a><a name="BKMK_Links"></a>另請參閱

- [使用使用者存取記錄進行開始](get-started-with-user-access-logging.md)