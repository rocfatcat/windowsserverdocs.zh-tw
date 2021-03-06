---
title: Scwcmd 復原
description: '* * * * 的參考文章'
ms.topic: reference
ms.assetid: 4fd9f89b-0420-420a-ad20-4a328636b1e7
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2db6e0aa85deb2ab999a50d1f2ed9cb311db9da0
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636984"
---
# <a name="scwcmd-rollback"></a>Scwcmd: rollback

> 適用于： Windows Server 2012 R2、Windows Server 2012

套用可用的最新復原原則，然後刪除該復原原則。

## <a name="syntax"></a>語法

```
scwcmd rollback /m:<ComputerName> [/u:<UserName>] [/pw:<Password>]
```

#### <a name="parameters"></a>參數

|參數|描述|
|---------|-----------|
|一樣\<ComputerName>|指定應執行復原操作之電腦的 NetBIOS 名稱、DNS 名稱或 IP 位址。|
|u\<UserName>|指定執行遠端回復時要使用的其他使用者帳戶。 預設值是登入的使用者。|
|/pw\<Password>|指定執行遠端回復時要使用的替代使用者認證。 預設值是登入的使用者。|
|/?|在命令提示字元顯示說明。|

## <a name="remarks"></a>備註

Scwcmd.exe 只能在執行 Windows Server 2008 R2、Windows Server 2008 或 Windows Server 2003 的電腦上使用。

## <a name="examples"></a>範例

若要在位於 IP 位址172.16.0.0 的電腦上復原安全性原則，請輸入：
```
scwcmd rollback /m:172.16.0.0
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)