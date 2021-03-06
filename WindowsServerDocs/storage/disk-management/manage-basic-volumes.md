---
title: 管理基本磁碟區
description: 本文說明如何管理基本磁碟區。
ms.date: 10/12/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e97672e7ceceaa5eea83752169ccfd46bd910ed4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961572"
---
# <a name="manage-basic-volumes"></a>管理基本磁碟區

> **適用於：** Windows 10、Windows 8.1、Windows Server (半年通道)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

基本磁碟是包含主要磁碟分割、延伸磁碟分割或邏輯磁碟機的實體磁碟。 基本磁碟上的磁碟分割和邏輯磁碟機稱為基本磁碟區。 您只能在基本磁碟上建立基本磁碟區。

您可以藉由將現有的主要磁碟分割及邏輯磁碟機延伸到相同磁碟上相鄰的連續未配置空間，將更多空間新增至這些磁碟區。 若要延伸基本磁碟區，必須以 NTFS 檔案系統來格式化該磁碟區。 您可以在包含邏輯磁碟機之延伸磁碟分割的連續可用空間內延伸該磁碟機。 如果您延伸邏輯磁碟機超出延伸磁碟分割中提供的可用空間，只要延伸磁碟分割後面接著連續未配置的空間，延伸磁碟分割就會擴大來包含邏輯磁碟機。

## <a name="see-also"></a>另請參閱

-   [將掛接點資料夾路徑指派給磁碟機](assign-a-mount-point-folder-path-to-a-drive.md)
-   [延伸基本磁碟區](extend-a-basic-volume.md)
-   [壓縮基本磁碟區](shrink-a-basic-volume.md)