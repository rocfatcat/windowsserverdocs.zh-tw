---
title: ImageGroup
description: ImageGroup 的參考文章，可取得映射群組和其中影像的相關資訊。
ms.topic: reference
ms.assetid: 0fc25aca-a529-44ee-bc8e-96bc8affb458
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c135072be3ff8ccf0993ed72ddf8f079f1d88c05
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89638089"
---
# <a name="get-imagegroup"></a>ImageGroup

> 適用于： Windows Server (半年通道) 、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

抓取影像群組和其內影像的相關資訊。

## <a name="syntax"></a>語法
```
wdsutil [Options] /Get-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>參數
|參數|描述|
|-------|--------|
mediaGroup:<Image group name>|指定映射群組的名稱。|
|[/Server： <Server name> ]|指定伺服器的名稱。 這可以是 NetBIOS 名稱或完整功能變數名稱 (FQDN) 。 如果未指定伺服器名稱，則會使用本機伺服器。|
|[/detailed]|傳回每個影像的影像中繼資料。 如果未使用此參數，預設行為是只傳回映射名稱、描述和檔案名。|
## <a name="examples"></a>範例
若要查看映射群組的相關資訊，請輸入：
```
wdsutil /Get-ImageGroumediaGroup:ImageGroup1
```
若要查看包含中繼資料的資訊，請輸入：
```
wdsutil /verbose /Get-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>其他參考資料
- [命令列語法索引鍵](command-line-syntax-key.md) 
[使用 ImageGroup 命令](using-the-add-imagegroup-command.md) 
[使用 AllImageGroups 命令](using-the-get-allimagegroups-command.md) 
[使用 ImageGroup 命令](using-the-remove-imagegroup-command.md) 
[子命令： set-ImageGroup](subcommand-set-imagegroup.md)
