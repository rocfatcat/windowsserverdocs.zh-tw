---
title: graftabl
description: Graftabl 命令的參考文章，可讓 Windows 作業系統以圖形模式顯示延伸字元集。
ms.topic: reference
ms.assetid: b08351d4-3d24-490c-86f6-1252da11d923
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9f8759679865c87c11417c64ef130736de2a1e9e
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634612"
---
# <a name="graftabl"></a>graftabl

讓 Windows 作業系統以圖形模式顯示延伸字元集。 如果使用時不含參數， **graftabl** 會顯示上一個和目前的字碼頁。

## <a name="syntax"></a>語法

```
graftabl <codepage>
graftabl /status
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| --------- | ----------- |
| `<codepage>` | 指定字碼頁，以在圖形模式中定義擴充字元的外觀。 有效的字碼頁識別碼為：<ul><li>**437** -美國</li><li>**850** -多語系 (拉丁) </li><li>**852** -斯拉夫 (拉丁 II) </li><li>**855** -斯拉夫 (俄文) </li><li>**857** -土耳其文</li><li>**860** -葡萄牙文</li><li>**861** -冰島文</li><li>**863** -加拿大（法文）</li><li>**865** -北歐</li><li>**866** -俄文</li><li>**869** -新式希臘文</li></ul> |
| /status | 顯示此命令目前使用的字碼頁。 |
| /? | 在命令提示字元顯示說明。 |

#### <a name="remarks"></a>備註

- **Graftabl**命令只會影響您所指定之字碼頁的擴充字元的監視器顯示。 它不會變更實際的主控台輸入字碼頁面。 若要變更控制台輸入字碼頁面，請使用 [mode](mode.md) 或 [chcp](chcp.md) 命令。

- 每個結束代碼和它的簡短描述：

    | 結束碼 | 描述 |
    | --------- | ----------- |
    | 0 | 已成功載入字元集。 未載入任何先前的字碼頁。 |
    | 1 | 指定了不正確的參數。 未採取任何動作。 |
    | 2 | 發生檔案錯誤。 |

- 您可以使用批次程式中的 ERRORLEVEL 環境變數來處理 **graftabl**所傳回的結束代碼。

### <a name="examples"></a>範例

若要查看 **graftabl**所使用的目前字碼頁，請輸入：

```
graftabl /status
```

若要載入字碼頁437的圖形字元集 (美國) 至記憶體中，請輸入：

```
graftabl 437
```

若要載入字碼頁850的圖形字元集， (多語系) 至記憶體中，請輸入：

```
graftabl 850
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [freedisk 命令](freedisk.md)

- [mode 命令](mode.md)

- [chcp 命令](chcp.md)
