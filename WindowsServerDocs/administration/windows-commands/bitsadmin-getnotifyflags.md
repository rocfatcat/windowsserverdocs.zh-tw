---
title: bitsadmin getnotifyflags
description: Bitsadmin getnotifyflags 命令的參考文章，此命令會抓取指定作業的通知旗標。
ms.topic: reference
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b7cdc2d65316bfcc856bb0fe55a9379d4fc6ba6b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631904"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags

抓取指定作業的通知旗標。

## <a name="syntax"></a>語法

```
bitsadmin /getnotifyflags <job>
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| -------------- | -------------- |
| 作業 | 作業的顯示名稱或 GUID。 |

## <a name="remarks"></a>備註

作業可以包含下列一或多個通知旗標：

| 旗標 | 描述 |
| ----- | ----- |
| 0x001 | 當作業中的所有檔案都已傳送時產生事件。 |
| 0x002 | 發生錯誤時產生事件。 |
| 0x004 | 停用通知。 |
| 0x008 | 在修改作業或進行傳輸進度時產生事件。 |

## <a name="examples"></a>範例

若要取得名為 *myDownloadJob*之作業的通知旗標：

```
bitsadmin /getnotifyflags myDownloadJob
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [bitsadmin 命令](bitsadmin.md)
