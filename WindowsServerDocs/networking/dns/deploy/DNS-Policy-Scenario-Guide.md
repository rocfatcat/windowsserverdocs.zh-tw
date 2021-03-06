---
title: DNS 原則案例指南
description: 本主題是 Windows Server 2016 DNS 原則案例指南的一部分
manager: brianlic
ms.topic: article
ms.assetid: 50fdb08a-bbd8-4107-954a-6699672110ff
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ed28fe6dd472b505d2a39ac55c74c399ef63e068
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966655"
---
# <a name="dns-policy-scenario-guide"></a>DNS 原則案例指南

>適用於：Windows Server (半年度管道)、Windows Server 2016

本指南旨在供 DNS、網路和系統管理員使用。

DNS 原則是 Windows Server 2016 中 DNS 的新功能 &reg; 。 您可以使用本指南來瞭解如何使用 DNS 原則來控制 DNS 伺服器如何根據您在原則中定義的不同參數來處理名稱解析查詢。

本指南包含 DNS 原則總覽資訊，以及特定的 DNS 原則案例，其提供如何設定 DNS 伺服器行為以達成目標的指示，包括主要和次要 DNS 伺服器的地理位置型流量管理、應用程式高可用性、分割大腦 DNS 等等。

本指南涵蓋下列各節。

- [DNS 原則總覽](DNS-Policies-Overview.md)
- [透過主要伺服器使用地理位置流量管理的 DNS 原則](primary-geo-location.md)
- [透過主要-次要部署使用地理位置流量管理的 DNS 原則](primary-secondary-geo-location.md)
- [使用 DNS 原則以時間為基礎進行智慧型 DNS 回應](dns-tod-intelligent.md)
- [使用 Azure 雲端應用程式伺服器以一天的時間為基礎的 DNS 回應](dns-tod-azure-cloud-app-server.md)
- [使用 DNS 原則進行分割的 DNS 部署](split-brain-DNS-deployment.md)
- [在 Active Directory 中使用適用于分裂式 DNS 的 DNS 原則](dns-sb-with-ad.md)
- [使用 DNS 原則在 DNS 查詢上套用篩選](apply-filters-on-dns-queries.md)
- [使用 DNS 原則進行應用程式負載平衡](app-lb.md)
- [使用 DNS 原則進行具有地理位置感知的應用程式負載平衡](app-lb-geo.md)

