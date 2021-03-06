---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: 屬性存放區的角色
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 3486fe03738ab906580a629f084d3a2dd9e25b59
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937910"
---
# <a name="the-role-of-attribute-stores"></a>屬性存放區的角色
Active Directory 同盟服務使用「屬性存放區」一詞來參照組織用來儲存其使用者帳戶及其相關屬性值的目錄或資料庫。 在身分識別提供者組織中設定之後，AD FS 從存放區中抓取這些屬性值，並根據該資訊建立宣告，讓信賴憑證者組織中裝載的 Web 應用程式或服務可以在 \( 使用者帳戶儲存于身分識別提供者組織中的使用者 \) 嘗試存取應用程式或服務時，做出適當的授權決策。

如需有關如何產生宣告的詳細資訊，請參閱＜ [The Role of Claims](The-Role-of-Claims.md)＞。

## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>屬性存放區如何符合您的 AD FS 部署目標
使用者屬性存放區的位置，以及使用者驗證的位置，會決定您設計 AD FS 以支援使用者身分識別的方式。 根據屬性存放區的所在位置，以及使用者在內部網路或網際網路上存取應用程式的位置而定 \( \) ，您可以使用下列其中一個部署目標：

-   [為您的 Active Directory 使用者提供您的宣告感知應用程式和服務的存取權](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807071(v=ws.11))，在此目標中，貴組織中的使用者可在使用者登入公司內部網路中的 Active Directory 時，存取由 AD FS 保護的應用程式或服務， \( 以及您自己的應用程式或服務或合作夥伴的應用程式或服務 \) 。

-   [為您的 Active Directory 使用者提供其他組織的應用程式和服務的存取權](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807123(v=ws.11))-在此目標中， \( \) 當使用者登入公司內部網路中的屬性存放區，以及當他們從網際網路遠端登入時，您組織中的使用者會存取受 AD FS 保護的應用程式或服務，無論是您自己的應用程式或服務或是合作夥伴的應用程式或服務。

-   為[其他組織的使用者提供您的宣告感知應用程式和服務的存取權](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807099(v=ws.11))，在此目標中，另一個組織中的使用者帳戶位於該組織的公司內部網路上的屬性存放區，必須存取您組織中受 AD FS 保護的應用程式。 此目標也適用于在 \- 組織的周邊網路中的屬性存放區中，以取用者為基礎的使用者帳戶，必須能夠存取貴組織中受 AD FS 保護的應用程式。

視屬性存放區的位置和組織的其他需求而定，您可以結合其中數個部署目標來完成 AD FS 部署的設計。

## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>AD FS 支援的屬性存放區
AD FS 支援各種不同的目錄和資料庫存放區，可供您用來解壓縮系統管理員 \- 定義的屬性值，並以這些值填入宣告。 AD FS 支援下列任何目錄或資料庫做為屬性存放區：

-   Windows server 2003 中的 Active Directory、windows server \( 2008 中的 Active Directory Domain Services AD DS \) 、windows server 2012 和 2012 R2 中的 AD DS，以及 windows server 2016。

-   所有版本的 Microsoft SQL Server 2005、SQL Server 2008、SQL Server 2012、SQL Server 2014 和 SQL Server 2016

-   自訂屬性存放區

