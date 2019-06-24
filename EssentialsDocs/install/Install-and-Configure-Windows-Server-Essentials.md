---
title: 安裝和設定 Windows Server Essentials
description: 描述如何使用 Windows Server Essentials
ms.custom: na
ms.date: 06/17/2013
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e95cf219-46a4-4041-bd81-0c4c2a0622cf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 48fa18d5baf7d4b48b14cbda5a513c487920d70a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433473"
---
# <a name="install-and-configure-windows-server-essentials"></a>安裝和設定 Windows Server Essentials

>適用於：Windows Server 2016 Essentials、 Windows Server 2012 R2 Essentials 中，Windows Server 2012 Essentials

##  <a name="BKMK_InstallConfigure"></a>   

 本文件提供安裝和設定 Windows Server Essentials 的逐步指示。 在開始安裝之前，檢閱並完成工作所述[之前您安裝 Windows Server Essentials](Before-You-Install-Windows-Server-Essentials.md)。  

 本文件提供安裝和設定 Windows Server Essentials 的逐步指示。 在開始安裝之前，檢閱並完成工作所述[之前您安裝 Windows Server Essentials](../install/Before-You-Install-Windows-Server-Essentials.md)。  
  
 您可以安裝並設定 Windows Server Essentials 中兩個步驟：  
  

