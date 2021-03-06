---
title: net print
description: Net print 命令的參考文章。 此命令已被取代，而且在未來的 Windows 版本中不保證會受到支援。
ms.topic: reference
ms.assetid: f59b2015-4698-415d-9a74-09566c466f40
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 10e153da203e0e11c1560417f363e17b6b18aaa7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637968"
---
# <a name="net-print"></a>net print

> [!IMPORTANT]
> 此命令已被取代。 不過，您可以使用 [prnjobs 命令](prnjobs.md)來執行許多相同的工作， [Windows Management Instrumentation (WMI) ](/windows/win32/wmisdk/wmi-start-page)、 [Powershell 中的 printmanagement.msc](/powershell/module/printmanagement)，或 [IT 專業人員的腳本資源](https://gallery.technet.microsoft.com/ScriptCenter/site/search?f%5B0%5D.Type=RootCategory&f%5B0%5D.Value=printing&f%5B0%5D.Text=Printing)。

顯示指定之印表機佇列或指定的列印工作的相關資訊，或控制指定的列印工作。

## <a name="syntax"></a>語法

```
net print {\\<computername>\<sharename> | \\<computername> <jobnumber> [/hold | /release | /delete]} [help]
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| ---------- | ----------- |
| `\\<computername>\<sharename>` | 依名稱指定 (，) 您要顯示資訊的電腦和列印佇列。 |
| `\\<computername>` | 依名稱指定 (，) 裝載您要控制之列印工作的電腦。 如果您未指定電腦，則會假設為本機電腦。 需要 `<jobnumber>` 參數。 |
| `<jobnumber>` | 指定您想要控制的列印工作數目。 此數位是由裝載列印工作傳送之列印佇列的電腦所指派。 當電腦將數位指派給列印工作之後，該數位就不會指派給該電腦所裝載之任何佇列中的任何其他列印工作。 使用參數時為必要 `\\<computername>` 。 |
| `[/hold | /release | /delete]` | 指定要對列印工作採取的動作。 如果您指定工作編號，但未指定任何動作，則會顯示列印工作的相關資訊。<ul><li>**/hold** -延遲工作，讓其他列印工作略過它，直到釋放為止。</li><li>**/release** -釋放已延遲的列印工作。</li><li>**/delete** -從列印佇列中移除列印工作。</li></ul> |
| help | 在命令提示字元顯示說明。 |

#### <a name="remarks"></a>備註

- 此 `net print\\<computername>` 命令會顯示共用印表機佇列中列印工作的相關資訊。 以下是名為「 *鐳射*」之共用印表機的佇列中所有列印工作的報表範例：

    ```
    printers at \\PRODUCTION
    Name              Job #      Size      Status
    -----------------------------
    LASER Queue       3 jobs               *printer active*
    USER1          84        93844      printing
    USER2          85        12555      Waiting
    USER3          86        10222      Waiting
    ```

- 以下是列印工作的報表範例：

    ```
    Job #            35
    Status           Waiting
    Size             3096
    remark
    Submitting user  USER2
    Notify           USER2
    Job data type
    Job parameters
    additional info
    ```

### <a name="examples"></a>範例

若要在* \\ 實際*執行電腦上列出*Dotmatrix*列印佇列的內容，請輸入：

```
net print \\Production\Dotmatrix
```

若要在* \\ 實際*執行電腦上顯示作業編號*35*的相關資訊，請輸入：

```
net print \\Production 35
```

若要在* \\ 實際*執行電腦上延遲作業編號*263* ，請輸入：

```
net print \\Production 263 /hold
```

若要在* \\ 實際*執行電腦上釋放作業編號*263* ，請輸入：

```
net print \\Production 263 /release
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [列印命令參考](print-command-reference.md)

- [prnjobs 命令](prnjobs.md)

- [Windows Management Instrumentation (WMI)](/windows/win32/wmisdk/wmi-start-page)

- [Powershell 中的 Printmanagement.msc](/powershell/module/printmanagement)

- [IT 專業人員的腳本資源](https://gallery.technet.microsoft.com/ScriptCenter/site/search?f%5B0%5D.Type=RootCategory&f%5B0%5D.Value=printing&f%5B0%5D.Text=Printing)
