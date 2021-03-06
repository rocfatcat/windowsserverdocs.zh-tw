---
title: create volume stripe
description: 建立磁片區 stripe 命令的參考文章，此命令會使用兩個或多個指定的動態磁碟來建立等量磁片區。
ms.topic: reference
ms.assetid: 20dce735-5f7c-4f83-a580-d087e2913a00
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b8e2265a264b96a0c966a7548b1323c469392af3
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89629023"
---
# <a name="create-volume-stripe"></a>create volume stripe

> 適用于： Windows Server (半年通道) 、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

使用兩個或多個指定的動態磁碟來建立等量磁片區。 建立磁碟區之後，焦點會自動移到新磁碟區。

## <a name="syntax"></a>語法

```
create volume stripe [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr]
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| --------- |  -----------|
| 大小 =`<n>` | 磁碟區佔據每個磁碟上的磁碟空間 (以 MB 為單位)。 如果未指定大小，則新磁碟區會佔用最小磁碟上剩餘的可用空間，及每個後續磁碟上等量的空間。 |
| 磁片 =`<n>,<n>[,<n>,...]` | 建立等量磁片區的動態磁碟。 您至少需要兩個動態磁碟來建立一個等量磁碟區。 `size=<n>`在每個磁片上都會配置等於的空間量。 |
| align =`<n>` | 將所有磁片區範圍對齊到最接近的對齊界限。 通常會與硬體 RAID 邏輯單元編號搭配使用 (LUN) 陣列以改善效能。 `<n>` 這是從磁片開頭到最接近對齊界限的 kb (KB) 數目。 |
| noerr | 僅適合執行指令。 遇到錯誤時，DiskPart 會像沒有發生錯誤一般繼續處理命令。 如果沒有這個參數，錯誤會導致 DiskPart 結束，並產生錯誤碼。 |

## <a name="examples"></a>範例

若要建立大小為 1000 mb 的等量磁片區，請在磁片1和2上輸入：

```
create volume stripe size=1000 disk=1,2
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [create 命令](create.md)
