---
title: 使用 Azure 檔案同步來同步您的檔案伺服器與雲端
description: 使用 Azure 檔案同步將組織的檔案共用集中在 Azure 中，同時保有內部部署檔案伺服器的彈性、效能及相容性。 Azure 檔案同步使用選擇性的雲端分層功能，將 Windows Server 轉換成 Azure 檔案共用的快速快取。
ms.topic: article
author: fauhse
ms.author: fauhse
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: ce3f314eb4372ecc7448a53a3aeda35b5c6288a8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969675"
---
# <a name="sync-your-file-server-with-the-cloud-by-using-azure-file-sync"></a>使用 Azure 檔案同步來同步您的檔案伺服器與雲端

>適用於：Windows Admin Center、Windows Admin Center 預覽版

使用 Azure 檔案同步將組織的檔案共用集中在 Azure 中，同時保有內部部署檔案伺服器的彈性、效能及相容性。 Azure 檔案同步使用選擇性的雲端分層功能，將 Windows Server 轉換成 Azure 檔案共用的快速快取。 您可以使用 Windows Server 上可用的任何通訊協定來從本機存取資料，包括 SMB、NFS 和 FTPS。

當您的檔案同步到雲端之後，您就可以將多部伺服器連線到相同的 Azure 檔案共用，以便在本機同步和快取內容，也就是 (Acl) 的許可權也一律會進行傳輸。 Azure 檔案儲存體提供可產生 Azure 檔案共用差異快照集的快照集功能。 這些快照集甚至可以透過 SMB 掛接為唯讀網路磁碟機，方便流覽和還原。 結合雲端階層處理，執行內部部署檔案伺服器的作業並不容易。

如需詳細資訊，請參閱[規劃 Azure 檔案同步部署](https://aka.ms/afs)。