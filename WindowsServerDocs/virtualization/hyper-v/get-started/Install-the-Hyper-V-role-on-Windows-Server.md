---
title: 在 Windows Server 上安裝 Hyper-v 角色
description: 提供使用伺服器管理員或 Windows PowerShell 安裝 Hyper-v 的指示
manager: dongill
ms.topic: get-started-article
ms.assetid: 8e871317-09d2-4314-a6ec-ced12b7aee89
author: kbdazure
ms.author: kathydav
ms.date: 12/02/2016
ms.openlocfilehash: 32632e7af3db0c3b390606bc784b929e76b2892f
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997599"
---
# <a name="install-the-hyper-v-role-on-windows-server"></a>在 Windows Server 上安裝 Hyper-v 角色

>適用於：Windows Server 2016、Windows Server 2019

若要建立和執行虛擬機器，請在 windows Server 上使用伺服器管理員或 Windows PowerShell 中的**install---** 的指令程式安裝 hyper-v 角色。
若為 Windows 10，請參閱[在 windows 10 上安裝 hyper-v](/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)。

若要深入瞭解 Hyper-v，請參閱[Hyper-v 技術總覽](../Hyper-V-Technology-Overview.md)。 若要試用 Windows Server 2019，您可以下載並安裝評估版。 請參閱[評估中心](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)。

在您安裝 Windows Server 或新增 Hyper-v 角色之前，請先確定：
- 您的電腦硬體相容。 如需詳細資訊，請參閱 Windows server 的[系統需求](../../../get-started/System-Requirements.md)和[windows Server 上的 hyper-v 的系統需求](../System-requirements-for-Hyper-V-on-Windows.md)。
- 您不打算使用依賴 Hyper-v 所需之相同處理器功能的協力廠商虛擬化應用程式。 範例包括 VMWare 工作站和 VirtualBox。 您可以安裝 Hyper-v，而不需要卸載這些其他應用程式。 但是，如果您在 Hyper-v 虛擬機器執行時嘗試使用它們來管理虛擬機器，則虛擬機器可能無法啟動，或可能會執行 unreliably。 如需關閉 Hyper-v 虛擬機器的詳細資料和指示（如果您需要使用其中一個應用程式），請參閱[虛擬化應用程式無法與 hyper-v、Device Guard 和 Credential guard 搭配](https://support.microsoft.com/help/3204980/virtualization-applications-do-not-work-together-with-hyper-v-device-g)使用。

如果您只想要安裝管理工具，例如 Hyper-v 管理員，請參閱[使用 Hyper-v 管理員從遠端系統管理 hyper-v 主機](../Manage/Remotely-manage-Hyper-V-hosts.md)。

## <a name="install-hyper-v-by-using-server-manager"></a>使用伺服器管理員安裝 Hyper-v

1. 在 [伺服器管理員]**** 的 [管理]**** 功能表上，按一下 [新增角色及功能]****。

2. 在 [在您開始前]**** 頁面上，確認已準備好目的地伺服器和網路環境，以便安裝您要的角色和功能。 按 [下一步]  。

3. 在 [選取安裝類型]**** 頁面上，選取 [角色型或功能型安裝]****，然後按 [下一步]****。

4. 在 [選取目的地伺服器]**** 頁面上，從伺服器集區選取伺服器，然後按 [下一步]****。

5. 在 [選取伺服器角色]**** 頁面上，選取 [Hyper-V]****。

6. 若要新增用來建立和管理虛擬機器的工具，請按一下 [新增功能]****。 在 [功能] 頁面上，按 [下一步]****。

7. 在 [建立虛擬交換器]**** 頁面、[虛擬機器移轉]**** 頁面和 [預設存放區]**** 頁面上，選取適當的選項。

8. 在 [確認安裝選項]**** 頁面上，選取 [需要時自動重新啟動目的伺服器]****，然後按一下 [安裝]****。

9. 安裝完成時，請確認已正確安裝 Hyper-v。 開啟伺服器管理員中的 [**所有伺服器**] 頁面，然後選取安裝 hyper-v 的伺服器。 檢查所選伺服器頁面上的 [**角色及功能**] 磚。

## <a name="install-hyper-v-by-using-the-install-windowsfeature-cmdlet"></a>使用 Install-Add-windowsfeature Cmdlet 安裝 Hyper-v

1. 在 Windows 桌面上，按一下 [開始] 按鈕，然後輸入 **Windows PowerShell** 名稱的任何一部分。

2. 以滑鼠右鍵按一下 [Windows PowerShell]，然後選取 [**以系統管理員身分執行**]。

3. 若要在您從遠端連線的伺服器上安裝 Hyper-v，請執行下列命令，並 `<computer_name>` 將取代為伺服器的名稱。

    ```powershell
    Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart
    ```

    如果您是在本機連線到伺服器，請執行命令，但不包含 `-ComputerName <computer_name>` 。

4. 在伺服器重新開機之後，您可以看到已安裝 Hyper-v 角色，並藉由執行下列命令來查看已安裝的其他角色和功能：

    ```powershell
    Get-WindowsFeature -ComputerName <computer_name>
    ```

    如果您是在本機連線到伺服器，請執行命令，但不包含 `-ComputerName <computer_name>` 。

> [!NOTE]
> 如果您在執行 Windows Server 2016 之 Server Core 安裝選項的伺服器上安裝此角色，並使用參數 `-IncludeManagementTools` ，則只會安裝適用于 Windows PowerShell 的 Hyper-v 模組。 您可以使用另一部電腦上的 [GUI 管理工具] [Hyper-v 管理員]，從遠端系統管理在 Server Core 安裝上執行的 Hyper-v 主機。 如需遠端連線的指示，請參閱[使用 Hyper-v 管理員從遠端系統管理 hyper-v 主機](../Manage/Remotely-manage-Hyper-V-hosts.md)。

## <a name="additional-references"></a>其他參考資料

- [Install-Add-windowsfeature](/powershell/module/Microsoft.Windows.ServerManager.Migration/Install-WindowsFeature)