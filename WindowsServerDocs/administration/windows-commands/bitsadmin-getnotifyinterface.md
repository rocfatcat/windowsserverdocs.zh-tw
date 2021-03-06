---
title: bitsadmin getnotifyinterface
description: Bitsadmin getnotifyinterface 命令的參考文章，可判斷其他程式是否已針對指定的作業註冊 COM 回呼介面。
ms.topic: reference
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 563cdf103ce60fc13f0455caea98e30f9e2e03e4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631892"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

判斷其他程式是否已針對指定的作業， (通知介面) 註冊 COM 回呼介面。

## <a name="syntax"></a>語法

```
bitsadmin /getnotifyinterface <job>
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| -------------- | -------------- |
| 作業 | 作業的顯示名稱或 GUID。 |

#### <a name="output"></a>輸出

此命令的輸出會顯示、 **已註冊或已** 取消 **註冊**。

> [!NOTE]
> 無法判斷註冊回呼介面的程式。

## <a name="examples"></a>範例

若要取得名為 *myDownloadJob*之作業的通知介面：

```
bitsadmin /getnotifyinterface myDownloadJob
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [bitsadmin 命令](bitsadmin.md)
