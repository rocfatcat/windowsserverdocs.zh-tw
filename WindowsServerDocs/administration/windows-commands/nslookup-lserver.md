---
title: nslookup lserver
description: '適用於 Windows 命令主題 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0c4e1ed4697666062bb90f4a9c65054a3dd73661
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848049"
---
# <a name="nslookup-lserver"></a>nslookup lserver

>適用於：Windows Server （半年通道），Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012

變更指定的網域名稱系統 (DNS) 網域的預設伺服器。
## <a name="syntax"></a>語法
```
lserver <DNSDomain> 
```
## <a name="parameters"></a>參數
|參數|描述|
|-------|--------|
|<DNSDomain>|指定新的 DNS 網域的預設伺服器。|
|{help &#124; ?}|顯示的簡短摘要**nslookup**子命令。|
## <a name="remarks"></a>備註
-   **Lserver**命令會使用初始伺服器查詢指定的 DNS 網域的相關資訊。 這是相對於**server**命令，這個命令會使用目前的預設伺服器。
## <a name="additional-references"></a>其他參考資料
[命令列語法重點](command-line-syntax-key.md)
[nslookup 伺服器](nslookup-server.md)