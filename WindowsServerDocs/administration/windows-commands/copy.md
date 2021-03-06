---
title: copy
description: Copy 命令的參考文章，可將一或多個檔案從某個位置複製到另一個位置。
ms.topic: reference
ms.assetid: 9624d4a1-349a-4693-ad00-1d1d4e59e9ac
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 129a6e4575be47ab876ef6943aeca803269ac529
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89629229"
---
# <a name="copy"></a>copy

將一或多個檔案從某個位置複製到另一個位置。

> [!NOTE]
> 您也可以從 [修復主控台] 使用 [ **複製** ] 命令，並使用不同的參數。 如需有關修復主控台的詳細資訊，請參閱 [Windows 修復環境 (Windows RE) ](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)。

## <a name="syntax"></a>語法

```
copy [/d] [/v] [/n] [/y | /-y] [/z] [/a | /b] <source> [/a | /b] [+<source> [/a | /b] [+ ...]] [<destination> [/a | /b]]
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| --------- | ----------- |
| /d | 允許複製加密的檔案儲存為目的地的解密檔案。 |
| /v | 確認是否已正確寫入新檔案。 |
| /n | 當複製名稱超過八個字元或副檔名超過三個字元的檔案時，會使用短檔案名（如果有的話）。 |
| /y | 隱藏提示以確認您想要覆寫現有的目的地檔案。 |
| /-y | 提示您確認是否要覆寫現有的目的地檔案。 |
| /z | 將網路檔案複製到可重新開機的模式。 |
| /a | 表示 ASCII 文字檔。 |
| /b | 表示二進位檔案。 |
| `<source>` | 必要。 指定您要從中複製檔案或檔案集的位置。 *來源* 可以包含磁碟機號與冒號、目錄名稱、檔案名或這些的組合。 |
| `<destination>` | 必要。 指定您要複製檔案或檔案集的位置。 *目的地* 可以是由磁碟機號和冒號、目錄名稱、檔案名或這些的組合所組成。 |
| /? | 在命令提示字元顯示說明。 |

#### <a name="remarks"></a>備註

- 您可以複製使用檔案結尾字元 (CTRL + Z) 的 ASCII 文字檔來指出檔案結尾。

- 如果 **/a** 在命令列上的檔案清單之前或之後，則會套用至所有列出的檔案，直到 **複製** 遇到 **/b**為止。 在此情況下， **/b** 會套用至位於 **/b**之前的檔案。

    **/A**的影響取決於其在命令列字串中的位置：
      - 如果 **/a** 遵循 *來源*， **copy** 命令會將檔案視為 ASCII 檔，並將第一個檔案結尾字元之前的資料複製 (CTRL + Z) 。
      - 如果 **/a** 遵循 *destination*， **copy** 命令會將檔案結尾字元 (CTRL + Z) 新增為檔案的最後一個字元。

- 如果 **/b** 指示命令直譯器讀取目錄中的檔案大小所指定的位元組數目。 **/b** 是 **複製**的預設值，除非 **複製** 結合了檔案。

- 如果在命令列上的檔案清單之前或之後出現 **，則它** 會套用至所有列出的檔案，直到 **複製** 遇到 **/a**為止。 在此情況下， **/a** 會套用至位於 **/a**之前的檔案。

    **/B**的影響取決於其在命令列字串中的位置：-如果 **/b**跟隨*來源*， **copy**命令會複製整個檔案，包括任何檔案結尾字元 (CTRL + Z) 。
        -如果**在***目的地*之後，**複製**命令不會將檔案結尾字元新增 (CTRL + Z) 。

- 如果無法驗證寫入作業，就會出現錯誤訊息。 雖然 **copy** 命令很少會發生記錄錯誤，但您可以使用 **/v** 來確認已正確記錄重要資料。 **/V**命令列選項也會減緩**複製**命令，因為磁片上所記錄的每個磁區都必須經過檢查。

- 如果**COPYCMD**環境變數中的 **/y**是預設值，您可以在命令列使用 **/-y**覆寫此設定。 除非在批次腳本中執行 **copy** 命令，否則當您取代這個設定時，系統預設會提示您。

- 若要附加檔案，請指定*目的地*的單一檔案，但是*來源* (的多個檔案，則使用萬用字元或*file1* + *file2* + *file3*格式) 。

- 如果連接在複製階段遺失 (例如，如果伺服器離線，中斷連線) ，您可以在重新建立連線之後，使用 **copy/z** 繼續進行。 **/Z**選項也會顯示針對每個檔案完成的複製作業百分比。

- 您可以將裝置名稱替換成一或多個出現的 *來源* 或 *目的地*。

- 如果 *目的地* 是裝置 (例如，Com1 或 Lpt1) ， **/b** 選項會將資料以二進位模式複製到裝置。 在二進位模式中， **copy/b** 會複製所有的字元 (包括特殊字元，例如 Ctrl + C、Ctrl + S、Ctrl + Z，然後輸入) 至裝置的資料。 但是，如果您省略 **/b**，資料會以 ASCII 模式複製到裝置。 在 ASCII 模式中，特殊字元可能會在複製過程中造成檔案的合併。

- 如果您未指定目的地檔案，則會使用相同的名稱、修改日期和修改時間來建立複本，做為原始檔案。 新的複本會儲存在目前磁片磁碟機的目錄中。 如果來源檔案是在目前的磁片磁碟機上，而且您沒有為目的地檔案指定不同的磁片磁碟機或目錄，則 **複製** 命令會停止，並顯示下列錯誤訊息：

    ```
    File cannot be copied onto itself
    0 File(s) copied
    ```

- 如果您在 *來源*中指定多個檔案， **copy** 命令會使用 [ *目的地*] 中指定的檔案名，將這些檔案全部結合成單一檔案。 除非您使用 **/b**選項，否則**copy**命令會假設合併的檔案是 ASCII 檔案。

- 若要複製長度為0個位元組的檔案，或複製目錄的所有檔案和子目錄，請使用 [xcopy 命令](xcopy.md)。

- 若要將目前的時間和日期指派給檔案而不修改檔案，請使用下列語法：

    ```
    copy /b <source> +,,
    ```

    其中逗號表示已刻意省略 *目的地* 參數。

## <a name="examples"></a>範例

若要將稱為 *memo.doc* 的檔案複製到目前磁片磁碟機中的 *letter.doc* ，並確定檔案結尾字元 (CTRL + Z) 位於複製的檔案結尾，請輸入：

```
copy memo.doc letter.doc /a
```

若要將名為配置資源的檔案從目前磁片磁碟機和目錄複寫到位於磁片磁碟機 C*上名為**鳥*的現有目錄，請輸入：

```
copy robin.typ c:\birds
```

> [!NOTE]
> 如果 *鳥* 目錄不存在，則 *會將檔案配置檔案複製* 到名為 *鳥* 的檔案中，該檔案位於磁片磁碟機 C 的磁片根目錄中。

若要結合 *Mar89. rpt*、 *Apr89. rpt*和 *May89*（位於目前的目錄中），並將它們放在名為 *Report* (檔案中，請在 [目前的目錄]) 中輸入：

```
copy mar89.rpt + apr89.rpt + may89.rpt Report
```

> [!NOTE]
> 如果您合併檔案， **copy** 命令會將目的地檔案標示為目前的日期和時間。 如果您省略 *destination*，檔案會合並並儲存在清單中第一個檔案的名稱下。

若要合併 *報表*中的所有檔案，當名稱為 *report* 的檔案已經存在時，請輸入：

```
copy report + mar89.rpt + apr89.rpt + may89.rpt
```

若要將目前目錄中副檔名為 .txt 的所有檔案合併為 *Combined.doc*的單一檔案，請輸入：

```
copy *.txt Combined.doc
```

若要使用萬用字元將數個二進位檔案合併成一個檔案，請包含 **/b**。 這可防止 Windows 將 CTRL + Z 視為檔案結尾字元。 例如，輸入：

```
copy /b *.exe Combined.exe
```

> [!CAUTION]
> 如果您合併二進位檔案，產生的檔案可能因為內部格式而無法使用。

- 結合副檔名為 .txt 的每個檔案與其對應的 ref 檔案，會建立具有相同檔案名的檔案，但副檔名為 .doc。 **Copy**命令會將*file1.txt*與*file1*結合成表單*file1.doc*，然後命令會將*file2.txt*與*file2*結合以形成*file2.doc*等等。 例如，輸入：

```
copy *.txt + *.ref *.doc
```

若要結合副檔名為 .txt 的所有檔案，然後將副檔名為 ref 的所有檔案合併成一個名為 *Combined.doc*的檔案，請輸入：

```
copy *.txt + *.ref Combined.doc
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [xcopy 命令](xcopy.md)
