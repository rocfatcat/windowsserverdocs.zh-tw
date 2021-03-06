---
title: systeminfo
description: Systeminfo 的參考文章會顯示有關電腦及其作業系統的詳細設定資訊，包括作業系統設定、安全性資訊、產品識別碼和硬體內容 (例如 RAM、磁碟空間和網路卡) 。
ms.topic: reference
ms.assetid: 39954968-3c2e-4d3e-9d89-c9c43347461e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b8db86467c6d3190edd6c041951bf3c30eb21cc4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626748"
---
# <a name="systeminfo"></a>systeminfo

顯示有關電腦及其作業系統的詳細設定資訊，包括作業系統設定、安全性資訊、產品識別碼和硬體內容 (例如 RAM、磁碟空間和網路卡) 。



## <a name="syntax"></a>語法

```
Systeminfo [/s <Computer> [/u <Domain>\<UserName> [/p <Password>]]] [/fo {TABLE | LIST | CSV}] [/nh]
```

### <a name="parameters"></a>參數

|參數|描述|
|---------|-----------|
|/s \<Computer>|指定遠端電腦的名稱或 IP 位址 (不要使用反斜線) 。 預設是本機電腦。|
|u \<Domain>\<UserName>|使用指定之使用者帳戶的帳戶許可權來執行命令。 如果未指定 **/u** ，此命令會使用目前登入發出命令的電腦之使用者的許可權。|
|/p \<Password>|指定 **/u** 參數中指定之使用者帳戶的密碼。|
|/fo \<Format>|指定具有下列其中一個值的輸出格式：</br>資料表：在資料表中顯示輸出。</br>清單：在清單中顯示輸出。</br>CSV：以逗點分隔值格式顯示輸出。|
|/nh|隱藏輸出中的資料行標頭。 當 **/fo** 參數設定為數據表或 CSV 時有效。|
|/?|在命令提示字元顯示說明。|

## <a name="examples"></a>範例

若要查看名為 Srvmain 之電腦的設定資訊，請輸入：

**systeminfo/s srvmain**

若要從遠端查看位於 Maindom 網域上名為 Srvmain2 之電腦的設定資訊，請輸入：

**systeminfo/s srvmain2/u maindom\hiropln**

若要從遠端查看設定資訊 (以清單格式) 針對位於 Maindom 網域的電腦名稱為 Srvmain2 的電腦，請輸入：

**systeminfo/s srvmain2/u maindom\hiropln/p p@ssW23 /fo list**

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)