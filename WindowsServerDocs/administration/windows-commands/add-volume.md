---
title: add volume
description: '[新增磁片區] 命令的參考文章，此命令會將磁片區新增至陰影複製集，也就是要陰影複製的磁片區集合。'
ms.topic: reference
ms.assetid: b7d4d35d-8bda-46d2-8df5-eb598cecaaba
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2a1dc6f00ebc497e9276d1f3b5a74a1f1a10dbfc
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633547"
---
# <a name="add-volume"></a>add volume

將磁片區新增至陰影複製集，這是要陰影複製的磁片區集合。 建立陰影複製時，環境變數會將別名連結至陰影識別碼，讓別名可以用來編寫腳本。

磁片區會一次新增一個。 每次新增磁片區時，就會進行檢查以確定 VSS 支援該磁片區的陰影複製建立。 稍後使用 **set coNtext** 命令可能會使此檢查失效。

此命令是建立陰影複製的必要命令。 如果使用時不含參數，請在命令提示字元中 **新增磁片** 區顯示說明。

## <a name="syntax"></a>語法

```
add volume <volume> [provider <providerid>]
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| --------- | ----------- |
| `<volume>` | 指定要新增至陰影複製集的磁片區。 至少需要一個磁片區才能建立陰影複製。 |
| `[provider \<providerid>]` | 指定用於建立陰影複製之已註冊提供者的提供者識別碼。 如果未指定 **provider** ，則會使用預設提供者。 |

## <a name="examples"></a>範例

若要查看目前已註冊的提供者清單，請在 `diskshadow>` 提示中輸入：

```
list providers
```

下列輸出會顯示預設將使用的單一提供者：

```
* ProviderID: {b5946137-7b9f-4925-af80-51abd60b20d5}
        Type: [1] VSS_PROV_SYSTEM
        Name: Microsoft Software Shadow Copy provider 1.0
        Version: 1.0.0.7
        CLSID: {65ee1dba-8ff4-4a58-ac1c-3470ee2f376a}
1 provider registered.
```

若要將磁片磁碟機 C：新增至陰影複製集，並指派名為 *系統 1*的別名，請輸入：

```
add volume c: alias System1
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [設定內容命令](set-context.md)