1.  [步驟 1：安裝 Windows Server Essentials 作業系統](Install-and-Configure-Windows-Server-Essentials.md#BKMK_ManualInstallation)在此步驟中，您必須安裝作業系統在您的伺服器上。  
  
2.  [步驟 2：設定 Windows Server Essentials 作業系統](Install-and-Configure-Windows-Server-Essentials.md#BKMK_Step2Configure)在此步驟中，您必須完成安裝所提供的公司、 網域設定和網路系統管理員的相關資訊。 使用此資訊是為了取得供您使用的伺服器。  

1.  [步驟 1：安裝 Windows Server Essentials 作業系統](../install/Install-and-Configure-Windows-Server-Essentials.md#BKMK_ManualInstallation)在此步驟中，您必須安裝作業系統在您的伺服器上。  
  
2.  [步驟 2：設定 Windows Server Essentials 作業系統](../install/Install-and-Configure-Windows-Server-Essentials.md#BKMK_Step2Configure)在此步驟中，您必須完成安裝所提供的公司、 網域設定和網路系統管理員的相關資訊。 使用此資訊是為了取得供您使用的伺服器。  

  
###  <a name="BKMK_ManualInstallation"></a> 步驟 1:安裝 Windows Server Essentials 作業系統  
  
> [!IMPORTANT]
>  在安裝作業系統之後，不要自訂您的伺服器在結束之前[步驟 2:設定 Windows Server Essentials 作業系統](#BKMK_Step2Configure)。  
  
 **估計的完成時間：** 大約 30 分鐘。  
  
> [!NOTE]
>  此程序的估計完成時間是根據最低硬體需求計算。  
  
##### <a name="to-install-the-operating-system"></a>安裝作業系統  
  
1. 將您的電腦以網路線連線至網路。  
  
   > [!IMPORTANT]
   >  安裝期間請勿將您的電腦與網路的連線中斷。 如此可能會造成安裝失敗。  
  
2. 開啟您的電腦，並再將 Windows Server Essentials DVD 插入 DVD 光碟機。  
  
    如果您要執行自動安裝，請連接含有您的回應檔案之卸除式媒體 (如磁碟片或者 USB 快閃磁碟機)。 視您的回應檔案內容而定，您可能會看見以下某些 (或者任何) 安裝畫面：  
  
3. 重新啟動您的電腦。 顯示 **按任何鍵從 CD 或 DVD 開機** 訊息時，請按任何鍵。  
  
   > [!NOTE]
   >  如果您的電腦並未從 DVD 啟動，請確認 CD-ROM 光碟機在 BIOS 的開機順序中排在第一位。 如需更多有關 BIOS 開機順序的資訊，請參閱電腦製造商的文件。  
  
4. 選取您要安裝的 **語言** 、 **時間及貨幣格式**，以及 **鍵盤或輸入法**，然後按一下 **下一步**。  
  
5. 按一下 **立即安裝**。  
  
6. 在 **輸入產品金鑰**鍵入產品金鑰。  
  
7. 請詳細閱讀 **授權條款**。 如果您接受，請選取 **我同意授權條款** 和取方塊，然後按一下 **下一步**。  
  
   > [!NOTE]
   >  如果您不選擇同意授權條款，則安裝不會繼續。  
  
8. 在 **哪一種安裝？** ，按一下**自訂：只安裝 Windows （進階）**  
  
9. 在 **您要在哪裏安裝 Windows?** 中，選取您要安裝 Windows 作業系統的硬碟機。 請確認您所有的內部硬碟機皆可用於安裝。  
  
    > [!IMPORTANT]
    >   必須安裝 Windows Server Essentials 為 c： 磁碟區，並將磁碟區大小必須至少為 60 GB。 建議您在作業系統磁碟上建立兩個磁碟分割，並且不要使用 C: (系統磁碟分割) 來儲存任何商業資料。  
  
    > [!NOTE]
    >  如果有硬碟機未列出 (例如，串流進階配接器 (SATA) 硬碟)，您必須從該硬碟載入載入裝置驅動程式。 請從製造商取得裝置驅動程式並將其儲存在卸除式媒體 (例如磁碟片或者 USB 快閃磁碟機) 將卸除式媒體連接至電腦，按一下 **載入驅動程式**。  
  
     如果您需要刪除和/或建立分割區，請請參照以下步驟：  
  
    1.  若要刪除分割區，請選取分割區，按一下 **磁碟機選項 (進階)** ，然後按一下 **刪除**。 在您刪除系統分割區之後，請使用步驟 **b** 或者步驟 **c** 中的說明建立新的分割區。  
  
        > [!NOTE]
        >  在您按下 **磁碟機選項 (進階)** 之後，該選項就不會再出現。 在此情形下，請略過與磁碟機選項有關的步驟。  
  
    2.  若要在尚未分割的空間建立分割區，按一下您要分割的硬碟，按下 **磁碟機選項 (進階)** ，按下 **新增**然後在 **大小** 文字方塊中，鍵入您想要建立的分割區大小。 例如，如果您使用建立的分割區大小 120 gigabytes (GB)，請鍵入 **122880**，然後按一下 **套用**。 建立分割區之後，按一下 **下一步**。 分割區在繼續安裝之前已經格式化。  
  
    3.  若要用所有尚未分割的空間建立分割區，按一下您要分割的硬碟，按下 **磁碟機選項 (進階)** ，按下 **新增**，然後按下 **套用** 即可接受預設分割區大小。 建立分割區之後，按一下 **下一步**。 分割區在繼續安裝之前已經格式化。  
  
        > [!IMPORTANT]
        >  在您完成此步驟後就不能將作業系統移動到不同的分割區。  
  
   在安裝期間，暫存檔將會複製到電腦上的安裝資料夾，大約花費 30 分鐘的時間。 Windows Server Essentials 作業系統安裝之後，您的電腦會重新啟動。 現在，您已準備好設定 Windows Server Essentials 的作業系統。  
  
###  <a name="BKMK_Step2Configure"></a> 步驟 2:設定 Windows Server Essentials 作業系統  
  
> [!IMPORTANT]
>  如果您從舊版的 Windows Small Business Server 移轉到 Windows Server Essentials，您必須遵循不同的處理序。 如需有關移轉安裝的詳細資訊，請參閱：  
> 
> - [從 Windows SBS 2003 移轉](../migrate/Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
>   -   [從 Windows SBS 2008 移轉](../migrate/Migrate-Windows-Small-Business-Server-2008-to-Windows-Server-Essentials.md)  
  
 在此階段的安裝期間，系統會提示您回答幾個有關您的組織的問題。 這是用於設定作業系統的資訊。  
  
> [!IMPORTANT]
>  開始此步驟之前，請確認區域網路介面卡連線至已開啟的路由器或交換器並且正常作用。  
  
 **估計的完成時間：** 大約 30 分鐘  
  
##### <a name="to-configure-the-operating-system"></a>設定作業系統  
  
1.  在 **確認日期和時間設定** 頁面, 按一下 **變更系統日期和時間設定** 以選擇伺服器的日期、時間以及時區設定。 在您完成時，請按一下 **下一步**。  
  
    > [!IMPORTANT]
    >  如果您要在虛擬機器上安裝 Windows Server Essentials，請確定您選擇與所要使用的主機作業系統的時區設定相同。 如果時區設定不同，可能會無法成功安裝伺服器。  
  
2.  在 **選擇伺服器安裝模式** 頁面，請執行以下動作之一：  
  
    1.  選擇**全新安裝**設為 Windows Server Essentials 伺服器軟體的完整全新安裝。  
  
    2.  選擇**伺服器移轉**安裝 Windows Server Essentials，並將此伺服器加入現有的 Windows 網域。  
  
3.  在 **個人化您的伺服器** 頁面，請輸入您的組織名稱，內部網域名稱以及伺服器名稱。  
  
    > [!IMPORTANT]
    >  伺服器名稱必須是在您的網路中未被使用的名稱。 在您完成此步驟後就無法變更伺服器名稱或者內部網域名稱。  
  
4.  按一下 [下一步]  。  
  
5.  在 **提供您的系統管理員帳戶資訊** 頁面，鍵入新系統管理員帳戶的資訊。  
  
    > [!CAUTION]
    >  未命名的系統管理員或網路系統管理員的網路系統管理員帳戶。 這些帳戶名稱要保留給系統使用。  
  
6.  在 **提供您的標準使用者帳戶資訊** 頁面，鍵入新的標準使用者帳戶資訊，然後按一下 **下一步**。  
  
7.  在 **讓伺服器自動保持最新** 頁面，選取您想要如何接收伺服器的 Windows Updates，然後按一下 **下一步**。  
  
8.  **正在更新及準備您的伺服器** 頁面顯示最後安裝程序的進度。 這需要花費一些時間完成，您的電腦將會重新啟動數次。  
  
9. 在伺服器最後一次重新啟動後會出現 **您的伺服器已可以使用** 頁面。 按一下 **關閉**。  
  
10. Click the Dashboard tile on the按一下 **開始** 畫面的儀表板圖標，然後在儀表板上，完成 **首頁** 頁面上的 **設定我的伺服器** 工作。 您應該在您的 Windows Server Essentials 安裝完成之後立即完成這些工作。  
  
> [!NOTE]
>  在安裝完成後，您就會以安裝期間新增的新系統管理員帳戶自動登入伺服器。 內建 Administrator 帳戶的密碼會設為與新系統管理員帳戶相同的密碼，然後內建 Administrator 帳戶就會停用。  
  
 您可以使用有限的一段時間 （稱為 「 評估期間 」） 的新安裝的伺服器，而不需要輸入產品金鑰。 試用期過後，您就必須輸入產品金鑰以啟動伺服器或延長試用期。 您最多可以延長試用期兩次。 當您屆滿試用期所允許的最大天數時，您就必須輸入產品金鑰以啟動伺服器。  
  
### <a name="customize-windows-server-essentials"></a>自訂 Windows Server Essentials  
 **首頁**Windows Server Essentials 儀表板頁面會連結到**安裝**您後應該要完成的工作會安裝您的伺服器。 您可以執行這些工作，來協助保護儲存在伺服器的資訊，並啟用可在 Windows Server Essentials 中的功能。  
  
 如果您選擇不執行這些工作，使用者可能無法存取某些網路功能。 若要稍後再回來進行這些工作，傳回到 Windows Server Essentials 儀表板**首頁**頁面。  
  
 以下表格為會出現在設定工作清單中的項目。  
  
|工作|描述
|----------|-----------------|  
|取得其他 Microsoft 產品的更新|按一下此工作，以存取執行一項工具，可讓您指定是否要使用 Microsoft Update 自動取得更新，Windows Server Essentials 與 Office 等其他 Microsoft 產品的連結。  
|新增使用者帳戶|按一下此工作以檢視有關新增使用者帳戶的簡短資訊。 提供用來執行 **[新增使用者帳戶精靈]** 的連結。 如需詳細資訊，請參閱 [Add a user account](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1)。  
|新增伺服器帳戶|按一下此工作以檢視有關新增伺服器資料夾的簡短資訊。 提供用來執行 **[新增資料夾精靈]** 的連結。 此外也提供有關「伺服器資料夾」的線上說明主題。 如需詳細資訊，請參閱[新增或移動伺服器資料夾](../manage/Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5)。 
|設定伺服器備份|按一下此工作以檢視有關使用伺服器資料夾保護資料的簡短資訊。 提供用來執行 **[設定伺服器備份精靈]** 的連結。 如需詳細資訊，請參閱[設定或自訂伺服器備份](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_1)。 
|設定隨處存取|按一下此工作以在 Windows Server Essentials 中檢視有關 「 隨處存取 」 功能的簡短資訊。 提供前往 **[隨處存取設定]** 頁面的連結。 如需詳細資訊，請參閱 < [Manage Anywhere Access](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)。 
|設定電子郵件警示通知|按一下此工作以檢視有關電子郵件警示通知的簡短資訊。 提供用來執行 **[設定警示的電子郵件通知]** 工具的連結。 如需詳細資訊，請參閱 [Set up email notifications for alerts](../manage/Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Email)。  
|設定媒體伺服器|按一下此工作以檢視有關使用媒體伺服器分享音樂、影片與影像檔案的簡短資訊。 提供前往 [媒體設定]   頁面的連結。 也提供前往關於媒體伺服器詳細資訊的線上說明主題連結。 如需詳細資訊，請參閱 < [Manage Digital Media](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)。 
|連線電腦|按一下此工作以檢視有關將網路電腦連線到伺服器的簡短資訊。 如需詳細資訊，請參閱[將電腦連線到伺服器](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)。
  
## <a name="see-also"></a>另請參閱  
  
-   [安裝 Windows Server Essentials](Install-Windows-Server-Essentials.md)
