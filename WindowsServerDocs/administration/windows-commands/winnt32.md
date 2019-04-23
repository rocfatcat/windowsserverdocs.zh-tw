---
title: winnt32
description: '適用於 Windows 命令主題 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a0a6fb3-ba4e-4ace-8984-7f6d3875560e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 28675ac6d5a1f1a7f56a9b72ef11a3e99e4ed130
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851259"
---
# <a name="winnt32"></a>winnt32

>適用於：Windows Server （半年通道），Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012

Windows Server 2003 中執行的安裝或升級產品。 您可以執行**winnt32**在命令提示字元中執行 Windows Server 2003 中的 Windows 95、 Windows 98、 Windows Millennium edition、 Windows NT、 Windows 2000，Windows XP 或產品的電腦上。 如果您執行**winnt32**的電腦上執行 Windows NT 4.0 版，您必須先套用 Service Pack 5 或更新版本。
## <a name="syntax"></a>語法
```
winnt32 [/checkupgradeonly] [/cmd: <CommandLine>] [/cmdcons] [/copydir:{i386|ia64}\<FolderName>] [/copysource: <FolderName>] [/debug[<Level>]:[ <FileName>]] [/dudisable] [/duprepare: <pathName>] [/dushare: <pathName>] [/emsport:{com1|com2|usebiossettings|off}] [/emsbaudrate: <BaudRate>] [/m: <FolderName>]  [/makelocalsource] [/noreboot] [/s: <Sourcepath>] [/syspart: <DriveLetter>] [/tempdrive: <DriveLetter>] [/udf: <ID>[,<UDB_File>]] [/unattend[<Num>]:[ <AnswerFile>]]
```
### <a name="parameters"></a>參數
|參數|描述|
|-------|--------|
|/checkupgradeonly|檢查您的電腦與 Windows Server 2003 中的產品的升級相容性。<br /><br />如果您使用這個選項搭配 **/unattend**，不須有任何使用者輸入。  否則，結果會顯示在畫面上，並將它們儲存在您指定的檔案名稱。 預設檔案名稱是**upgrade.txt** systemroot 資料夾中。|
|/cmd|會指示安裝程式安裝程式的最終階段之前執行特定命令。 會發生這種情況是您的電腦重新啟動並安裝已收集到必要的設定資訊之後，但之前安裝程式完成之後。|
|\<CommandLine>|指定要安裝的最終階段之前執行命令列。|
|/cmdcons|在 x86 型電腦上，會復原主控台安裝為啟動選項。  修復主控台是命令列介面，讓您執行工作，例如啟動和停止服務，以及存取本機的磁碟機 （包括使用 NTFS 格式化磁碟機）。 您只能使用 **/cmdcons**選項安裝完成之後。|
|/copydir|建立安裝作業系統檔案所在的資料夾內的其他資料夾。  例如，適用於 x86 和 x64 型電腦，您可以建立名為的資料夾*Private_drivers* i386 來源資料夾，您的安裝和驅動程式檔案的資料夾中。 型別**/copydir:i386\\* * * Private_drivers*讓安裝程式將該資料夾複製到您新安裝的電腦，讓新的資料夾位置**systemroot** \\*Private_drivers *。<br /><br />-   **i386**指定 i386<br />-   **ia64**指定 ia64<br /><br />您可以使用 **/copydir**建立您想要的多個其他資料夾。|
|\<FolderName>|指定您建立來保存修改您的站台的資料夾。|
|/copysource|建立額外的暫存資料夾，在其中安裝作業系統檔案的資料夾內。 您可以使用 **/copysource**建立您想要的多個其他資料夾。<br /><br />不同於資料夾 **/copydir**建立時， **/copysource**安裝程式完成之後，會刪除資料夾。|
|/debug|例如，在層級指定，會建立偵錯記錄檔 **/debug4:Debug.log**。  預設的記錄檔是**C:\systemroot\winnt32.log**，及|
|\<level>|層級的值和描述<br /><br />-   0:嚴重錯誤<br />-   1:錯誤<br />-   2:預設層級。 警告<br />-   3:資訊<br />-4： 詳細的偵錯資訊<br /><br />每個層級包含其下的層級。|
|/dudisable|防止執行動態更新。 沒有動態更新時，安裝程式會執行只能使用原始的安裝程式檔案。 此選項會停用動態更新，即使您使用回應檔案，並指定該檔案中的動態更新選項。|
|/duprepare|If&lt 屬於安裝共用的準備工作，以便它可以搭配您從 Windows Update 網站下載的動態更新檔案。 此共用可用的 Windows XP 安裝多個用戶端。|
|\<pathName>|指定完整路徑名稱。|
|/dushare|指定在其您先前下載的動態更新檔案 （用於安裝的更新檔案） 的共用，從 Windows Update 網站，並在其中您之前已執行 **/duprepare: * * * < 路徑名稱 >*。 用戶端上執行時，指定將用戶端安裝使用更新的檔案中指定的共用上<pathName>。|
|/emsport|啟用或停用緊急管理服務，在安裝期間，並在安裝伺服器作業系統之後。 使用緊急管理服務，您可以從遠端管理伺服器，以在本機鍵盤、 滑鼠及監視器，例如當網路無法使用時通常需要的緊急情況下，或伺服器的運作不正常。 緊急管理服務都有特定的硬體需求，並只適用於 Windows Server 2003 中的產品。<br /><br />-   **com1**只適用於 x86 型電腦 （不 Itanium 架構的電腦）。<br />-   **com2**只適用於 x86 型電腦 （不 Itanium 架構的電腦）。<br />-Default。 使用在 [BIOS 序列埠主控台重新導向 (SPCR)] 資料表中，或在 Itanium 架構的系統中，透過 EFI 主控台裝置路徑指定的設定。 如果您指定**usebiossettings**並沒有任何 SPCR 表或適當的 EFI 主控台裝置路徑，將不會啟用緊急管理 Lbs。<br />-   **關閉**緊急管理服務會停用。 您稍後可以啟用它，藉由修改開機設定。|
|/emsbaudrate|x86 型電腦，指定緊急管理服務的傳輸速率。 （此選項不適用於 Itanium 架構的電腦。）必須搭配 **/emsport:com1**或是 **/emsport:com2** (否則 **/emsbaudrate**會被忽略)。|
|\<BaudRate>|指定的 9600，baudrate 19200、 57600 或 115200。 預設值為 9600。|
|/m|指定安裝程式從替代位置複製替代檔案。  會先尋找替代位置中，如果檔案存在，才能使用它們而不是從預設位置檔案的安裝程式的指示。|
|/makelocalsource|會指示安裝程式將所有的安裝來源檔案複製到本機硬碟。  使用 **/makelocalsource**從光碟中無法使用稍後安裝 cd 時，提供安裝檔案進行安裝時。|
|/noreboot|會指示安裝程式未重新啟動電腦，以便您可以執行另一個命令完成檔案複製階段的安裝程式。|
|/s|指定您的安裝檔案的來源位置。 若要同時從多部伺服器複製的檔案，請輸入 **/s:**\<Sourcepath > 多次 （最多八個） 的選項。 如果您多次輸入選項，必須可使用指定的第一部伺服器，或安裝程式將會失敗。|
|\<Sourcepath>|指定完整來源路徑名稱。|
|/syspart|在 x86 型電腦上，指定您可以將安裝程式啟動檔案複製到硬碟、 標示為作用中，磁碟和將安裝到另一部電腦的 磁碟。 當您啟動該電腦時，它會自動啟動安裝程式的下一個階段。<br /><br />您一律必須使用 **/tempdrive**參數搭配 **/syspart**參數。<br /><br />您可以啟動**winnt32**具有 **/syspart**執行 Windows Server 2003 中的 Windows NT 4.0、 Windows 2000，Windows XP 或產品的 x86 型電腦上的選項。 如果電腦執行 Windows NT 4.0 版，它就會需要 Service Pack 5 或更新版本。 電腦無法執行，Windows 95、 Windows 98 或 Windows Millennium edition。|
|\<DriveLetter>|指定的磁碟機代號。|
|/tempdrive|將指定的磁碟分割上的暫存檔案的安裝程式，會指示。<br /><br />適用於新安裝中，伺服器作業系統也會安裝在指定的磁碟分割上。<br /><br />進行升級時， **/tempdrive**選項會影響僅限暫存檔案的位置; 將升級作業系統，在您執行的資料分割**winnt32**。|
|/udf|表示識別項 (\<識別碼 >)，安裝程式會使用來指定唯一性 Database (UDB) 檔案修改回應檔案的方式 (請參閱 < **/unattend**選項)。  UDB 覆寫在回應檔案中的值和識別項可讓您決定使用 UDB 檔案中的哪些值。 例如， **/udf:RAS_user,Our_company.udb** RAS_user 識別碼 Our_company.udb 檔案中指定的設定會覆寫。 如果沒有\<UDB_file > 指定，則安裝程式會提示使用者插入包含的磁碟 **$Unique$.udb**檔案。|
|\<ID>|表示用來指定如何唯一性 Database (UDB) 檔案修改回應檔案的識別碼。|
|\<UDB_file>|指定唯一性 Database (UDB) 檔案。|
|/unattend|在 x86 型電腦上，升級舊版的 Windows NT 4.0 Server （含 Service Pack 5 或更新版本） 或 Windows 2000 中自動的安裝模式。 所有使用者設定都取自先前的安裝，因此在安裝期間需要不需要使用者介入。|
|\<num>|指定設定的時間之間的秒數可讓您完成複製的檔案，以及當重新啟動您的電腦。 您可以使用\<Num > Windows Server 2003 中執行 Windows 98、 Windows Millennium edition、 Windows NT、 Windows 2000，Windows XP 或產品的電腦上。 如果電腦執行 Windows NT 4.0 版，它就會需要 Service Pack 5 或更新版本。|
|\<AnswerFile>|安裝程式提供您的自訂規格|
|/?|在命令提示字元顯示說明。|

