---
title: Windows Server 2019 中 Windows Time Service 功能的 Insider Preview
description: Windows Server 2019 中新的 Windows Time Service 功能
author: dahavey
ms.author: dahavey
ms.date: 06/06/2020
ms.topic: article
ms.openlocfilehash: 01968fe51d25f394e346cebc8dbeafd2dd17ca4a
ms.sourcegitcommit: b5b040a47cf48c94852de9aad8b91475f891d2f7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2020
ms.locfileid: "88563368"
---
# <a name="insider-preview"></a>Insider Preview


## <a name="leap-second-support"></a>閏秒支援

> 適用於：Windows Server 2019 和 Windows 10 (1809 版)

閏秒是 UTC 的臨時 1 秒調整。 隨著地球的旋轉速度變慢，[UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) (原子時幅) 會與[平均太陽時間](https://en.wikipedia.org/wiki/Solar_time#Mean_solar_time)或天文時間分歧。 一旦 UTC 的分歧高達 .9 秒，就會插入[閏秒](https://en.wikipedia.org/wiki/Leap_second)，使 UTC 與平均太陽時間保持同步。

閏秒變得非常重要，用以符合美國和歐盟的準確度和可追溯性法規需求。

如需詳細資訊，請參閱：

- 我們的[公告部落格](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- 適用於[開發人員](https://aka.ms/Dev-LeapSecond)的驗證指南

- 適用於 [IT 專業人員](https://aka.ms/ITPro-LeapSecond)的驗證指南


## <a name="precision-time-protocol"></a>精確時間通訊協定

> 適用於：Windows Server 2019 和 Windows 10 (1809 版)

Windows Server 2019 和 Windows 10 (1809 版) 內含的新時間提供者可讓您使用精確時間通訊協定 (PTP) 來同步處理時間。 隨著時間分散於網路，其會遇到延遲，若未將延遲納入考量，或者不是對稱的，就會越來越難以了解從時間伺服器傳送的時間戳記。 PTP 讓網路裝置能夠將每個網路裝置所引入的延遲新增到時間量測中，進而將更準確的時間樣本提供給 Windows 用戶端。

如需詳細資訊，請參閱：

- 我們的[公告部落格](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- 適用於 [IT 專業人員](https://aka.ms/PTPValidation)的驗證指南


## <a name="software-timestamping"></a>軟體時間戳記

> 適用於：Windows Server 2019 和 Windows 10 (1809 版)

透過網路從時間伺服器接收計時封包時，該封包必須先由作業系統的網路堆疊進行處理，才能在時間服務中使用。 網路堆疊中的每個元件都會引入變動的延遲量，進而影響時間量測的準確度。

![軟體時間戳記](../media/Windows-Time-Service/software-timestamping.png)

為了解決這個問題，軟體時間戳記可讓我們為上面所示「Windows 網路元件」前後的封包加上時間戳記，以將作業系統的延遲納入考量。

如需詳細資訊，請參閱：

- 我們的[公告部落格](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- [開發人員和 IT 專業人員的驗證指南](https://github.com/microsoft/W32Time/tree/master/Leap%20Seconds)


---
