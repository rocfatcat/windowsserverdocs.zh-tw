---
ms.assetid: 2f4b6641-0ec2-4b1c-85fb-a1f1d16685c8
title: 叢集感知更新進階選項和更新執行設定檔
ms.topic: article
ms.prod: windows-server-threshold
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 08/06/2018
description: 如何設定進階的選項和更新執行設定檔的叢集感知更新 (CAU)
ms.openlocfilehash: 5fac31ad35422e623b98caaabdd9eae183e2e5d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830549"
---
# <a name="cluster-aware-updating-advanced-options-and-updating-run-profiles"></a>叢集感知更新進階選項和更新執行設定檔

>適用於：Windows Server （半年通道），Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012

本主題說明可以設定的更新執行 」 選項[Cluster-aware Updating](cluster-aware-updating.md) (CAU) 「 更新執行。 當您使用 CAU UI 或 CAU Windows PowerShell cmdlet 套用更新，或設定自行更新選項時，可以設定這些進階的選項。

大部分組態設定都可儲存成 XML 檔案，這稱為更新執行設定檔，可在之後的更新執行重複使用。 CAU 提供的「更新執行」選項預設值也可用於許多叢集環境。

如需您可為每個更新執行指定的其他選項與更新執行設定檔的相關資訊，請參閱本主題稍後的下列各節：

您可以指定更新執行使用更新執行設定檔 」 選項可以設定 「 更新執行設定檔中的要求時的選項

下表列出您可在 CAU 更新執行設定檔中設定的選項。 

> [!NOTE] 
> 若要設定 [PreUpdateScript 或 PostUpdateScript] 選項，請確定安裝 Windows PowerShell 和.NET Framework 4.6 或 4.5 和叢集中的每個節點上已啟用 PowerShell 遠端。 如需詳細資訊，請參閱 < 設定節點以進行中的遠端管理[需求和叢集感知更新的最佳做法](cluster-aware-updating-requirements.md)。


