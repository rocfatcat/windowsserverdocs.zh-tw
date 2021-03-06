---
title: bootcfg
description: 適用于 bootcfg 命令的參考文章，可設定、查詢或變更 Boot.ini 的檔案設定。
ms.topic: reference
ms.assetid: 3deb354c-5717-4066-bc79-b9323d559e44
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6f187015ab3c8cba18e34601faebc1637ecf7896
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630092"
---
# <a name="bootcfg"></a>bootcfg

> 適用于： Windows Server (半年通道) 、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

設定、查詢或變更 Boot.ini 檔案設定。

## <a name="syntax"></a>語法

```
bootcfg <parameter> [arguments...]
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| --------- | ----------- |
| [bootcfg addsw](bootcfg-addsw.md) | 新增指定作業系統專案的作業系統載入選項。 |
| [bootcfg copy](bootcfg-copy.md) | 建立現有開機專案的複本，您可以在其中新增命令列選項。 |
| [bootcfg dbg1394](bootcfg-dbg1394.md) | 針對指定的作業系統專案設定1394埠的偵錯工具。 |
| [bootcfg debug](bootcfg-debug.md) | 新增或變更指定之作業系統專案的偵錯工具設定。 |
| [bootcfg default](bootcfg-default.md) | 指定要指定為預設值的作業系統專案。 |
| [bootcfg delete](bootcfg-delete.md) | 在 Boot.ini 檔案的 [作業系統] 區段中刪除作業系統專案。 |
| [bootcfg ems](bootcfg-ems.md) | 可讓使用者新增或變更將緊急管理服務主控台重新導向至遠端電腦的設定。 |
| [bootcfg query](bootcfg-query.md) | 查詢並顯示 Boot.ini 中的 [開機載入器] 和 [作業系統] 區段專案。 |
| [bootcfg raw](bootcfg-raw.md) | 在 Boot.ini 檔案的 [作業系統] 區段中，將指定為字串的作業系統載入選項新增至作業系統專案。 |
| [bootcfg rmsw](bootcfg-rmsw.md) | 移除指定作業系統專案的作業系統載入選項。 |
| [bootcfg timeout](bootcfg-timeout.md) | 變更作業系統超時值。 |
