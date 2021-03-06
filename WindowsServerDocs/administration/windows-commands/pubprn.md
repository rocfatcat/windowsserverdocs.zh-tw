---
title: pubprn
description: Pubprn 命令的參考文章，此命令會將印表機發佈至 Active Directory Domain Services。
ms.topic: reference
ms.assetid: 0bc7f7e3-84e1-4359-b477-7b1a1a0bd639
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 36366e91f390ee8afb4884e31951cd5efde9251a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640601"
---
# <a name="pubprn"></a>pubprn

> 適用于： Windows Server (半年通道) 、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

將印表機發佈至 Active Directory Domain Services。 此命令是位於目錄中的 Visual Basic 腳本 `%WINdir%\System32\printing_Admin_Scripts\<language>` 。 若要在命令提示字元中使用此命令，請輸入 **cscript** ，後面接著 pubprn 檔案的完整路徑，或將目錄變更為適當的資料夾。 例如：`cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn`。

## <a name="syntax"></a>語法

```
cscript pubprn {<servername> | <UNCprinterpath>} LDAP://CN=<container>,DC=<container>
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|--|--|
| `<servername>` | 指定裝載您要發佈之印表機的 Windows server 名稱。 如果您未指定電腦，則會使用本機電腦。 |
| `<UNCprinterpath>` | 通用命名慣例 (UNC) 路徑指向您想要發佈的共用印表機。 |
| `LDAP://CN=<Container>,DC=<Container>` | 指定要在其中發行印表機的 Active Directory Domain Services 容器的路徑。 |
| /? | 在命令提示字元顯示說明。 |

#### <a name="remarks"></a>備註

- 如果您提供的資訊包含空格，請使用引號括住文字 (例如「電腦名稱稱」 ) 。

### <a name="examples"></a>範例

若要將 Server1 電腦上的所有印表機發佈 \\ 至 MyDomain.company.com 網域中的 MyContainer 容器，請輸入：

```
cscript pubprn Server1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

若要將 \Server1 伺服器上的 Laserprinter1 印表機發佈 \\ 到 MyDomain.company.com 網域中的 MyContainer 容器，請輸入：

```
cscript pubprn \\Server1\Laserprinter1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [列印命令參考資料](print-command-reference.md)
