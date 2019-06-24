---
title: robocopy
description: 了解如何使用 Windows 和 Windows Server 中的 robocopy 命令來複製檔案
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4c6e8e9-fcb3-4a4a-9d04-2d8c367b6354
author: coreyp-at-msft
ms.author: coreyp
manager: lizapo
ms.date: 07/25/2018
ms.openlocfilehash: 7ab2eff32b105916d979a954275e9c9122a06903
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441719"
---
# <a name="robocopy"></a>robocopy

將資料複製檔案。

## <a name="syntax"></a>語法

```
robocopy <Source> <Destination> [<File>[ ...]] [<Options>]
```

## <a name="parameters"></a>參數

|   參數    |                                                                                            描述                                                                                             |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   \<來源 >    |                                                                            指定來源目錄的路徑。                                                                             |
| \<目的地 > |                                                                          指定的目的地目錄的路徑。                                                                          |
|    \<檔案 >     | 指定要複製的檔案。 您可以使用萬用字元 ( **&#42;** 或是 **？** )，如果您想要。 如果**檔案**未指定參數，  **\*。\\** \*做為預設值。 |
|   \<Options>   |                                                                    指定要搭配使用的選項**robocopy**命令。                                                                     |

### <a name="copy-options"></a>複製選項

|選項|描述|
|------|-----------|
|/s|複製子目錄。 請注意，此選項會排除空的目錄。|
|/e|複製子目錄。 請注意，這個選項會包含空的目錄。 如需詳細資訊，請參閱[備註](#remarks)。|
|/lev:\<N >|複製只傳回前*N*來源目錄樹狀結構的層級。|
|/z|將檔案複製可重新啟動模式。|
|/b|將檔案複製備份 」 模式。|
|/zb|使用可重新啟動模式。 如果存取被拒，此選項會使用備份 」 模式。|
|/efsraw|將所有加密的檔案複製以 EFS RAW 模式。|
|/copy:\<CopyFlags>|指定要複製的檔案屬性。 以下是有效的值，這個選項：</br>**D**資料</br>**A**屬性</br>**T**時間戳記</br>**S** NTFS 存取控制清單 (ACL)</br>**O**擁有者資訊</br>**U**稽核資訊</br>預設值**CopyFlags**是**DAT** （資料、 屬性和時間戳記）。|
|/dcopy:\<copyflags\>|定義要複製的目錄項目。 預設值是 DA. 選項為 D = data，A = 屬性和 T = 時間戳記。|
|/sec|將檔案複製具有安全性 (相當於 **/copy:DATS**)。|
|/copyall|複製所有的檔案資訊 (相當於 **/copy**)。|
|/nocopy|不複製任何檔案資訊 (適用於 **/清除**)。|
|/secfix|修正檔案安全性的所有檔案，甚至是略過的。|
|/timfix|修正檔案的時間所有檔案，甚至是略過的。|
|/purge|目的地檔案和目錄不再存在於來源中刪除。 如需詳細資訊，請參閱[備註](#remarks)。|
|/mir|鏡像目錄樹狀結構 (相當於 **/e**加上 **/清除**)。 如需詳細資訊，請參閱[備註](#remarks)。|
|/mov|移動檔案，並複製之後從來源刪除它們。|
|/move|移動檔案和目錄，並複製之後從來源刪除它們。|
|/a+:[RASHCNET]|將指定的屬性加入至複製的檔案中。|
|/a-:[RASHCNET]|從複製的檔案中移除指定的屬性。|
|/create|建立樹狀目錄和僅限零長度檔案。|
|/fat|使用只 8.3 FAT 字元長度的檔案名稱，以建立目的地檔案。|
|/256|關閉很長的路徑 （長度超過 256 個字元） 的支援。|
|/ mon:\<N >|監視來源，並會在再次執行，當多個*N*偵測到變更。|
|/mot:\<M >|監視來源，並執行中再次*M*分鐘如果偵測到變更。|
|/MT[:N]|建立具有多執行緒的複本*N*執行緒。 *N*必須是介於 1 到 128 之間的整數。 預設值*N*為 8。</br>**/MT**參數無法搭配 **/IPG**並 **/EFSRAW**參數。</br>輸出使用的重新導向 **/log**以提升效能的選項。</br>注意:/MT 參數適用於 Windows Server 2008 R2 和 Windows 7。|
|/rh:hhmm-hhmm|指定新的複本可能已啟動的執行的時間。|
|/pf|檢查每個檔案 （沒有每個階段） 上，執行時間。|
|/ipg:n|指定間的封包間距，以釋放在緩慢的行上的頻寬。|
|/sl|不遵循符號連結，並改為建立一份連結。|

> [!IMPORTANT]
> 使用時 **/SECFIX**複製選項，指定您想要複製也使用其中一個其他複本選項的安全性資訊的類型：
>- **/COPYALL**
>- **/COPY:O**
>- **/COPY:S**
>- **/COPY:U**
>- **/SEC**

### <a name="file-selection-options"></a>檔案選擇的選項

|選項|描述|
|------|-----------|
|/a|只檔案，複製**封存**屬性設定。|
|/m|只檔案，複製**封存**屬性設定，並且重設**封存**屬性。|
|/ia:[RASHCNETO]|包含任何指定的屬性會設定的檔案。|
|/xa:[RASHCNETO]|會排除任何指定的屬性設定的檔。|
|/xf \<FileName>[ ...]|排除符合指定之名稱或路徑的檔案。 請注意，*檔名*可包含萬用字元 ( **&#42;** 並**嗎？** )。|
|/xd \<Directory>[ ...]|排除符合指定的名稱和路徑的目錄。|
|/xc|排除已變更的檔案。|
|/xn|排除較新的檔案。|
|/xo|排除較舊的檔案。|
|/xx|排除額外的檔案和目錄。|
|/xl|會排除 「 領域獨自站哨"的檔案和目錄。|
|/is|包含相同的檔案。|
|/it|包含 「 調整 」 的檔案。|
|/ 最大：\<N >|指定檔案大小上限 (若要排除檔案大於*N*位元組為單位)。|
|/min:\<N >|指定檔案大小下限 (若要排除檔案小於*N*位元組為單位)。|
|/maxage:\<N >|指定的最大的檔案存在時間 (排除檔案的時限*N*天或日期)。|
|/minage:\<N >|指定的最短檔案存在時間 (排除的檔案較*N*天或日期)。|
|/maxlad:\<N >|指定上次存取日期的最大值 (因為未使用的檔案中排除*N*)。|
|/minlad:\<N >|指定最小值上次存取日期 (自使用的檔案中排除*N*) 如果*N*是小於 1900年*N*指定的天數。 否則，請*N*指定的日期，格式為 YYYYMMDD。|
|/xj|排除預設通常會包含的連接點。|
|/fft|假設 FAT 檔案時間 （兩秒有效位數）。|
|/dst|補償一小時 DST 時間差異。|
|/xjd|排除目錄的連接點。|
|/xjf|排除檔案的連接的點。|

### <a name="retry-options"></a>重試選項

|選項|描述|
|------|-----------|
|/r:\<N >|失敗的複本上指定的重試次數。 預設值*N*為 1000000 （1 百萬個重試）。|
|/w:\<N >|指定重試次數，以秒為單位之間的等待時間。 預設值*N*為的 30 （等候 30 秒的時間）。|
|/reg|將儲存在指定的值 **/r**並 **/w**為登錄中的預設設定的選項。|
|/tbd|指定系統將會等候定義的共用名稱 （重試錯誤 67）。|

### <a name="logging-options"></a>記錄選項

|選項|描述|
|------|-----------|
|/l|指定只列出檔案 （並不會複製、 刪除或時間戳記）。|
|/x|報告所有額外的檔案，不只是那些已選取。|
|/v|會產生詳細資訊輸出，並顯示所有略過的檔案。|
|/ts|在輸出中包含來源檔案時間戳記。|
|/fp|在輸出中包含的檔案完整路徑名稱。|
|/bytes|列印大小，以位元組為單位。|
|/ns|指定檔案大小不會記錄。|
|/nc|指定不是要記錄檔案類別。|
|/nfl|指定檔案名稱不會記錄。|
|/ndl|指定不是要記錄的目錄名稱。|
|/np|指定將不會顯示進度的複製作業 （檔案或目錄複製到目前為止的數字）。|
|/eta|顯示的估計的時間抵達 (ETA) 的複製的檔案。|
|/ 記錄檔：\<記錄檔 >|寫入記錄檔 （會覆寫現有的記錄檔） 中的狀態輸出。|
|/log+:\<LogFile>|寫入記錄檔 （將輸出附加至現有的記錄檔） 中的狀態輸出。|
|/unicode|以 Unicode 文字的顯示狀態輸出。|
|/unilog:\<記錄檔 >|將寫入狀態 （覆寫現有的記錄檔） 的 Unicode 文字形式輸出至記錄檔。|
|/unilog+:\<LogFile>|寫入輸出記錄檔為 Unicode 文字 （將輸出附加至現有的記錄檔） 的狀態。|
|/tee|將狀態輸出寫入至主控台視窗中，以及記錄檔。|
|/njh|指定為無作業標頭。|
|/njs|指定為無作業摘要。|

### <a name="job-options"></a>工作選項

|選項|描述|
|------|-----------|
|/job:\<JobName>|指定參數是衍生自該具名的工作檔案。|
|/ 儲存：\<JobName >|指定參數是儲存在具名的工作檔案。|
|/quit|（若要檢視參數） 的處理命令列之後結束。|
|/nosd|表示指定沒有來源目錄。|
|/nodd|表示不指定任何目的地目錄。|
|/if|包含指定的檔案。|

### <a name="exit-return-codes"></a>（傳回） 的結束代碼

值 | 描述
-- | --
0 | 已不複製任何檔案。 不遇到任何失敗。  沒有任何檔案已不相符。 檔案已存在於目的地目錄中;因此，已略過複製作業。
1 | 已成功地複製所有檔案。
2 | 有一些額外檔案目的地目錄中的，不會出現在 [source] 目錄。 已不複製任何檔案。
3 | 某些檔案會被複製。 其他檔案已存在。 不遇到任何失敗。
5 | 某些檔案會被複製。 某些檔案已不相符。 不遇到任何失敗。
6 | 其他檔案和不相符的檔案存在。 已將檔案複製，並不發生任何失敗。 這表示檔案已存在於目的地目錄。
7 | 已複製檔案，檔案不相符，並存在其他的檔案已存在。
8 | 沒有複製數個檔案。

> [!NOTE]
> 任何大於 8，表示複製作業期間發生至少一個錯誤的值。

### <a name="remarks"></a>備註

-   **/Mir**選項相當於 **/e**加上 **/清除**一個些許的不同行為的選項：  
    -   具有 **/e**加上 **/清除**選項，如果目的地目錄存在，目的地目錄的安全性設定不覆寫。
    -   具有 **/mir**選項，如果目的地目錄存在，目的地目錄的安全性設定會覆寫。

#### <a name="additional-references"></a>其他參考資料

[命令列語法關鍵](command-line-syntax-key.md)