|選項|預設值|詳細資料|  
|------------|-------------------|-------------|  
|**StopAfter**|不限時間|如果「更新執行」經過此時間 (分鐘) 尚未完成，則將予以停止。 **注意：** 如果您指定更新前或更新後的 PowerShell 指令碼，執行指令碼和執行更新的整個程序必須是完整內**StopAfter**時間限制。|  
|**WarnAfter**|根據預設，不會顯示警告|如果「更新執行」(包括已設定的更新前指令碼及更新後指令碼) 經過此時間 (分鐘) 尚未完成，則將出現警告。|  
|**MaxRetriesPerNode**|3|更新處理程序 (包括已設定的更新前指令碼及更新後指令碼) 在每個節點的重試次數上限。 上限為 64。|  
|**MaxFailedNodes**|對大部分叢集而言，這個整數大概是叢集節點數的三分之一。|更新可以失敗的最大節點數，這可能是因為節點失敗或叢集服務停止執行。 如果再有一個節點失敗，「更新執行」就會停止。<br /><br /> 有效值的範圍是 0 到叢集節點數減 1。|  
|**RequireAllNodesOnline**|None|指定所有節點都必須在線上且可搜尋，才能開始更新。|  
|**RebootTimeoutMinutes**|15|CAU 允許重新啟動節點 (如有需要重新啟動) 與啟動所有自動啟動服務的時間 (分鐘)。 如果重新啟動程序未在此時間內完成，該節點上 「 更新執行標示為失敗。|  
|**PreUpdateScript**|None|若要更新開始之前以及節點進入維護模式之前，每個節點上執行的 PowerShell 指令碼路徑和檔案名稱。 檔案名稱的副檔名必須是 **.ps1**，而且路徑加上檔案名稱的總長度不得超過 260 個字元。 最佳作法是讓指令碼位於叢集存放裝置的磁碟上，或在高可用性的網路檔案共用，以確保所有叢集節點永遠都能存取該指令碼。 如果指令碼位於網路檔案共用，請確定已設定檔案共用的 Everyone 群組讀取權限並禁止寫入存取，以防止未經授權的使用者竄改檔案。<br /><br /> 如果指定了更新前指令碼，請務必設定可讓指令碼順利執行的設定，像是時間限制 (例如 **StopAfter**)。 這些限制會套用到執行指令碼和安裝更新的整個處理程序中，而非只針對安裝更新的處理程序。|  
|**PostUpdateScript**|None|（節點離開維護模式之後），就會完成更新之後執行的 PowerShell 指令碼路徑和檔案名稱。 檔案名稱的副檔名必須是 **.ps1**而且路徑加上檔案名稱的總長度不得超過 260 個字元。 最佳作法是讓指令碼位於叢集存放裝置的磁碟上，或在高可用性的網路檔案共用，以確保所有叢集節點永遠都能存取該指令碼。 如果指令碼位於網路檔案共用，請確定已設定檔案共用的 Everyone 群組讀取權限並禁止寫入存取，以防止未經授權的使用者竄改檔案。<br /><br /> 如果指定了更新後指令碼，請務必設定可讓指令碼順利執行的設定，像是時間限制 (例如 **StopAfter**)。 這些限制會套用到執行指令碼和安裝更新的整個處理程序中，而非只針對安裝更新的處理程序。|  
|**ConfigurationName**|此設定只會在您執行指令碼時生效。<br /><br /> 如果您指定更新前指令碼或更新後指令碼，但您未指定**ConfigurationName**、 預設的工作階段會使用 PowerShell (Microsoft.PowerShell) 的設定。|指定定義工作階段指令碼的 PowerShell 工作階段設定 (藉由指定**PreUpdateScript**並**PostUpdateScript**) 會執行，而且會限制可以執行的命令。|  
|**CauPluginName**|**Microsoft.WindowsUpdatePlugin**|設定讓叢集感知更新用來預覽更新或執行「更新執行」的外掛程式。 如需詳細資訊，請參閱 <<c0> [ 如何叢集感知更新外掛程式運作](cluster-aware-updating-plug-ins.md)。|  
|**CauPluginArguments**|None|更新外掛程式使用的一組 *name=value* 組 (引數)，例如：<br /><br /> **Domain=Domain.local**<br /><br /> 對於您在 *CauPluginName* 中指定的外掛程式而言，這些 **name=value** 組必須是有意義的配對。<br /><br /> 若要使用 CAU UI 指定引數，請輸入 *name*，按下 Tab 鍵，然後輸入對應的 *value*。 再次按下 Tab 鍵即可提供下一個引數。 每個 *name* 及 *value* 都會自動以等號 (=) 分隔。 多個組會自動以分號分隔。<br /><br /> 預設值**Microsoft.WindowsUpdatePlugin**外掛程式不需要引數。 不過，您可以指定選用引數，例如指定標準 Windows Update Agent 查詢字串以篩選外掛程式套用的更新組。 針對*名稱*，使用**QueryString**，並針對*值*，以引號括住完整查詢。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 如何叢集感知更新外掛程式運作](cluster-aware-updating-plug-ins.md)。|  
  
##  <a name="BKMK_runtime"></a> 指定當您要求 「 更新執行選項  
 下表列出要求「更新執行」時可以指定的選項 (「更新執行設定檔」選項以外的選項)。 如需可在「更新執行設定檔」中設定之選項的相關資訊，請參閱上一個表格。  
  
