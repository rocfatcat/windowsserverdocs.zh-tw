---
title: 安裝 Server Core
description: 如何取得並安裝 Windows Server 2019、 Windows Server 2016 或 Windows Server （半年通道） 上的 Server Core 安裝。
ms.prod: windows-server-threshold
ms.date: 05/21/2019
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d22818c-fbb7-487a-bb82-81ef0a3f7ede
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 6f685ce29088b56bb243d21315787ab90e6863a4
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65976724"
---
# <a name="install-server-core"></a>安裝 Server Core

> 適用於：Windows Server 2019，Windows Server 2016 中，Windows Server （半年通道）
  
當您第一次安裝 Windows Server 時，您會有下列安裝選項：

>[!NOTE]
> 在下列清單中，沒有「桌面體驗」的版本是 Server Core 安裝選項

-   Windows Server Standard
-   Windows Server Standard 含桌面體驗
-   Windows Server Datacenter
-   Windows Server Datacenter 含桌面體驗

當您安裝 Windows Server （半年通道） 時，您會有下列安裝選項：

-   Windows Server Standard 
-   Windows Server Datacenter

[Server Core] 選項可以減少所需的磁碟空間和潛在的攻擊面。因此，除非您對 [含有桌面體驗的伺服器] 選項所包含的額外使用者介面元素與圖形化管理工具有特定需求，否則建議您選擇 Server Core 安裝。 如果您確實認為需要額外的使用者介面元素，請參閱[安裝「含有桌面體驗的伺服器」](Getting-Started-with-Server-with-Desktop-Experience.md)。 

[Server Core] 選項不會安裝標準使用者介面 (桌面體驗)；您可以使用命令列、Windows PowerShell 或透過遠端方法來管理伺服器。

>[!NOTE]
>
>與 Windows Server 某些更早的版本不同，您無法在安裝完成後在 Server Core 與桌面體驗伺服器之間進行轉換。 如果您安裝 Server Core，並稍後決定使用桌面體驗伺服器，您應該執行全新安裝。

**使用者介面︰** 命令提示字元

**在本機安裝、設定、解除安裝伺服器角色：** 在命令提示字元使用 Windows PowerShell。

**安裝、 設定、 從遠端解除安裝伺服器角色，從 Windows 用戶端電腦 （或已安裝桌面體驗的伺服器）：** 利用伺服器管理員、 遠端伺服器管理工具 (RSAT)、 Windows PowerShell 或 Windows Admin Center.

>[!NOTE]
>
>對於 RSAT，您必須使用 Windows 10 版本。
>Microsoft Management Console 在本機無法使用。

**範例中可用的伺服器角色：**

- Active Directory 憑證服務
- Active Directory Domain Services
- DHCP 伺服器
- DNS 伺服器
- 檔案服務 (包括檔案伺服器資源管理員)
- Active Directory 輕量型目錄服務 (AD LDS)
- Hyper-V
- 列印和文件服務
- 串流處理媒體服務
- 網頁伺服器 (包括 ASP.NET 子集)
- Windows Server 更新伺服器
- Active Directory Rights Management Server
- 路由及遠端存取伺服器和下列子角色：
   - 遠端桌面服務連線代理人
   - 授權
   - 虛擬化
   - 大量啟用服務

針對不包含在 Server Core 角色，請參閱[角色、 角色服務和功能不在 Windows Server 的 Server Core](../administration/server-core/server-core-removed-roles.md)。

## <a name="installing-on-windows-server-2019-or-windows-server-2016"></a>在 Windows Server 2019 或 Windows Server 2016 安裝

如需一般的安裝步驟和選項適用於 Windows Server （長時間詞彙維護通道），請參閱[Windows Server 安裝與升級](installation-and-upgrade.md)。

## <a name="installing-on-windows-server-semi-annual-channel"></a>Windows Server （半年通道） 上安裝

安裝適用於 Windows Server （半年通道） 的步驟完全一樣安裝舊版的 Windows Server (從。ISO 映像），但有下列例外狀況：

- 不支援從先前的 Windows Server to Windows Server 版本 1709 升級。 永遠需要全新安裝。
   這表示，當您從 Windows 電腦的桌面上執行 setup.exe，安裝程式體驗不允許 [升級] 選項 （會變成灰色）。
- 沒有適用於 Windows Server （半年通道） 的評估版本
- 沒有 OEM 或零售版。 透過軟體保證或忠誠度方案時，即可只獲得 Windows Server （半年通道）。

如需 半年通道的詳細資訊，請參閱[比較的服務通道](../get-started-19/servicing-channels-19.md)。

若要查看新功能 Windows Server 半年通道，請參閱[What's New in Windows Server](whats-new-in-windows-server.md)