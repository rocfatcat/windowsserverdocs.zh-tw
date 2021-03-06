---
title: reset
description: 重設命令的參考文章，會將 DiskShadow.exe 重設為預設狀態。
ms.topic: reference
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 84f4aedee746e642e59a09055c3994160f503afa
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626887"
---
# <a name="reset"></a>reset

將 DiskShadow.exe 重設為預設狀態。 此命令特別適用于分隔複合 DiskShadow 作業，例如 **建立**、匯 **入**、 **備份**或 **還原**。

> [!重要事項：執行此命令之後，您將會遺失命令的狀態資訊，例如 **add**、 **set**、 **load**或 **writer**。 此命令也會釋放 IVssBackupComponent 介面，並失去非持續性陰影複製。

## <a name="syntax"></a>語法

```
reset
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [create 命令](create.md)

- [匯入命令](import_1.md)

- [backup 命令](begin-backup.md)

- [restore 命令](begin-restore.md)

- [新增命令](add.md)

- [set 命令](set_2.md)

- [載入命令](reg-load.md)

- [寫入器命令](writer.md)
