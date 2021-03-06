---
title: auditpol clear
description: Auditpol clear 命令的參考文章會刪除所有使用者的每一使用者稽核原則，重設 (會停用所有子類別的系統稽核原則) ，並將所有的審核選項設定為停用。
ms.topic: reference
ms.assetid: 05bfa218-2434-4ad1-b33c-e6fcfb2b4f67
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1858b2ccc870b459ee864c5d135934f494d4aab6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633227"
---
# <a name="auditpol-clear"></a>auditpol clear

> 適用于： Windows Server (半年通道) 、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

刪除所有使用者的每一使用者稽核原則，重設 (會停用所有子類別的系統稽核原則) ，並將所有審核選項設定為停用。

若要對*每個使用者*和*系統*策略執行*明確*作業，您必須擁有安全描述項中該物件集的 [**寫入**] 或 [**完全控制**] 許可權。 如果您有 [**管理審核和安全性記錄**檔 (SeSecurityPrivilege) 使用者權限，也可以執行*清除*作業。 不過，此許可權可讓您不需要執行整體 *明確* 作業的額外存取權。

## <a name="syntax"></a>語法

```
auditpol /clear [/y]
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| ----------- | --------------- |
| /y | 抑制提示以確認是否應該清除所有稽核原則設定。 |
| /? | 在命令提示字元顯示說明。 |

## <a name="examples"></a>範例

若要刪除所有使用者的每一使用者稽核原則，請重設 (停用所有子類別的系統稽核原則) ，並將所有稽核原則設定設為 [停用]，請在確認提示輸入：

```
auditpol /clear
```

若要刪除所有使用者的每一使用者稽核原則，請重設所有子類別的系統稽核原則設定，並將所有稽核原則設定設為 [停用]，而不需要確認提示，請輸入：

```
auditpol /clear /y
```

> [!NOTE]
> 使用腳本執行這項作業時，上述範例會很有用。

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [auditpol 命令](auditpol.md)
