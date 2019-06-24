---
ms.assetid: c91c7196-ee0d-4856-8cfb-4c38494ccf1f
title: 工作資料夾概觀
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 06/07/2019
description: 工作資料夾概觀 - 這是 Windows Server 中的一種伺服器角色，可提供使用者一致的方式來存取電腦和裝置中的工作檔案。
ms.openlocfilehash: 1313c49982cb85b5cce1e9a442ff0c622c6be272
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812571"
---
# <a name="work-folders-overview"></a>工作資料夾概觀

>適用於：Windows Server （半年通道）、 Windows Server 2019、 Windows Server 2016、 Windows Server 2012 R2、 Windows 10，Windows 8.1，Windows 7

此主題所討論的是工作資料夾，這是一種執行 Windows Server 的檔案伺服器角色服務，它可讓使用者更為一致地存取電腦和裝置中的工作檔案。  
  
如果您想要下載或使用 Windows 10，Windows 7 或 Android 或 iOS 裝置上的工作資料夾，請參閱下列各項：

- [適用於 Windows 10 的工作資料夾](https://support.microsoft.com/help/12370/windows-10-work-folders)
- [工作資料夾適用於 Windows 7 （64 位元下載）](https://www.microsoft.com/download/details.aspx?id=42558)
- [工作資料夾適用於 Windows 7 （32 位元下載）](https://www.microsoft.com/download/details.aspx?id=42559)
- [適用於 iOS 的工作資料夾](https://itunes.apple.com/app/work-folders/id950878067)
- [適用於 Android 的工作資料夾](https://play.google.com/store/apps/details?id=com.microsoft.workfolders)

## <a name="role-description"></a>角色說明

 利用工作資料夾，除了公司電腦，使用者可以在個人電腦和裝置 (通常稱為「帶您自己的裝置 (BYOD)」) 上儲存和存取工作檔案。 使用者獲得方便儲存工作檔案的位置，而他們能夠從任何地方存取這類檔案。 組織將檔案儲存在集中管理的檔案伺服器上，並選擇性地指定使用者裝置原則 (例如加密和鎖定畫面密碼)，藉此維持對公司資料的控制權。  
  
 工作資料夾可利用資料夾重新導向、離線檔案和主資料夾的現有部署進行部署。 工作資料夾會將使用者檔案儲存在伺服器上稱為 *sync share* 的資料夾中。 您可以指定已包含使用者資料的資料夾，使您可以採用工作資料夾而不需要移轉伺服器和資料，或立即分階段廢除現有的解決方案。  
  
## <a name="practical-applications"></a>實際應用

 系統管理員可使用工作資料夾提供使用者其工作檔案的存取權，同時保持集中式的存放裝置以及對於組織資料的控制。 工作資料夾的一些特定應用包括︰  
  
-   提供單一存取點，讓使用者可從其工作及個人電腦和裝置存取工作檔案  
  
-   在離線時存取工作檔案，然後在電腦或裝置可連線網際網路或內部網路時與中央檔案伺服器進行同步  
  
-   利用資料夾重新導向、離線檔案和主資料夾的現有部署進行部署  
  
-   使用現有的檔案伺服器管理技術 (例如檔案分類和資料夾配額) 來管理使用者資料  
  
-   指定安全性原則，以指示使用者的電腦和裝置加密工作資料夾，並使用鎖定畫面密碼  
  
-   使用容錯移轉叢集搭配工作資料夾以提供高可用性的解決方案  
  
## <a name="important-functionality"></a>重要功能

 工作資料夾包含下列功能。  
  
| 功能 | 可用性 | 描述 |  
| ------------------- | ------------------ | ----------------- |  
| 伺服器管理員中的工作資料夾角色服務 | Windows Server 2019、 Windows Server 2016 或 Windows Server 2012 R2 | 檔案和存放服務可提供設定同步共用 (儲存使用者工作檔案的資料夾)、監視工作資料夾和管理同步共用與使用者存取的方法 |
| 工作資料夾 Cmdlet | Windows Server 2019、 Windows Server 2016 或 Windows Server 2012 R2 | Windows PowerShell 模組包含可用來管理工作資料夾伺服器的完整 Cmdlet |  
| 工作資料夾與 Windows 的整合 | Windows 10<br /><br /> Windows 8.1<br /><br /> Windows RT 8.1<br /><br /> Windows 7（需要下載） | 工作資料夾可在 Windows 電腦中提供下列功能：<br /><br /> -   可設定及監視工作資料夾的控制台項目<br />-   可輕鬆存取工作資料夾檔案的檔案總管整合<br />-   同步引擎可將檔案傳入及傳出中央檔案伺服器，同時將電池壽命和系統效能最大化 |
| 適用於裝置的工作資料夾 App | Android<br /><br /> Apple iPhone 和 iPad® | 可讓常見的裝置存取工作資料夾檔案的 App |  
  
## <a name="new-and-changed-functionality"></a>新功能和變更的功能
  
下表描述工作資料夾的一些重大變更。  
  
| 特色/功能 | 新功能或更新功能？ | 描述 |
| ---------------------------- | --------------------- | ----------------- |
| Azure AD 應用程式 Proxy 支援 | 已新增至 Windows 10 版本 1703、Android、iOS | 遠端使用者可以使用 Azure AD 應用程式 Proxy，安全地存取他們在工作資料夾伺服器上的檔案。 |
| 更快速地變更複寫 | Windows 10 和 Windows Server 2016 中的更新 | 在 Windows Server 2012 R2 中，將檔案變更同步處理到工作資料夾伺服器時，用戶端不會收到變更的通知，而且最多等待 10 分鐘就會收到更新。 當使用 Windows Server 2016 時，工作資料夾伺服器就會立即通知 Windows 10 用戶端和立即同步處理檔案變更。 這是 Windows Server 2016 的新功能，且需要 Windows 10 用戶端。 如果您使用的是舊版用戶端，或工作資料夾伺服器是 Windows Server 2012 R2，則用戶端會每隔 10 分鐘繼續輪詢變更。 |  
| 已和 Windows 資訊保護 (WIP) 整合 | 已新增至 Windows 10 版本 1607 | 如果系統管理員已部署 WIP，工作資料夾可在電腦上加密資料以強制執行資料保護。 此加密方式使用與企業 ID 相關聯的金鑰，可使用如 Microsoft Intune 等支援的行動裝置管理套件以遠端方式加以清除。 |  
| Microsoft Office 整合 | 已新增至 Windows 10 版本 1511 | 在 Windows 8.1 中，您可以按一下或點選此電腦，並瀏覽到電腦上的工作資料夾位置以瀏覽 Office App 中的工作資料夾。 在 Windows 10 中，瀏覽工作資料夾會變得更為容易，因為您可以將其新增至 Office 在儲存或開啟檔案時顯示的位置清單中。 如需詳細資訊，請參閱 [Windows 10 中的工作資料夾](https://windows.microsoft.com/windows-10/work-folders-in-windows-10) 和  [使用工作資料夾作為 Microsoft Office 中的位置進行疑難排解](https://social.technet.microsoft.com/wiki/contents/articles/32881.troubleshooting-using-work-folders-as-a-place-in-microsoft-office.aspx)。 |  
  
## <a name="software-requirements"></a>軟體需求

工作資料夾對檔案伺服器和網路基礎結構具有下列軟體需求：  
  
-   執行 Windows Server 2019 的伺服器，Windows Server 2016 或 Windows Server 2012 R2 裝載同步共用包含使用者檔案  
  
-   以 NTFS 檔案系統格式化的磁碟區，用來存放使用者檔案  
  
-   若要在 Windows 7 電腦上強制執行密碼原則，您必須使用群組原則密碼原則。 您也必須將 Windows 7 電腦從「工作資料夾」密碼原則排除 (若有使用的話)。

-   每個裝載工作資料夾之檔案伺服器的伺服器憑證。 這些憑證必須來自使用者信任的憑證授權單位 (CA)，最好是公開憑證授權單位。

-   （選擇性）若要使用多個檔案伺服器時支援自動電腦和裝置參照到正確的檔案伺服器的 Windows Server 2012 R2 中的結構描述延伸模組與 Active Directory 網域服務樹系。  
  
若要讓使用者透過網際網路同步，還有下列其他需求：  
  
-   能夠從網際網路存取伺服器，方法是在組織的反向 Proxy 或網路閘道中建立發佈規則  
  
-   (選用) 公開登錄的網址名稱以及能夠建立網域的其他公用 DNS 記錄  
  
-   (選用) 使用 Active Directory 同盟服務 (AD FS) 驗證時的 AD FS 基礎結構  
  
工作資料夾對用戶端電腦具有下列軟體需求：  
  
-   電腦和伺服器必須執行下列其中一種作業系統：  
  
    -   Windows 10  
  
    -   Windows 8.1  
  
    -   Windows RT 8.1  
  
    -   Windows 7  
  
    -   Android 4.4 KitKat 和更新版本  
  
    -   iOS 10.2 和更新版本  
  
-   Windows 7 電腦必須執行下列其中一個 Windows 版本：  
  
    -   Windows 7 專業版  
  
    -   Windows 7 旗艦版  
  
    -   Windows 7 企業版  
  
-   Windows 7 電腦必須加入您組織的網域 (它們無法加入工作群組)。  
  
-   本機 NTFS 格式的磁碟機上具有足夠可用空間，可用來在工作資料夾中存放所有使用者的檔案，如果工作資料夾位於系統磁碟機，還需要額外 6 GB 的可用空間，如預設的指定。 工作資料夾預設會使用下列位置︰ **%USERPROFILE%\Work Folders**  
  
     不過，使用者在設定期間可以變更位置 (支援的位置包括 microSD 記憶卡和使用 NTFS 檔案系統格式化的 USB 磁碟機，如果磁碟機被移除，則會停止同步)。  
  
     個別檔案的預設大小上限為 10 GB。 每個使用者的儲存空間沒有限制，但是系統管理員可以使用檔案伺服器資源管理員的配額功能來實作配額。  
  
-   工作資料夾不支援復原用戶端虛擬機器的虛擬機器狀態。 請改為使用系統映像備份或其他備份應用程式，從用戶端虛擬機器內部執行備份和還原作業。  
  
## <a name="work-folders-compared-to-other-sync-technologies"></a>工作資料夾與其他同步技術進行比較  

下表討論各種 Microsoft 同步技術如何定位以及何時使用。  
  
| | 工作資料夾 | 離線檔案 | 商務用 OneDrive | OneDrive |
| - | ------------------ | ------------------- | -------------------------- | -------------- |
| **技術摘要** | 同步處理儲存在檔案伺服器與電腦和裝置上的檔案 | 同步處理儲存在可存取企業網路的檔案伺服器與電腦上的檔案 (可由工作資料夾取代) | 同步處理儲存在 Office 365 或 SharePoint 與電腦和裝置 (位於企業網路內部或外部) 中的檔案，並提供文件共同作業功能 | 同步處理儲存在 OneDrive 與 PC、Mac 電腦和裝置上的個人檔案 |
| **目的是為了讓使用者存取工作檔案** | 是 | 是 | 是 | 否 |
| **雲端服務** | None | None | Office 365 | Microsoft OneDrive |
| **內部網路伺服器** | 執行 Windows Server 2012 R2 或 Windows Server 2016 的檔案伺服器 | 檔案伺服器 | SharePoint 伺服器 (選擇性) | None |
| **支援的用戶端** | PC、iOS、Android | 位於企業網路內，或透過 DirectAccess、VPN 或其他遠端存取技術連接的電腦 | PC、iOS、Android、Windows Phone | PC、Mac 電腦、Windows Phone、iOS、Android |
  
> [!NOTE]
>  除了列於上表中的同步技術以外，Microsoft 還提供其他的複寫技術，包括針對伺服器對伺服器複寫所設計的 DFS 複寫，以及設計為分公司 WAN 加速技術的 BranchCache。 如需詳細資訊，請參閱 [DFS 命名空間和 DFS 複寫](https://technet.microsoft.com/library/jj127250(v=ws.11).aspx) 和 [BranchCache 概觀](https://technet.microsoft.com/library/hh831696(v=ws.11).aspx) 
  
## <a name="server-manager-information"></a>伺服器管理員資訊  

工作資料夾為檔案和存放服務角色的一部分。 您可以使用 \[新增角色及功能精靈\] 或 `Install-WindowsFeature` Cmdlet 來安裝工作資料夾。 這兩種方法都可執行下列動作︰  
  
-   將 **\[工作資料夾\]** 頁面新增至伺服器管理員中的 **\[檔案和存放服務\]**  
  
-   安裝 Windows 同步共用服務，可供 Windows Server 主控同步共用  
  
-   安裝 SyncShare Windows PowerShell 模組以管理伺服器上的工作資料夾  
  
## <a name="interoperability-with-windows-azure-virtual-machines"></a>與 Windows Azure 虛擬機器的互通性

 您可以在 Windows Azure 的虛擬機器上執行此 Windows Server 角色服務。 此案例已透過 Windows Server 2012 R2 和 Windows Server 2016 進行測試。  
  
若要深入瞭解如何開始使用 Windows Azure 虛擬機器，請造訪 [Windows Azure 網站](http://www.windowsazure.com/documentation/services/virtual-machines)。  
  
## <a name="see-also"></a>另請參閱

 如需其他相關資訊，請參閱下列資源。  
  
| 內容類型 | 參考 |
| ------------------ | ---------------- |
| **產品評估** | -   [適用於 Android – 工作資料夾已釋放](https://blogs.technet.microsoft.com/filecab/2016/03/16/work-folders-for-android-released)（部落格文章）<br />-   [IOS-iPad 應用程式發行的工作資料夾](https://blogs.technet.com/b/filecab/archive/2015/01/16/work-folders-for-ios-ipad-app-release.aspx)（部落格文章）<br />-   [簡介 Windows Server 2012 R2 上的工作資料夾](http://blogs.technet.com/b/filecab/archive/2013/07/09/introducing-work-folders-on-windows-server-2012-r2.aspx)（部落格文章）<br />-   [工作資料夾簡介](http://channel9.msdn.com/posts/Introduction-to-Work-Folders)（Channel 9 影片）<br />-   [工作資料夾測試實驗室部署](http://blogs.technet.com/b/filecab/archive/2013/07/10/work-folders-test-lab-deployment.aspx)（部落格文章）<br />-   [工作資料夾適用於 Windows 7](http://blogs.technet.com/b/filecab/archive/2014/04/24/work-folders-for-windows-7.aspx) （部落格文章） |
| **部署** | -   [設計工作資料夾實作](plan-work-folders.md)<br />-   [部署工作資料夾](deploy-work-folders.md)<br />-   [搭配 AD FS 與 Web 應用程式 Proxy (WAP) 部署工作資料夾](deploy-work-folders-adfs-overview.md)<br />-   [使用 Azure AD 應用程式 Proxy 的部署工作資料夾](https://blogs.technet.microsoft.com/filecab/2017/05/31/enable-remote-access-to-work-folders-using-azure-active-directory-application-proxy/)<br />- [離線檔案 (CSC) 工作資料夾移轉指南](https://blogs.technet.microsoft.com/filecab/2016/08/12/offline-files-csc-to-work-folders-migration-guide/)<br />-   [工作資料夾部署的效能考量](https://blogs.technet.com/b/filecab/archive/2013/11/01/performance-considerations-for-large-scale-work-folders-deployments.aspx)<br />-   [工作資料夾適用於 Windows 7 （64 位元下載）](https://www.microsoft.com/download/details.aspx?id=42558)<br />-   [工作資料夾適用於 Windows 7 （32 位元下載）](https://www.microsoft.com/download/details.aspx?id=42559) |
| **操作** | -   [工作資料夾 iPad 應用程式：常見問題集](https://windows.microsoft.com/windows/work-folders-ipad-faq)（適用於使用者）<br />-   [工作資料夾的憑證管理](https://blogs.technet.com/b/filecab/archive/2013/08/09/work-folders-certificate-management.aspx)（部落格文章）<br />-   [監視 Windows Server 2012 R2 工作資料夾部署](https://blogs.technet.com/b/filecab/archive/2013/10/15/monitoring-windows-server-2012-r2-work-folders-deployments.aspx)（部落格文章）<br />-   [Windows PowerShell 中的方法 （工作資料夾） Cmdlet](https://docs.microsoft.com/powershell/module/syncshare/?view=win10-ps)<br />-   [Windows Server 2012 R2 Preview 版的儲存體和檔案服務 PowerShell Cmdlet 快速參考卡](http://blogs.technet.com/b/filecab/archive/2013/07/30/storage-and-file-services-powershell-cmdlets-quick-reference-card-for-windows-server-2012-r2-preview-edition.aspx) |
| **疑難排解** | -   [Windows Server 2012 R2 – 使用 IIS 網站和工作資料夾的 Resolving 通訊埠衝突](https://blogs.technet.com/b/filecab/archive/2013/10/15/windows-server-2012-r2-resolving-port-conflict-with-iis-websites-and-work-folders.aspx)（部落格文章）<br />-   [工作資料夾中的常見錯誤](https://social.technet.microsoft.com/wiki/contents/articles/30578.common-errors-in-work-folders.aspx) |
| **社群資源** | -   [檔案服務和儲存體論壇](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverfiles)<br />-   [Microsoft-檔案櫃部落格儲存體團隊](http://blogs.technet.com/b/filecab/)<br />-   [詢問目錄服務小組部落格](http://blogs.technet.com/b/askds/) |  
| **相關技術** | -   [Windows Server 2016 中的儲存體](../storage.md)<br>-   [檔案和存放服務](https://technet.microsoft.com/library/hh831487(v=ws.11).aspx)<br />-   [檔案伺服器資源管理員](https://technet.microsoft.com/library/hh831701(v=ws.11).aspx)<br />-   [資料夾重新導向、 離線檔案和漫遊使用者設定檔](https://technet.microsoft.com/library/hh848267(v=ws.11).aspx)<br />-   [BranchCache](https://technet.microsoft.com/library/hh831696(v=ws.11).aspx)<br />-   [DFS 命名空間和 DFS 複寫](https://technet.microsoft.com/library/jj127250(v=ws.11).aspx) |