---
title: bitsadmin 快取與資訊
description: Bitsadmin 快取的 Windows 命令主題**和 info** -傾印特定的快取專案。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11963ff5640ef30e597e5e802778aff121c0efb3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381974"
---
# <a name="bitsadmin-cache-and-info"></a>bitsadmin 快取與資訊



傾印特定的快取專案。

## <a name="syntax"></a>語法

```
bitsadmin /Cache /Info RecordID [/Verbose] 
```

## <a name="parameters"></a>參數

|參數|描述|
|---------|-----------|
|RecordID|與快取專案相關聯的 GUID。|

## <a name="BKMK_examples"></a>典型

下列範例會傾印具有 {6511FB02-E195-40A2-B595-E8E2F8F47702} RecordID 的快取專案。
```
C:\>bitsadmin /Cache /Info {6511FB02-E195-40A2-B595-E8E2F8F47702} 
```

#### <a name="additional-references"></a>其他參考資料

[命令列語法關鍵](command-line-syntax-key.md)