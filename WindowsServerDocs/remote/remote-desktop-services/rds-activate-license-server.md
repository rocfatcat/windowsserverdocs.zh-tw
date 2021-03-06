---
title: 啟用遠端桌面服務授權伺服器
description: 安裝並啟用 RD 授權伺服器
ms.topic: article
ms.assetid: eb24ddd2-0361-41fe-bd6b-c7c63427cb71
author: lizap
ms.author: elizapo
ms.date: 09/20/2016
manager: dongill
ms.openlocfilehash: 0caf683c95bcaaa8838028bb78c1209ccd5c916c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948901"
---
# <a name="activate-the-remote-desktop-services-license-server"></a>啟用遠端桌面服務授權伺服器

>適用於：Windows Server (半年通道)、Windows Server 2019、Windows Server 2016

遠端桌面服務授權伺服器會在使用者和裝置存取 RD 工作階段主機時，為他們發出用戶端存取使用權 (CAL)。 您可以使用遠端桌面授權管理員來啟用授權伺服器。

## <a name="install-the-rd-licensing-role"></a>安裝 RD 授權角色

1. 使用系統管理員帳戶登入您要作為授權伺服器的伺服器。
2. 在 [伺服器管理員] 中，按一下 [角色摘要]  ，然後按一下 [新增角色]  。
   角色精靈的第一個頁面上，按 [下一步]  。
3. 選取 [遠端桌面服務]  並按 [下一步]  ，然後在 [遠端桌面服務] 頁面上按 [下一步]  。
4. 選取 [遠端桌面授權]  ，然後按 [下一步]  。
5. 設定網域 - 選取 [設定此授權伺服器的探索範圍]  ，並按一下 [此網域]  ，然後按 [下一步]  。
6. 按一下 [安裝]  。

## <a name="activate-the-license-server"></a>啟用授權伺服器

1. 開啟 [遠端桌面授權管理員]：按一下 [開始] > [系統管理工具] > [遠端桌面服務] > [遠端桌面授權管理員]  。
2. 以滑鼠右鍵按一下授權伺服器，然後按一下 [啟用伺服器]  。
3. 在 [歡迎頁面] 上按 [下一步]  。
4. 針對連線方法，選取 [自動連線 (建議使用)]  ，然後按 [下一步]  。
5. 輸入您的公司資訊 (您的名稱、公司名稱、您的地理區域)，然後按 [下一步]  。
6. 選擇性地輸入任何其他公司資訊 (例如，電子郵件和公司地址)，然後按 [下一步]  。
7. 確定未選取 [立即啟動安裝授權精靈]  (我們將在後續步驟安裝授權)，然後按 [下一步]  。

您的授權伺服器現在已可開始發出及管理授權。