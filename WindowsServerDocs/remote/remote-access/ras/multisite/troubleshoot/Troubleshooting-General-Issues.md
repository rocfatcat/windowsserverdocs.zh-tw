---
title: 疑難排解一般問題
description: 本主題是在 Windows Server 2016 的多網站部署中部署多部遠端存取服務器指南的一部分。
manager: brianlic
ms.topic: article
ms.assetid: 354ae5e3-bae1-44f9-afd7-7eaba70f2346
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 911d12088acc5071e18e7e24000364d9fe539250
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87958476"
---
# <a name="troubleshooting-general-issues"></a>疑難排解一般問題

>適用於：Windows Server (半年度管道)、Windows Server 2016

本主題包含與遠端存取相關之一般問題的疑難排解資訊。

## <a name="gpo-retrieval-error"></a>GPO 抓取錯誤
**收到錯誤**。 無法抓取 DirectAccess 伺服器 GPO 設定。 確定您有 GPO 的編輯許可權。

在收到此錯誤之後，[遠端存取管理] 主控台沒有回應。

**原因**

DirectAccess 無法存取部署中其中一個進入點的 GPO，因此無法載入設定。

**方案**

請確定部署中的每個進入點在其網域控制站上都有對應的 GPO，並確認登入的使用者具有遠端存取部署中設定之所有 Gpo 的讀取和寫入權限。

因應措施是使用 configuration Cmdlet，而不是使用遠端存取管理主控台;例如，使用 `Get-RemoteAccess` 和 `Get-DAEntryPoint` 。

> [!NOTE]
> 當目前進入點的伺服器 GPO 無法使用時，不會發生這種情況。

您可以使用指令 `Get-DAEntryPointDC` 程式來列出所有儲存伺服器 gpo 的網域控制站，並 `Get-DAMultiSite` 搭配使用 `Get-RemoteAccess` 來取得部署中伺服器 gpo 的完整清單。 例如：

```
$ServerGpos = Get-DAEntryPointDC | ForEach-Object {
   @{
       GpoName = (Get-RemoteAccess -EntryPoint $_.EntryPointName).ServerGpoName;
        DC = $_.DomainControllerName }
}
$ServerGpos | ForEach-Object { $GpoName = $_['GpoName'] ; $DC = $_['DC'] ; Write-Host "Server GPO '$GpoName' on DC '$DC'" }
```

## <a name="windows-7-to-windows-8-or-10-client-upgrade"></a>Windows 7 到 Windows 8 或10用戶端升級
**徵兆**。 當 Windows 7 用戶端在多網站部署中升級至 Windows 10 或 Windows 8 之後，DirectAccess 連線不會顯示在 [網路] 清單中。

**原因**

多網站部署中的 Windows 7 Gpo 並不包含 Windows 8 網路連線助理設定。

 Windows 7 用戶端應該使用 DirectAccess 連線助理來監視其 DirectAccess 線上狀態，這需要在 Windows 7 用戶端 Gpo 中進行個別的手動設定。 當 Windows 7 用戶端升級至 Windows 10 或 Windows 8 時，如果仍然套用 Windows 7 用戶端 GPO，網路連線助理將無法運作。

**方案**

如果在 Windows 7 Gpo 中設定 DirectAccess 連線助理設定，您可以在升級用戶端電腦之前先解決此問題，方法是使用下列 PowerShell Cmdlet 修改 Windows 7 Gpo：

```
Set-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant" -ValueName "TemporaryValue" -Type Dword -Value 1
Remove-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant"
```

如果用戶端已升級，或未設定 DCA，請將用戶端電腦移至 Windows 10 或 Windows 8 安全性群組。

## <a name="general-cmdlet-errors"></a>一般 Cmdlet 錯誤

-   **問題 1**

    **收到錯誤**。 <server_name 或 entry_point_name> 無法連線到網域控制站 <domain_controller>。

    **原因**

    為了保持多站台部署中的設定一致，確認每一個 GPO 都是由單一網域控制站所管理非常重要。 當管理進入點之伺服器 GPO 的網域控制站無法使用時，便無法讀取或修改遠端存取設定。

    **方案**

    遵循2.4 中所述的「變更管理伺服器 Gpo 的網域控制站」程式[。設定 Gpo](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs)。

-   **問題 2**

    **收到錯誤**。 無法連線到網域 <domain_name> 中的主域控制站。

    **原因**

    為了保持多站台部署中的設定一致，確認每一個 GPO 都是由單一網域控制站所管理非常重要。 用戶端 GPO 是在網域主控站上管理。 如果網域主控站無法使用，便無法讀取或修改遠端存取組態設定。

    **方案**

    遵循2.4 中所述的「傳送 PDC 模擬器角色」程式[。設定 Gpo](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs)。



