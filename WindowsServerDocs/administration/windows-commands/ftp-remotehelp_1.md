---
title: ftp remotehelp
description: Ftp remotehelp 命令的參考文章，此命令會顯示遠端命令的說明。
ms.topic: reference
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c91fda83ea988f79237b27f6df6bd6062748e37c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639378"
---
# <a name="ftp-remotehelp"></a>ftp remotehelp

> 適用于： Windows Server (半年通道) 、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

顯示遠端命令的說明。

## <a name="syntax"></a>語法

```
remotehelp [<command>]
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| ------- | -------- |
| `[<command>]` | 指定您想要協助的命令名稱。 如果 `<command>` 未指定，此命令會顯示所有遠端命令的清單。 您也可以使用 [ftp 引號](ftp-quote.md) 或 [ftp 常](ftp-literal_1.md)值來執行遠端命令。 |

### <a name="examples"></a>範例

若要顯示遠端命令的清單，請輸入：

```
remotehelp
```

若要顯示 [ *操作遠端] 命令的語法* ，請輸入：

```
remotehelp feat
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [ftp quote](ftp-quote.md)

- [ftp literal](ftp-literal_1.md)

- [其他 FTP 指導方針](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
