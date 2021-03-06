---
title: AllDevices
description: AllDevices 的參考文章，會顯示所有預先設置電腦的 Windows 部署服務屬性。
ms.topic: reference
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5087b67c15b3969085d3c8c66072f09396165614
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89621978"
---
# <a name="get-alldevices"></a>AllDevices

> 適用于： Windows Server (半年通道) 、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

顯示所有預先設置電腦的 Windows 部署服務屬性。 預先設置的電腦是指已連結至 active directory 網域服務中電腦帳戶的實體電腦。

## <a name="syntax"></a>語法
```
wdsutil [Options] /Get-AllDevices [/forest:{Yes | No}] [/ReferralServer:<Server name>]
```
### <a name="parameters"></a>參數
|參數|描述|
|-------|--------|
|[/forest： {Yes &#124; No}]|指定 Windows 部署服務是否應傳回整個樹系或本機網域中的電腦。 預設設定為 [ **否**]，表示只會傳回本機網域中的電腦。|
|[/ReferralServer： <Server name> ]|只傳回針對指定伺服器預先設置的電腦。|
## <a name="examples"></a>範例
若要查看所有電腦，請輸入下列其中一項：
```
wdsutil /Get-AllDevices
wdsutil /verbose /Get-AllDevices /forest:Yes /ReferralServer:MyWDSServer
```
## <a name="additional-references"></a>其他參考資料
- [命令列語法索引鍵](command-line-syntax-key.md) 
[子命令：設定裝置](subcommand-set-device.md) 
[使用 [新增裝置] 命令](using-the-add-device-command.md) 
[使用取得裝置命令](using-the-get-device-command.md)
