---
title: 從 Windows Server (版本 1709) 開始移除或計劃取代的功能
description: 已移除或已計劃在發行版本中移除的特性與功能。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 06/05/2018
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 37970f3bee2070cffc77bff855a8f28641196b24
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452865"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1709"></a>從 Windows Server 版本 1709 開始移除或計劃取代的功能

>適用於：Windows Server 版本 1709

以下清單列出的 Windows Server 版本 1709 特性與功能已從該版本的產品中移除，或開始考慮可能在後續版本中取代。 適用對象是在商業環境中更新作業系統的 IT 專業人員。 **這份清單會在後續版本中有所變更，並可能不會包含每個受影響的功能。** 

## <a name="features-removed-from-windows-server-version-1709"></a>Windows Server 版本 1709 已移除的功能
Windows Server 版本 1709 包含 Windows Server 2016 中提供的相同功能。 不過，這個版本提供不同於 Windows Server 2016 的安裝選項：

- 做為半年度管道發行版本，Windows Server 版本 1709 僅提供 Server Core 安裝選項。 如需詳細資訊，請參閱 <<c0> [ 比較的服務通道](../get-started-19/servicing-channels-19.md)。
- 從這個版本開始，Nano Server 無法用來做為可安裝的主機作業系統。 Nano Server 改以容器作業系統形式來提供。 請參閱[Nano Server 在 Windows Server 版本 1709 中的變更](nano-in-semi-annual-channel.md)。
- 從這個版本開始，伺服器訊息區塊 (SMB) 第 1 版不會再預設會安裝。 如需詳細資訊，請參閱 < [SMBv1 不會安裝在 Windows 10 Fall Creators Update 和 Windows Server，版本 1709年和更新版本的預設](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows)。


## <a name="features-being-considered-for-replacement-starting-with-subsequent-releases"></a>考慮要從後續版本開始取代的功能

正在考慮要從 Windows Server 版本 1709 之後的發行開始取代下列特色及功能。 最後可能都會從已安裝的產品映像完全移除，並由取代其他特色或功能取代 (或是可從其他來源安裝)，這些功能有時會有特定功能遭移除，但在此版本中仍然可用。 您現在就應該開始針對所有依存於這些功能的應用程式、程式碼或使用方式，規劃替代方法或日後取代。

如果您有建議取代任何這些功能的意見反應要分享，可以使用[意見反應中樞 App](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)。 即使此 App 執行於 Windows 10，您同樣可以用來傳送有關 Windows Server 產品 (和文件) 的意見反應給我們。

### <a name="iis-6-management-compatibility"></a>IIS 6 管理相容性
考慮要取代的特定功能︰

- IIS 6 Metabase 相容性 (Web-Metabase)
- IIS 6 管理主控台 (Web-Lgcy-Mgmt-Console)
- IIS 6 指令碼工具 (Web-Lgcy-Scripting)
- IIS 6 WMI 相容性 (Web-WMI)

不考慮 IIS 6 Metabase 相容性 (當做 IIS 6 Metabase 指令碼與 IIS 7 或更新版本所用檔案型設定之間的模擬層)，而是應該使用 Microsoft.Web.Administration 命名空間等工具，開始將管理指令碼直接移轉至目標 IIS 檔案型設定。

您也應該開始從 IIS 6.0 或較舊版本進行移轉，並移到永遠會在最新發行的 Windows Server 版本中提供的最新版 IIS。


### <a name="iis-digest-authentication"></a>IIS 摘要式驗證
此驗證方法已計劃要進行取代。 您應該開始改用其他驗證方法，例如用戶端憑證對應 (請參閱[設定一對一用戶端憑證對應](https://docs.microsoft.com/iis/manage/configuring-security/configuring-one-to-one-client-certificate-mappings)) 或 Windows 驗證 (請參閱[應用程式設定](https://docs.microsoft.com/iis-administration/configuration/appsettings.json))。

### <a name="internet-storage-name-service-isns"></a>網際網路儲存名稱服務 (iSNS)
iSNS 即將列入取代考量中。 伺服器訊息區 (SMB) 功能提供基本上相同的功能，而且還有額外的功能。 如需這項功能的背景資訊，請參閱[伺服器訊息區概觀](https://technet.microsoft.com/library/hh831795(v=ws.11).aspx)。

### <a name="rsaaes-encryption-for-iis"></a>IIS 的 RSA/AES 加密 
此加密方法會取代正在考慮，因為優異的密碼編譯 API:已使用 next Generation (CNG) 方法。 若要深入了解 CNG 加密，請參閱[關於 CNG](https://msdn.microsoft.com/library/windows/desktop/aa375276(v=vs.85).aspx)。

### <a name="windows-powershell-20"></a>Windows PowerShell 2.0
這個早期 Windows PowerShell 版本已被數個較新的版本取代。 為獲得最佳功能及效能，請移轉至 Windows PowerShell 5.0 或更新版本。 如需詳細資訊，請參閱 [PowerShell 文件](https://docs.microsoft.com/powershell/index?view=powershell-5.1)。
