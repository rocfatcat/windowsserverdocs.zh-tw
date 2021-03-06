---
title: nslookup set search
description: Nslookup set 搜尋命令的參考文章，此命令會將 DNS 網域搜尋清單中的網域名稱系統 (DNS) 功能變數名稱寫入要求，直到收到解答為止。
ms.topic: reference
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 91efbb50ab54a920be4c2942db1ea8b9cea71fbe
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637452"
---
# <a name="nslookup-set-search"></a>nslookup set search

將 DNS 網域搜尋清單中的網域名稱系統 (DNS) 功能變數名稱加入要求，直到收到解答為止。 這適用于設定和查閱要求至少包含一段時間，但結尾不是句號的時候。

## <a name="syntax"></a>語法

```
set [no]search
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| --------- | ----------- |
| nosearch | 停止在要求的 DNS 網域搜尋清單中附加網域名稱系統 (DNS) 功能變數名稱。 |
| 搜尋 | 將網域名稱系統附加在要求的 DNS 網域搜尋清單中 (DNS) 功能變數名稱，直到收到解答為止。 這是預設值。 |
| /? | 在命令提示字元顯示說明。 |
| /help | 在命令提示字元顯示說明。 |

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)
