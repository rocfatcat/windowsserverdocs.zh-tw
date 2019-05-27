---
title: bitsadmin gethelpertokenflags
description: 適用於 Windows 命令主題**bitsadmin gethelpertokenflags** -傳回的 BITS 傳送工作相關聯的協助程式權杖的使用方式旗標。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: e5665ed4670891dcbecd56215342f3d94e1ed753
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885789"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitsadmin gethelpertokenflags

傳回的使用方式旗標 [協助程式的語彙基元](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs) BITS 傳送工作相關聯。

**3.0 版和更早版本的位元**: 未支援。

## <a name="syntax"></a>語法

```
bitsadmin /GetHelperTokenFlags <Job>
```

## <a name="parameters"></a>參數

|參數|描述|
|---------|-----------|
|Job|作業的顯示名稱或 GUID|

## <a name="remarks"></a>備註

可能的傳回值包括下列項目。

- 0x0001。 協助程式權杖用來開啟 上傳作業，若要建立或重新命名的暫存檔案的下載工作，或若要建立或重新命名的上傳-回覆作業的回覆檔案的本機檔案。
- 0x0002。 協助程式權杖用來開啟遠端檔案伺服器訊息區塊 (SMB) 上傳或下載作業，或在回應 HTTP 伺服器或 proxy 要求隱含的 NTLM 或 Kerberos 認證。 您必須呼叫 SetCredentialsJob TargetScheme NULL NULL，以允許透過 HTTP 傳送的認證。

#### <a name="additional-references"></a>其他參考資料

[命令列語法關鍵](command-line-syntax-key.md)