---
title: logman update counter
description: Logman update counter 命令的參考文章，此命令會更新現有的計數器資料收集器屬性。
ms.topic: reference
ms.assetid: 607df6d5-876c-428d-a0b3-f59cb244e2ce
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c164fdaf8e9a22b6072555a893fb6c41c69f177b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640366"
---
# <a name="logman-update-counter"></a>logman update counter

> 適用于： Windows Server (半年通道) 、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

更新現有的計數器資料收集器屬性。

## <a name="syntax"></a>語法

```
logman update counter <[-n] <name>> [options]
```

### <a name="parameters"></a>參數


| 參數 | 描述 |
| --------- | ----------- |
| -s `<computer name>` | 在指定的遠端電腦上執行命令。 |
| -config `<value>` | 指定包含命令選項的設定檔。 |
| [-n] `<name>` | 目標物件的名稱。 |
| -f `<bin|bincirc>` | 指定資料收集器的記錄檔格式。 |
| -[-] u `<user [password]>` | 指定要執行的使用者。 輸入 `*` 密碼會產生密碼提示。 當您在密碼提示字元中輸入密碼時，不會顯示該密碼。 |
| -m `<[start] [stop] [[start] [stop] [...]]>` | 手動啟動或停止的變更，而不是排程的開始或結束時間。 |
| -rf `<[[hh:]mm:]ss>` | 在指定的一段時間內執行資料收集器。 |
| -b `<M/d/yyyy h:mm:ss[AM|PM]>` | 在指定的時間開始收集資料。 |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | 在指定的時間結束資料收集。 |
| -si `<[[hh:]mm:]ss>` | 指定效能計數器資料收集器的取樣間隔。 |
| -o `<path|dsn!log>` | 指定 SQL 資料庫中的輸出記錄檔或 DSN 和記錄集名稱。 |
| -[-] r | 每日在指定的開始和結束時間重複資料收集器。 |
| -[-] a | 附加現有的記錄檔。 |
| -[-] 允許 | 覆寫現有的記錄檔。 |
| -[-] v `<nnnnnn|mmddhhmm>` | 將檔案版本設定資訊附加至記錄檔名稱的結尾。 |
| -[-] rc `<task>` | 每次關閉記錄檔時，執行指定的命令。 |
| -[-] max `<value>` | 最大記錄檔大小（以 MB 為單位）或 SQL 記錄檔的最大記錄數目。 |
| -[-] my.cnf `<[[hh:]mm:]ss>` | 指定時間時，請在指定的時間已過時建立新的檔案。 如果未指定時間，當超過大小上限時，請建立新的檔案。 |
| -y | 針對所有問題回答「是」，而不提示。 |
| -cf `<filename>` | 指定要收集的效能計數器清單。 檔案應包含每行一個效能計數器名稱。 |
| -c `<path [path [ ]]>` | 指定要收集的效能計數器)  (s。 |
| -sc `<value>` | 指定使用效能計數器資料收集器收集的樣本數上限。 |
| /? | 顯示即時線上說明。 |

#### <a name="remarks"></a>備註

- 列出 [-] 時，新增額外的連字號 (-) 會否定選項。

### <a name="examples"></a>範例

若要建立稱為 *perf_log* 的計數器，請使用處理器 (_Total) 計數器類別中的 [% Processor time] 計數器，輸入：

```
logman create counter perf_log -c \Processor(_Total)\% Processor time
```

若要更新名為 *perf_log*的現有計數器、將取樣間隔變更為10、將記錄格式變更為 CSV，以及將版本設定新增至記錄檔名稱的格式為 mmddhhmm，請輸入：

```
logman update counter perf_log -si 10 -f csv -v mmddhhmm
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [logman create counter 命令](logman-create-counter.md)

- [logman 命令](logman.md)
