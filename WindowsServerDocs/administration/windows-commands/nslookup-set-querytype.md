---
title: nslookup set querytype
description: Nslookup set querytype 命令的參考文章，此命令會變更查詢的資源記錄類型。
ms.topic: reference
ms.assetid: 5af54ac5-fc1a-4af6-977b-f8e97c8eba90
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3c40d9002b170f411992fc48f65d0114524d92e6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628044"
---
# <a name="nslookup-set-querytype"></a>nslookup set querytype

> 適用于： Windows Server (半年通道) 、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

變更查詢的資源記錄類型。 如需資源記錄類型的詳細資訊，請參閱 [ (Rfc 的批註要求) 1035](https://tools.ietf.org/html/rfc1035)。

> [!NOTE]
> 此命令與 [nslookup set type](nslookup-set-type.md) 命令相同。

## <a name="syntax"></a>語法

```
set querytype=<resourcerecordtype>
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| --------- | ----------- |
| `<resourcerecordtype>` | 指定 DNS 資源記錄類型。 預設的資源記錄類型是，但您可以使用下列任何 **一個**值：<ul><li>**答：** 指定電腦的 IP 位址。</li><li>**任何：** 指定電腦的 IP 位址。</li><li>**CNAME：** 指定別名的正式名稱。</li><li>**GID** 指定組名的群組識別碼。</li><li>**HINFO：** 指定電腦的 CPU 和類型的作業系統。</li><li>**MB：** 指定信箱功能變數名稱。</li><li>**MG：** 指定郵件群組成員。</li><li>**MINFO：** 指定信箱或郵寄清單資訊。</li><li>**MR：** 指定郵件重新命名的功能變數名稱。</li><li>**MX：** 指定郵件交換。</li><li>**NS：** 指定命名區域的 DNS 名稱伺服器。</li><li>**PTR：** 如果查詢是 IP 位址，則指定電腦名稱稱;否則，指定其他資訊的指標。</li><li>**SOA：** 指定 DNS 區域的起始授權單位。</li><li>**TXT：** 指定文字資訊。</li><li>**UID：** 指定使用者識別碼。</li><li>**UINFO：** 指定使用者資訊。</li><li>**WKS：** 描述知名的服務。</li></ul> |
| /? | 在命令提示字元顯示說明。 |
| /help | 在命令提示字元顯示說明。 |

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [nslookup set type](nslookup-set-type.md)
