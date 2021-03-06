---
title: Vssadmin 調整大小 shadowstorage
description: Vssadmin 調整大小 shadowstorage 命令的描述。
ms.topic: reference
author: JasonGerend
ms.author: jgerend
ms.date: 03/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0eb9a4096c529b73a87c5a9fb4d6a95b5e655fe3
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "89022832"
---
# <a name="vssadmin-resize-shadowstorage"></a>Vssadmin 調整大小 shadowstorage

> 適用于： Windows 10、Windows 8.1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

調整可用於陰影複製儲存空間的最大儲存空間量。

您可以使用 **MinDiffAreaFileSize** 登錄值來指定可用於陰影複製儲存空間的最小儲存空間量。 如需詳細資訊，請參閱 [MinDiffAreaFileSize](/windows/win32/backup/registry-keys-for-backup-and-restore#mindiffareafilesize)。

> [!WARNING]
> 調整儲存體關聯的大小可能會導致陰影複製消失。

## <a name="syntax"></a>語法

```cmd
vssadmin resize shadowstorage /for=<ForVolumeSpec> /on=<OnVolumeSpec> [/maxsize=<MaxSizeSpec>]
```

### <a name="parameters"></a>參數

|參數|描述|
|---|---|
`/for=<ForVolumeSpec>`  | 指定要調整大小之最大儲存空間量的磁片區。
`/on=<OnVolumeSpec>` | 指定存放磁片區。
`[/maxsize=<MaxSizeSpec>]` |  指定可用於儲存陰影複製的最大空間量。 如果未針對/maxsize 指定任何值，則可使用的儲存空間量沒有限制。  <br> <br> MaxSizeSpec 值必須是 1 MB 或更大的值，且必須以下列其中一個單位表示： KB、MB、GB、TB、PB 或 EB。 如果未指定 unit，MaxSizeSpec 預設會使用 bytes。

## <a name="examples"></a>範例

```cmd
vssadmin Resize ShadowStorage /For=C: /On=D: /MaxSize=900MB
vssadmin Resize ShadowStorage /For=C: /On=D: /MaxSize=UNBOUNDED
vssadmin Resize ShadowStorage /For=C: /On=C: /MaxSize=20%
```

## <a name="additional-references"></a>其他參考資料

* [命令列語法索引鍵](./command-line-syntax-key.md)
* [Vssadmin](vssadmin.md)
