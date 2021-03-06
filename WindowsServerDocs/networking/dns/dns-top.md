---
title: 網域名稱系統 (DNS)
description: 本主題概要說明 Windows Server 2016 中的 DNS
manager: brianlic
ms.topic: article
ms.assetid: 1324ba18-4e28-4b9d-bbe7-75707e6d30ab
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1117e523e23bfc5415754484385d290eb2375d91
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954094"
---
# <a name="domain-name-system-dns"></a>網域名稱系統 (DNS)

>適用於：Windows Server (半年度管道)、Windows Server 2016

網域名稱系統 (DNS) 是一種業界標準的通訊協定套件，其中包含 TCP/IP，而且 DNS 用戶端和 DNS 伺服器會將電腦名稱稱到 IP 位址對應名稱解析服務提供給電腦和使用者。

> [!NOTE]
> 除了本主題之外，還有下列 DNS 內容可供使用。
>
> -   [DNS 用戶端的新功能](What-s-New-in-DNS-Client.md)
> -   [DNS 伺服器的新功能](What-s-New-in-DNS-Server.md)
> -   [DNS 原則案例指南](deploy/DNS-Policy-Scenario-Guide.md)
> -   影片： [Windows Server 2016： IPAM 中的 DNS 管理](https://channel9.msdn.com/Blogs/windowsserver/Windows-Server-2016-DNS-management-in-IPAM)

在 Windows Server 2016 中，DNS 是一種伺服器角色，您可以使用伺服器管理員或 Windows PowerShell 命令來安裝它。 如果您要安裝新的 Active Directory 樹系和網域，則會自動安裝 DNS，Active Directory 做為樹系和網域的全域目錄伺服器。

Active Directory Domain Services (AD DS) 會使用 DNS 作為其網域控制站位置機制。 執行任何主體 Active Directory 作業時（例如驗證、更新或搜尋），電腦會使用 DNS 來尋找 Active Directory 網域控制站。 此外，網域控制站會使用 DNS 來尋找彼此。

DNS 用戶端服務會包含在 Windows 作業系統的所有用戶端和伺服器版本中，而且預設會在作業系統安裝時執行。 當您使用 DNS 伺服器的 IP 位址設定 TCP/IP 網路連線時，DNS 用戶端會查詢 DNS 伺服器以探索網域控制站，並將電腦名稱稱解析成 IP 位址。 例如，當具有 Active Directory 使用者帳戶的網路使用者登入 Active Directory 網域時，DNS 用戶端服務會查詢 DNS 伺服器，以找出 Active Directory 網域的網域控制站。 當 DNS 伺服器回應查詢，並將網域控制站的 IP 位址提供給用戶端時，用戶端會連線到網域控制站，而驗證程式就可以開始。

Windows Server 2016 DNS 伺服器和 DNS 用戶端服務會使用 TCP/IP 通訊協定套件中包含的 DNS 通訊協定。 DNS 是 TCP/IP 參考模型的應用層一部分，如下圖所示。

![TCP/IP 中的 DNS](../media/Domain-Name-System--DNS-/dns_in_tcpip.jpg)


