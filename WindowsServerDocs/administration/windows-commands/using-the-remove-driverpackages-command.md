---
title: 使用移除 DriverPackages 命令
description: '適用於 Windows 命令主題 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a527084b-305e-4d3d-95c3-4f5a5ea0637b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 166602bcb1203f0ecb870ed04888ca0051f16827
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872479"
---
# <a name="using-the-remove-driverpackages-command"></a>使用移除 DriverPackages 命令

>適用於：Windows Server （半年通道），Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012

從伺服器移除驅動程式套件。
## <a name="syntax"></a>語法
```
wdsutil /remove-DriverPackages [/Server:<Server name>] /Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value> ...]
```
## <a name="parameters"></a>參數
|參數|描述|
|-------|--------|
|[/ 伺服器：<Server name>]|指定伺服器的名稱。 這可以是 NetBIOS 名稱或 FQDN。 如果未指定伺服器名稱，則會使用本機伺服器。|
|/ Filtertype:<Filter type>|指定要搜尋的驅動程式套件的屬性。 您可以在單一命令中指定多個屬性。 您也必須指定 **/Operator**並 **/值**使用此選項。<br /><br /><Filter type> 可以是下列其中一項：<br /><br />**PackageId**<br /><br />**PackageName**<br /><br />**PackageEnabled**<br /><br />**Packagedateadded**<br /><br />**PackageInfFilename**<br /><br />**PackageClass**<br /><br />**PackageProvider**<br /><br />**PackageArchitecture**<br /><br />**PackageLocale**<br /><br />**PackageSigned**<br /><br />**PackagedatePublished**<br /><br />**Packageversion**<br /><br />**Driverdescription**<br /><br />**DriverManufacturer**<br /><br />**DriverHardwareId**<br /><br />**DrivercompatibleId**<br /><br />**DriverExcludeId**<br /><br />**DriverGroupId**<br /><br />**DriverGroupName**|
|/Operator:{Equal &#124; NotEqual &#124; GreaterOrEqual &#124; LessOrEqual &#124; Contains}|指定屬性和值之間的關聯性。 您只能指定**Contains**的字串屬性。 您只能指定**GreaterOrEqual**並**LessOrEqual**使用日期和版本的屬性。|
|/ 值：<Value>|指定要搜尋指定的值<attribute>。 您可以指定多個值的單一 **/Filtertype**。 下列清單列出您可以指定每個篩選器的屬性。 如需有關這些屬性的詳細資訊，請參閱 <<c0> [ 驅動程式和封裝屬性](https://go.microsoft.com/fwlink/?LinkId=166895)(https://go.microsoft.com/fwlink/?LinkId=166895)。<br /><br />-PackageId-指定有效的 GUID。 例如: {4d36e972-e325-11ce-bfc1-08002be10318}。<br />-PackageName 指定任何字串值。<br />-PackageEnabled-指定 **[是]** 或是**No**。<br />-Packagedateadded-指定的日期，格式如下：YYYY/MM/DD<br />-PackageInfFilename 指定任何字串值。<br />-PackageClass-指定有效的類別名稱或類別 GUID。 例如: **DiskDrive**， **Net**，或 {4d36e972-e325-11ce-bfc1-08002be10318}。<br />-PackageProvider 指定任何字串值。<br />-PackageArchitecture-指定**x86**， **x64**，或**ia64**。<br />-PckageLocale-指定有效的語言識別碼。 例如： **EN-US**或是**ES-ES**。<br />-PackageSigned-指定 **[是]** 或是**No**。<br />-PackagedatePublished-指定的日期，格式如下：YYYY/MM/DD<br />-Packageversion-以下列格式指定版本： a.b.x.y. 例如: 6.1.0.0<br />-Driverdescription 指定任何字串值。<br />-DriverManufacturer 指定任何字串值。<br />-DriverHardwareId-指定任何字串值。<br />-DrivercompatibleId-指定任何字串值。<br />-DriverExcludeId-指定任何字串值。<br />-DriverGroupId-指定有效的 GUID。 例如: {4d36e972-e325-11ce-bfc1-08002be10318}。<br />-DriverGroupName 指定任何字串值。|
## <a name="BKMK_examples"></a>範例
若要移除封裝，請輸入下列其中一項：
```
wdsutil /verbose /remove-DriverPackages /Server:MyWdsServer
/Filtertype:PackageProvider /Operator:Equal /Value:Name1 /Value:Name2
```
```
wdsutil /remove-DriverPackages /Filtertype:PackageArchitecture /Operator:Equal
/Value:x86 /Value:x64 /Filtertype:PackageEnabled /Operator:Equal /Value:No
```
```
wdsutil /verbose /remove-DriverPackages /Server:MyWdsServer
/Filtertype:Packagedateadded /Operator:LessOrEqual /Value:2008/01/01
```
#### <a name="additional-references"></a>其他參考資料
[命令列語法重點](command-line-syntax-key.md)
[使用移除 DriverPackage 命令](using-the-remove-driverpackage-command.md)