---
title: bitsadmin gethelpertokenflags
description: Bitsadmin gethelpertokenflags 命令的參考文章，它會傳回與 BITS 傳送工作相關聯之 helper 權杖的使用旗標。
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 244dee15e201c877bdf3c17a219e190bee9a5821
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632054"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitsadmin gethelpertokenflags

 [helper token](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)   傳回與 BITS 傳送工作相關聯之 helper 權杖的使用旗標。

> [!NOTE]
> BITS 3.0 及更早版本不支援此命令。

## <a name="syntax"></a>語法

```
bitsadmin /gethelpertokenflags <job>
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| -------------- | -------------- |
| 作業 | 作業的顯示名稱或 GUID。 |

### <a name="remarks"></a>備註

可能的傳回值，包括：

- **0x0001.** 協助程式權杖可用來開啟上傳作業的本機檔案、建立或重新命名下載作業的暫存檔案，或建立或重新命名上傳回復作業的回復檔案。

- **0x0002.** 協助程式權杖可用來開啟伺服器訊息區的遠端檔案 (SMB) 上傳或下載作業，或回應 HTTP 伺服器或 proxy 挑戰的隱含 NTLM 或 Kerberos 認證。 您必須呼叫  `/SetCredentialsJob TargetScheme NULL NULL`   以允許透過 HTTP 傳送認證。

## <a name="examples"></a>範例

若要取得與名為 *myDownloadJob*之 BITS 傳送工作相關聯之協助程式權杖的使用旗標：

```
bitsadmin /gethelpertokenflags myDownloadJob
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [bitsadmin 命令](bitsadmin.md)
