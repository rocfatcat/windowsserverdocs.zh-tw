---
title: AD FS 進行登入分頁
description: 本文件說明的新登入體驗的 AD FS 2019。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c528b9c4e944849b7ed9a2fc5213a7b263be70c7
ms.sourcegitcommit: ccc802338b163abdad2e53b55f39addcfea04603
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66687374"
---
# <a name="ad-fs-paginated-sign-in"></a>AD FS 進行登入分頁


適用於 Windows Server 2019 中的 AD FS，我們已重新設計的登入 UI。  現在，AD FS 登入將會有相同的外觀及操作，Azure ad。  這會提供使用者更一致登入體驗、 併入置中和已編頁的使用者流程。

## <a name="whats-changing"></a>有哪些變更
在 Windows Server 2012 R2 和 2016年中的 AD FS，您的登入畫面看起來如下：

![oldsignin](media/AD-FS-paginated-sign-in/signin1.png)

我們正在移開顯示在畫面右側位於單一表單。

在 Windows Server 2019 AD FS，這些是主要的設計變更，您會看到：


- **A 集中 UI**。 先前，登入 UI 存在於螢幕的右邊如上所示。 我們已移動的 UI 前端和中心以現代化的體驗。
- **分頁**。 而不是提供長填寫表單，我們已納入新的流程，將會引導您完成逐步的登入體驗。 我們的遙測會顯示使用此方法時，我們的客戶有更成功的登入。它也提供我們更多的彈性，以納入各種驗證方法，這類美國電話要素驗證。

![newsignin](media/AD-FS-paginated-sign-in/signin2.png)

在第一個頁面上，您將要求輸入您的使用者名稱。 您也可以選取 「 讓我保持登中 」 的選項以減少登入提示的頻率，並安全地執行這項操作時保持登入。 （這個選項會停用預設值。）

![newsignin](media/AD-FS-paginated-sign-in/signin3.png)

在第二個頁面上，您會看到您的系統管理員所設定的驗證選項。 如果已啟用 允許外部驗證為主要，這將會包含也。

![newsignin](media/AD-FS-paginated-sign-in/signin4.png)

在第三個頁面上，您將要求輸入密碼 （假設您選取 「 密碼 」 為您的驗證選項）。

## <a name="how-to-get-the-new-experience"></a>如何取得新的體驗

### <a name="new-installation-of-ad-fs"></a>新安裝的 AD FS
如果您是新的客戶，AD fs，您會收到新的設計預設。

### <a name="upgrading-a-farm"></a>升級伺服器陣列
如果您是現有的客戶 AD FS 2012 R2 或 2016年，有兩種方式可將伺服器升級至 AD FS 2019 並啟用到 2019 FBL 之後會收到新的設計。

- 允許在新登入時透過 Powershell。 執行下列命令來啟用分頁： ``Set-AdfsGlobalAuthenticationPolicy -EnablePaginatedAuthenticationPages $true``

 - 啟用外部驗證為主要，透過 Powershell 或透過 AD FS 伺服器管理員。 啟用此功能時，將會啟用新的分頁的登入頁面。
如果您是新的客戶，AD fs，您會收到新的設計預設。 不過，如果您是現有的客戶與 AD FS 2012 R2 或 2016年，有幾個步驟，您必須在收到新的設計： ``Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true``

## <a name="customization"></a>自訂
自訂選項仍會適用於 ad FS 2019。
以下是一些連結可供您參考其他文件。

• 對於使用者而言不打算將其伺服器升級至 AD FS 2019 但仍想要新的設計：[在 Active Directory Federation Services 中使用 Azure AD UX 網頁佈景主題](azure-ux-web-theme-in-ad-fs.md)

• 自訂的中央位置：[自訂 AD FS 使用者登入](ad-fs-user-sign-in-customization.md)