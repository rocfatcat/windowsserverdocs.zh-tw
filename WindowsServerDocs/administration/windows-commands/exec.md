---
title: exec
description: Exec 命令的參考文章，此命令會在本機電腦上執行腳本檔案。
ms.topic: reference
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 668dc3cf3d93d11066d7dece4309f586b3a5b964
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635968"
---
# <a name="exec"></a>exec

在本機電腦上執行指令檔。 此命令也會在備份或還原順序中複製或還原資料。 如果腳本失敗，則會傳回錯誤並結束 DiskShadow。

檔案可以是 **cmd** 腳本。

## <a name="syntax"></a>語法

```
exec <scriptfile.cmd>
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| --------- | ----------- |
| `<scriptfile.cmd>` | 指定要執行的腳本檔案。 |

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [diskshadow 命令](diskshadow.md)
