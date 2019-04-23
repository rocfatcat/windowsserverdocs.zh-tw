---
title: bde 管理鎖定
description: '適用於 Windows 命令主題 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b8858e61-3a7e-4d03-8c98-5c09853f35e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2b2f4971c0b4a1057d3206c5ead82bf27dfa9b8d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821129"
---
# <a name="manage-bde-lock"></a>管理 bde： 鎖定



鎖定受 BitLocker 保護的磁碟機，防止存取，除非提供解除鎖定金鑰。 如需如何使用此命令的範例，請參閱[範例](#BKMK_Examples)。

## <a name="syntax"></a>語法

```
manage-bde -lock [<Drive>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>參數

|參數|描述|
|---------|-----------|
|\<Drive>|表示磁碟機代號，後面接著冒號。|
|-computername|指定 bde.exe 用以修改不同的電腦上的 BitLocker 保護。 您也可以使用 **-cn**為此命令縮寫版。|
|\<名稱 >|表示要修改 BitLocker 保護之電腦的名稱。 可接受的值包括電腦的 NetBIOS 名稱和電腦的 IP 位址。|
|-? 或 /？|顯示在命令提示字元中，簡短說明。|
|-help 或-h|顯示在命令提示字元完成說明。|

## <a name="BKMK_Examples"></a>範例

下列範例說明如何利用 **-鎖定**命令，以鎖定資料磁碟機 d。
```
manage-bde –lock D:
```

#### <a name="additional-references"></a>其他參考資料

-   [命令列語法關鍵](command-line-syntax-key.md)
-   [管理 bde](manage-bde.md)