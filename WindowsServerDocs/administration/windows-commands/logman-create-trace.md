---
title: logman create trace
description: Logman create trace 命令的參考文章，此命令會建立事件追蹤資料收集器。
ms.topic: reference
ms.assetid: 1b4dfecd-6f56-4c51-b622-c2054b4aabd7
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 31a286d90873d76ad604de27ac94a0668939d8da
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622751"
---
# <a name="logman-create-trace"></a>logman create trace

> 適用于： Windows Server (半年通道) 、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

建立事件追蹤資料收集器。

## <a name="syntax"></a>語法

```
logman create trace <[-n] <name>> [options]
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| --------- | ----------- |
| -s `<computer name>` | 在指定的遠端電腦上執行命令。 |
| -config `<value>` | 指定包含命令選項的設定檔。 |
| -ets | 直接將命令傳送至事件追蹤會話，而不儲存或排程。 |
| [-n] `<name>` | 目標物件的名稱。 |
| -f `<bin|bincirc>` | 指定資料收集器的記錄檔格式。 |
| -[-] u `<user [password]>` | 指定要執行的使用者。 輸入 `*` 密碼會產生密碼提示。 當您在密碼提示字元中輸入密碼時，不會顯示該密碼。 |
| -m `<[start] [stop] [[start] [stop] [...]]>` | 手動啟動或停止的變更，而不是排程的開始或結束時間。 |
| -rf `<[[hh:]mm:]ss>` | 在指定的一段時間內執行資料收集器。 |
| -b `<M/d/yyyy h:mm:ss[AM|PM]>` | 在指定的時間開始收集資料。 |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | 在指定的時間結束資料收集。 |
| -o `<path|dsn!log>` | 指定 SQL 資料庫中的輸出記錄檔或 DSN 和記錄集名稱。 |
| -[-] r | 每日在指定的開始和結束時間重複資料收集器。 |
| -[-] a | 附加現有的記錄檔。 |
| -[-] 允許 | 覆寫現有的記錄檔。 |
| -[-] v `<nnnnnn|mmddhhmm>` | 將檔案版本設定資訊附加至記錄檔名稱的結尾。 |
| -[-] rc `<task>` | 每次關閉記錄檔時，執行指定的命令。 |
| -[-] max `<value>` | 最大記錄檔大小（以 MB 為單位）或 SQL 記錄檔的最大記錄數目。 |
| -[-] my.cnf `<[[hh:]mm:]ss>` | 當指定時間時，會在經過指定的時間時建立新的檔案。 如果未指定時間，當超過大小上限時，就會建立新的檔案。 |
| -y | 針對所有問題回答「是」，而不提示。 |
| -ct `<perf|system|cycle>` | 指定事件追蹤會話的頻率類型。 |
| -ln `<logger_name>` | 指定事件追蹤會話的記錄器名稱。 |
| -ft `<[[hh:]mm:]ss>` | 指定事件追蹤會話清除計時器。 |
| -[-] p `<provider [flags [level]]>` | 指定要啟用的單一事件追蹤提供者。 |
| -pf `<filename>` | 指定列出多個要啟用之事件追蹤提供者的檔案。 檔案應該是一個文字檔，每行包含一個提供者。 |
| -[-] rt | 以即時模式執行事件追蹤會話。 |
| -[-] ul | 在使用者中執行事件追蹤會話。 |
| -bs `<value>` | 指定事件追蹤會話緩衝區大小（以 kb 為單位）。 |
| -nb `<min max>` | 指定事件追蹤會話緩衝區的數目。 |
| -模式 `<globalsequence|localsequence|pagedmemory>` | 指定事件追蹤會話記錄器模式，包括：<ul><li>**Globalsequence** -指定事件追蹤程式會將序號新增至它所收到的每個事件，而不論哪個追蹤會話收到事件。</li><li>**Localsequence** -指定事件追蹤程式為在特定追蹤會話所收到的事件新增序號。 使用這個選項時，重複的序號可以存在於所有的會話中，但在每個追蹤會話中都是唯一的。</li><li>**Pagedmemory** -指定事件追蹤使用分頁記憶體，而非預設的非分頁式記憶體集區來進行內部緩衝區配置。</li></ul> |
| /? | 顯示即時線上說明。 |

#### <a name="remarks"></a>備註

- 列出 [-] 時，新增額外的連字號 (-) 會否定選項。

### <a name="examples"></a>範例

若要建立名為 *trace_log*的事件追蹤資料收集器，並使用不超過16個以上的緩衝區，256而且每個緩衝區的大小為 64 kb，將結果放在 c:\logfile 中，請輸入：

```
logman create trace trace_log -nb 16 256 -bs 64 -o c:\logfile
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [logman 更新追蹤命令](logman-update-trace.md)

- [logman 命令](logman.md)