## <a name="remarks"></a>備註
如果您要部署 Windows XP 用戶端電腦上，您可以使用隨附於 Windows XP 的 winnt32.exe 的版本。 部署 Windows XP 的另一種方式是使用的 winnt32.msi，透過 Windows 安裝程式，IntelliMirror 一部分的運作方式設定的技術。 如需有關用戶端部署的詳細資訊，請參閱說明 Windows Server 2003 Deployment Kit[使用 Windows Deployment and Resource Kits](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx)。

在 Itanium 型電腦上， **winnt32**可以從可延伸韌體介面 (EFI) 或 Windows Server 2003 Enterprise、 Windows Server 2003 R2 Enterprise、 Windows Server 2003 R2 Datacenter 或 Windows Server 2003 執行。資料中心。 此外，在 Itanium 架構的電腦上， **/cmdcons**並 **/syspart**是無法使用，並且與升級相關的選項不提供。
如需硬體相容性的詳細資訊，請參閱[硬體相容性](https://technet.microsoft.com/library/cc757927(v=ws.10).aspx)。
如需詳細使用動態更新及安裝多個用戶端的相關資訊，請參閱說明 Windows Server 2003 Deployment Kit[使用 Windows Deployment and Resource Kits](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx)。
如需修改開機設定的詳細資訊，請參閱資源套件適用於 Windows Server 2003 與 Windows 部署。 如需詳細資訊，請參閱 <<c0> [ 使用 Windows Deployment and Resource Kits](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx)。
使用 **/unattend**自動安裝的命令列選項 affirms 您已閱讀並接受 Microsoft 授權合約適用於 Windows Server 2003。 在之前您可以使用此命令列選項來代表非您自己組織中安裝 Windows Server 2003，您必須確認使用者 （不論是以個人或單一實體） 收到、 讀取，並接受 Microsoft 授權條款該產品的協議。  Oem 可能被賣給終端使用者機器上，未指定此金鑰。

## <a name="additional-references"></a>其他參考資料
-   [命令列語法關鍵](command-line-syntax-key.md)
