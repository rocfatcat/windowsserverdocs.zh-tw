---
title: 為 Hyper-V 虛擬機器建立虛擬交換器
description: 提供使用 Hyper-v 管理員或 Windows PowerShell 建立虛擬交換器的指示
manager: dongill
ms.topic: get-started-article
ms.assetid: fdc8063c-47ce-4448-b445-d7ff9894dc17
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: b9de14f9c3f66f6d8c8b532e8f4a83192b3e824b
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996631"
---
# <a name="create-a-virtual-switch-for-hyper-v-virtual-machines"></a>為 Hyper-V 虛擬機器建立虛擬交換器

>適用于： Windows 10、Windows Server 2016、Microsoft Hyper-v Server 2016、Windows Server 2019、Microsoft Hyper-v Server 2019

虛擬交換器可讓在 Hyper-v 主機上建立的虛擬機器與其他電腦通訊。 當您第一次在 Windows Server 上安裝 Hyper-v 角色時，可以建立虛擬交換器。 若要建立額外的虛擬交換器，請使用 Hyper-v 管理員或 Windows PowerShell。 若要深入瞭解虛擬交換器，請參閱[Hyper-v 虛擬交換器](../../hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)。

虛擬機器的網路功能可能是一個複雜的主題。 而且，您可能會想要使用數個新的虛擬交換器功能，像是[切換內嵌小組 (設定) ](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md#switch-embedded-teaming-set)。 但基本網路功能相當容易。 本主題只涵蓋足夠的內容，讓您可以在 Hyper-v 中建立網路虛擬機器。 若要深入瞭解如何設定您的網路基礎結構，請參閱[網路](../../../networking/index.yml)功能檔。

## <a name="create-a-virtual-switch-by-using-hyper-v-manager"></a>使用 Hyper-v 管理員建立虛擬交換器

1.  開啟 [Hyper-v 管理員]，選取 Hyper-v 主電腦名稱稱。

2.  選取 [**動作**] [  >  **虛擬交換器管理員**]。

    ![顯示功能表選項動作 > 虛擬交換器管理員的螢幕擷取畫面](../media/Hyper-V-Action-VSwitchManager.png)

3.  選擇您想要的虛擬交換器類型。

    |連線類型|描述|
    |-------------------|---------------|
    |外部|可讓虛擬機器存取實體網路，以與外部網路上的伺服器和用戶端進行通訊。 允許同一部 Hyper-v 伺服器上的虛擬機器彼此通訊。|
    |內部|允許在相同 Hyper-v 伺服器上的虛擬機器之間，以及虛擬機器與管理主機作業系統之間進行通訊。|
    |Private|只允許在相同 Hyper-v 伺服器上的虛擬機器之間進行通訊。 私人網路會與 Hyper-v 伺服器上的所有外部網路流量隔離。 當您必須建立隔離的網路環境（例如隔離的測試網域）時，這種類型的網路很有用。|

4.  選取 [**建立虛擬交換器**]。

5.  新增虛擬交換器的名稱。

6.  如果您選取 [外部]，請選擇您要使用的網路介面卡 (NIC) ，以及下表所述的任何其他選項。

    ![顯示外部網路選項的螢幕擷取畫面](../media/Hyper-V-NewVSwitch-ExternalOptions.png)

    |設定名稱|說明|
    |----------------|---------------|
    |允許管理作業系統共用此網路介面卡|如果您想要允許 Hyper-v 主機與虛擬機器共用虛擬交換器和 NIC 或 NIC 小組的使用，請選取此選項。 啟用此功能後，主機可以使用您為虛擬交換器設定的任何設定，例如服務品質 (QoS) 設定、安全性設定，或 Hyper-v 虛擬交換器的其他功能。|
    |啟用單一根目錄 I/O 虛擬化 (SR-IOV)|只有在您想要允許虛擬機器流量略過虛擬機器交換器，並直接移至實體 NIC 時，才選取此選項。 如需詳細資訊，請參閱海報隨附參考： Hyper-v 網路中的[單一根目錄 I/o 虛擬化](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn641211(v=ws.11)#Sec4)。|

7.  如果您想要隔離來自管理 Hyper-v 主機作業系統或其他共用相同虛擬交換器之虛擬機器的網路流量，請選取 [**啟用管理作業系統的虛擬 LAN 識別**]。 您可以將 VLAN ID 變更為任何數位，或保留預設值。 這是管理作業系統將用於所有透過此虛擬交換器進行網路通訊的虛擬 LAN 識別碼。

    ![顯示 VLAN ID 選項的螢幕擷取畫面](../media/Hyper-V-NewSwitch-VLAN.png)

8.  按一下 [確定]  。

9. 按一下 [是] 。

    ![顯示 [暫止的變更可能會中斷網路連線] 訊息的螢幕擷取畫面](../media/Hyper-V-NewVSwitch-DisruptNetwork.png)

## <a name="create-a-virtual-switch-by-using-windows-powershell"></a>使用 Windows PowerShell 建立虛擬交換器

1.  在 Windows 桌面上，按一下 [開始] 按鈕，然後輸入 **Windows PowerShell** 名稱的任何一部分。

2.  以滑鼠右鍵按一下 [Windows PowerShell]，然後選取 [**以系統管理員身分執行**]。

3.  藉由執行[get-netadapter](https://technet.microsoft.com/library/jj130867.aspx) Cmdlet 來尋找現有的網路介面卡。 記下您要用於虛擬交換器的網路介面卡名稱。

    ```
    Get-NetAdapter
    ```

4.  使用[新的-VMSwitch](/powershell/module/hyper-v/new-vmswitch?view=win10-ps) Cmdlet 建立虛擬交換器。 例如，若要使用 ethernet 網路介面卡建立名為 ExternalSwitch 的外部虛擬交換器，並開啟 [**允許管理作業系統共用此網路介面卡**]，請執行下列命令。

    ```
    New-VMSwitch -name ExternalSwitch  -NetAdapterName Ethernet -AllowManagementOS $true
    ```

    若要建立內部交換器，請執行下列命令。

    ```
    New-VMSwitch -name InternalSwitch -SwitchType Internal
    ```

    若要建立私用交換器，請執行下列命令。

    ```
    New-VMSwitch -name PrivateSwitch -SwitchType Private
    ```

如需更多有關 Windows Server 2016 中改良或新虛擬交換器功能的先進 Windows PowerShell 腳本，請參閱[遠端直接記憶體存取和交換器內嵌](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)小組。


## <a name="next-step"></a>後續步驟
[在 Hyper-V 中建立虛擬機器](Create-a-virtual-machine-in-Hyper-V.md)