|選項|預設值|詳細資料|  
|------------|-------------------|-------------|  
|**ClusterName**|None <br>**注意：** 只有在容錯移轉叢集節點沒有執行 CAU UI 時，或者您想參照執行 CAU UI 以外的其他容錯移轉叢集時，才必須設定這個選項。|要執行「更新執行」的叢集 NetBIOS 名稱。|  
|**認證**|目前的帳戶認證|將要執行「更新執行」的目標叢集的系統管理認證。 您可以從已經擁有所需的認證啟動 CAU UI （或開啟的 PowerShell 工作階段中，如果您使用 CAU 的 PowerShell cmdlet） 在叢集具有系統管理員權限和權限的帳戶。|  
|**NodeOrder**|根據預設，CAU 會從擁有最少叢集角色的節點開始，接著處理擁有第二少叢集角色的節點，依此類推。|依更新順序 (可能的話) 顯示的叢集節點名稱。|  
  
##  <a name="BKMK_profile"></a> 使用更新執行設定檔  
 每個「更新執行」都可與特定更新執行設定檔建立關聯。 更新執行設定檔會儲存在預設 *%windir%\cluster*資料夾。 如果您使用 CAU UI 中遠端更新模式中，您可以在您套用更新，時間指定 「 更新執行設定檔，或者您可以使用預設更新執行設定檔。 如果您在自行更新模式使用 CAU，您可以匯入的設定指定更新執行設定檔設定自行更新選項時。 在這兩種情況下，您可視需要覆寫「更新執行」選項顯示的值。 如有需要，您可以將「更新執行」選項儲存為更新執行設定檔，檔案名稱不一定要相同。 下一次套用更新或設定自行更新選項時，CAU 會自動選取之前選取的更新執行設定檔。  
  
 您可以修改現有更新執行設定檔，或建立一個新方法是選取**建立或修改更新執行設定檔**在 CAU UI 中。

以下是使用更新執行設定檔的一些重要事項：

* 「 更新執行設定檔不會儲存叢集特定資訊，例如系統管理認證。 如果您在自行更新模式使用 CAU，更新執行設定檔也不會儲存自行更新排程資訊。 這可以讓您在指定類別中的所有容錯移轉叢集間共用更新執行設定檔。
* 如果您設定自行更新選項，使用 「 更新執行設定檔，並稍後再修改設定檔使用不同的值，如 「 更新執行 」 選項，則自行更新設定不會自動變更。 若要套用新的更新執行設定，您必須再次設定自行更新選項。
* 執行設定檔編輯器不幸的是不支援檔案路徑包含空格，例如*C:\Program Files*。 因應措施，儲存您的前置和後更新指令碼中不包含空格，或使用 PowerShell 以獨佔方式來管理執行設定檔，執行時，將括住路徑的路徑**Invoke-caurun**。

### <a name="windows-powershell-equivalent-commands"></a>Windows PowerShell 對應的命令
  
 當您執行時，您可以會匯入設定從更新執行設定檔**Invoke-caurun**， **Add-cauclusterrole**，或**Set-cauclusterrole** cmdlet。  
  
 下列範例使用在 *C:\Windows\Cluster\DefaultParameters.xml* 指定的「更新執行」選項，在名為 *CONTOSO-FC1* 的叢集上執行掃描和完整的更新執行。 剩餘的 Cmdlet 參數使用預設值。  
  
```powershell  
$MyRunProfile = Import-Clixml C:\Windows\Cluster\DefaultParameters.xml  
Invoke-CauRun –ClusterName CONTOSO-FC1 @MyRunProfile   
```  
  
 使用更新執行設定檔，您可以重複更新容錯移轉叢集，並使用一致的例外狀況管理、時間界限與其他操作參數設定。 由於這些設定通常專用於某種容錯移轉叢集類別 (例如「所有 Microsoft SQL Server 叢集」或「我的業務關鍵叢集」)，您可以根據要使用的容錯移轉叢集類別來命名每個更新執行設定檔。 此外，您還可以在檔案共用管理更新執行設定檔，讓 IT 組織中特定類別的所有容錯移轉叢集都可存取。  
  
  
  
## <a name="see-also"></a>另請參閱

-   [叢集感知更新](cluster-aware-updating.md)
  
-   [在 Windows PowerShell 中的叢集感知更新 Cmdlet](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps)