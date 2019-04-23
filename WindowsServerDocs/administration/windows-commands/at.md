---
title: at
description: 適用於 Windows 命令主題**在**-排程命令和程式，在指定的時間和日期的電腦上執行。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff18fd16-9437-4c53-8794-bfc67f5256b3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 26ffa962541666e0e19b1c408bd6ab0b904296dd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832519"
---
# <a name="at"></a>at

>適用於：Windows Server （半年通道），Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012

排程在指定的時間和日期的電腦上執行的命令和程式。 您可以使用**在**只有在執行的排程服務時。 不含參數，**在**列出已排程的命令。
## <a name="syntax"></a>語法
```
at [\\computername] [[id] [/delete] | /delete [/yes]]
at [\\computername] <time> [/interactive] [/every:date[,...] | /next:date[,...]] <command>
```
## <a name="parameters"></a>參數
|參數|描述|
|----------------------|--------|
|\\\\\<computerName\>|指定遠端電腦。 如果您省略這個參數，**在**排程命令和在本機電腦上的程式。|
|\<id\>|指定指派給排程的命令的識別碼。|
|/delete|取消已排程的命令。 如果您省略*識別碼*，所有的電腦上的排程命令已取消。|
|/yes|答案是所有的查詢從系統中，當您刪除排定的事件。|
|\<time\>|指定當您想要執行命令時的時間。 時間會以小時： 分鐘以 24 小時制標記法 (也就是 00:00 [午夜] 23:59)。|
|/interactive|可讓*命令*與次登入之使用者的桌面互動*命令*執行。|
|/ 每個：|回合*命令*上每個指定的日期或天數週或個月 （例如，每個星期四或在每個月的第三天）。|
|\<date\>|指定當您想要執行命令時的日期。 您可以指定一或多個星期幾 (也就是類型**M**，**T**，**W**，**Th**，**F**，**S**，**Su**) 或每月的一或多個天數 （也就是輸入 1 到 31）。 以逗號分隔多個日期項目。 如果您省略*日期*，**在**會使用目前日期的月份。|
|/ 下一步:|回合*命令*下一步 （例如下, 一個星期四） 天一次。|
|\<command\>|指定 [Windows] 指令程式 （也就是.exe 或.com 檔案） 或您想要執行的批次程式 （也就是.bat 或.cmd 檔案）。 當此命令需要做為引數的路徑時，請使用絕對路徑 （也就是整個路徑開頭的磁碟機代號）。 如果命令是在遠端電腦上，指定伺服器的通用命名慣例 (UNC) 表示法，並共用名稱，而不是遠端磁碟機代號。|
|/?|在命令提示字元顯示說明。|
## <a name="remarks"></a>備註
-   **schtasks**是另一個命令列的排程工具，可用來建立和管理排程的工作。 如需詳細資訊**schtasks**，請參閱相關主題。
-   使用**在**  
    若要使用**在**，您必須是本機 Administrators 群組的成員。
-   正在載入 Cmd.exe  
    **在**不會自動載入 Cmd.exe 命令解譯器，再執行命令。 如果您不執行可執行檔 (.exe)，則必須明確地載入 Cmd.exe 命令開頭，如下所示： **cmd /c dir > c:\test.out**
-   檢視排程命令  
    當您使用**在**不用命令列選項，排定的工作會出現在表中，格式如下所示：
    ```
    Status  ID   Day        time        Command Line
    OK      1    Each F     4:30 PM     net send group leads status due
    OK      2    Each M     12:00 AM    chkstor > check.file
    OK      3    Each F     11:59 PM    backup2.bat
    ```
-   包括識別號碼 (*識別碼*)  
    當您包含識別號碼 (*識別碼*) 與**在**的命令提示字元中，單一項目資訊會顯示類似下列的格式：  
    ```
    Task ID:      1
    Status:       OK
    Schedule:     Each  F
    time of Day:  4:30 PM
    Command:      net send group leads status due
    ```
    排程的命令之後**在**，特別是有命令列選項，請檢查命令語法是否正確輸入命令**在**不用命令列選項。 如果命令列的資料行中的資訊不正確，delete 命令，並重新輸入它。 如果仍然不正確，請重新輸入具有較少的命令列選項的命令。
-   檢視結果  
    命令排程**在**以背景處理序執行。 輸出不會顯示在電腦螢幕上。 若要將輸出重新導向至檔案，使用重新導向符號 (>)。 如果您將輸出重新導向至檔案時，您需要使用逸出符號 (^) 之前重新導向的符號，不論您使用**在**在命令列或批次檔中。 例如，若要輸出重新導向至 Output.text，請輸入：  
    `at 14:45 c:\test.bat ^>c:\output.txt`  
    執行命令的目前目錄是 systemroot 資料夾。
-   變更系統時間  
    如果您變更電腦的系統時間之後您排程要執行的命令,**位於**，同步處理**在**與輸入的修改過的系統時間的排程器**在**而不需要命令列選項。
-   儲存命令  
    已排程的命令會儲存在登錄中。 如此一來，您不會遺失已排程的工作如果您重新啟動排程服務。
-   連線到網路磁碟機  
    確定用於存取網路的排程工作的重新導向的磁碟機。 排程服務可能無法存取重新導向的磁碟機，或可能不存在於，如果不同的使用者，會在排定的工作執行的時間登入重新導向的磁碟機。 請改用 UNC 路徑的排程工作。 例如:   
    `at 1:00pm my_backup \\\server\share`  
    請勿使用下列語法，其中**x:** 是使用者所做的連線：  
    `at 1:00pm my_backup x:`  
    如果您排程**位於**連線至共用的目錄中，使用磁碟機代號的命令包含**在**命令可中斷連接磁碟機，當您完成使用磁碟機。 如果磁碟機未中斷連線，不在命令提示字元中，您可以使用指派磁碟機代號。
-   72 小時後停止的工作  
    根據預設，使用排程的工作**在**72 小時後的命令停止。 您可以修改登錄來變更此預設值。
    1.  啟動登錄編輯程式 (regedit.exe)。
    2.  找出並按一下下列登錄機碼：**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Schedule**
    3.  在 編輯 功能表中，按一下 新增值，然後新增下列登錄值：數值名稱︰ atTaskMaxHours 資料類型： reg_DWOrd 基底：十進位值的資料：0. 在數值資料欄位的 0 值表示沒有限制，不會停止。 從 1 到 99 的值表示小時的數。
**注意**
-   不正確地編輯登錄可能會對系統造成嚴重的損害。 變更登錄之前，您應該先備份電腦所有的重要資料。
-   工作排程器和**在**命令  
    您可以使用 排定的工作資料夾來檢視或修改的工作，使用所建立的設定**在**命令。 當您排程工作，使用**位於**命令時，工作會列在排定的工作資料夾，如下所示的名稱：**at3478**。 不過，如果您修改在透過已排程的工作資料夾的工作，它會升級到一般的排程工作。 工作項目已無法再看到**在**命令，並在帳戶設定不會再套用到它。 工作，您必須明確地輸入的使用者帳戶和密碼。
## <a name="examples"></a>範例
若要顯示在行銷伺服器上排程的命令清單，請輸入：

`at \\marketing`

若要深入了解識別數字 3 Corp 伺服器上的命令，請輸入：

`at \\corp 3`

若要排程在上午 8:00 執行公司伺服器上的 net share 命令 和重新導向到維護伺服器，報表的共用的目錄和 Corp.txt 檔案中，類型的清單：

`at \\corp 08:00 cmd /c "net share reports=d:\marketing\reports >> \\maintenance\reports\corp.txt"`

若要備份至磁帶機每隔五天午夜 Marketing 伺服器硬碟機，建立批次程式，稱為 Archive.cmd，其中包含備份的命令，並接著排程要執行的批次程式，輸入：

`at \\marketing 00:00 /every:5,10,15,20,25,30 archive`

若要取消目前的伺服器上排程的所有命令，請清除**在**排程資訊，如下所示：

`at /delete`

若要執行不是可執行檔 (也就是.exe) 檔案的命令，在前面的命令並搭配**cmd /c**載入 Cmd.exe，如下所示：

`cmd /c dir > c:\test.out`