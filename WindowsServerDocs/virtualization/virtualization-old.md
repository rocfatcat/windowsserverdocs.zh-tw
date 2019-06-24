---
title: 虛擬化
description: 提供虛擬化技術概觀，例如容器、Hyper-V 和 Hyper-V -V 虛擬交換器，以及 Windows Server 2016 和較新版作業系統的其他內容連結。
ms.prod: windows-server-threshold
manager: dougkim
ms.technology: compute
ms.topic: article
author: shortpatti
ms.author: pashort
ms.localizationpriority: medium
ms.date: 03/16/2018
ms.openlocfilehash: e6dbb5be6d836462c9a24078dbec3700b09b08fc
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446055"
---
# <a name="virtualization"></a>虛擬化

>適用於：Windows Server （半年通道），Windows Server 2016 

>[!TIP]
> 尋找舊版 Windows Server 的相關資訊嗎？ 查看我們其他位於 docs.microsoft.com 的 [Windows Server 文件庫](/previous-versions/windows/)。 您也可以[搜尋這個網站](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)以取得特定資訊。

<img src="../media/landing-icons/virtualization.png" style='float:left; padding:.5em;' alt="Icon showing a box with spokes"> Windows Server 2016 中的虛擬化是建立軟體定義基礎結構所需的其中一種基礎技術。 搭配網路功能與儲存空間，虛擬化功能可以賦予為您客戶提供強大工作負載所需的彈性。

Windows Server 虛擬化技術包括 HYPER-V、 HYPER-V 虛擬交換器，以及受防護網狀架構與受防護的虛擬機器的更新\(Vm\)，可改善安全性、 延展性及可靠性。 容錯移轉叢集、網路功能和儲存空間的更新讓您更容易在搭配 Hyper-V 時部署和管理這些技術。 


<ul class="cardsI panelContent">
<li>
        <a href="../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md">
          <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-access.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>受防護網狀架構與受防護的 VM</h3>
                        <p>身為雲端服務提供者或企業私人雲端系統管理員，您可以使用受防護網狀架構為 VM 提供更安全的環境。 受防護網狀架構包含一個主機守護者服務 (HGS)-一般而言，三個節點叢集-加上一個或多個受防護主機和一組受防護的 Vm。</p>
                    </div>
                </div>
            </div>
        </div>
       </a>
    </li>
<li>
        <a href="/hyper-v/Hyper-V-on-Windows-Server.md">
          <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-access.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>適用於企業的 Windows 10:若要使用裝置工作的方式</h3>
                        <p>Hyper-V 技術透過硬體虛擬化提供運算資源。 Hyper-V 會建立電腦的軟體版本 (稱為虛擬機器)，讓您用來執行作業系統和應用程式。 您可以同時執行多個虛擬機器，也能視需要建立和刪除它們。 </p>
                    </div>
                </div>
            </div>
        </div>
       </a>
     </li>

<li>
        <a href="https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-server-2016">
          <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-access.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Microsoft Hyper-V Server</h3>
                        <p>Hyper-V 技術透過硬體虛擬化提供運算資源。 Hyper-V 會建立電腦的軟體版本 (稱為虛擬機器)，讓您用來執行作業系統和應用程式。 您可以同時執行多個虛擬機器，也能視需要建立和刪除它們。 </p>
                    </div>
                </div>
            </div>
        </div>
       </a>
     </li>


<li>
        <a href="hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md">
          <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-access.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Hyper-V 虛擬交換器</h3>
                        <p>Hyper-V 虛擬交換器是一種軟體式 Layer-2 乙太網路交換器，隨附在所有版本的 Hyper-V 中。</p>

                        <p>安裝 Hyper-V 伺服器角色之後，即可在 Hyper-V 管理員中使用 Hyper-V 虛擬交換器。</p>

                        <p>隨附的 Hyper-V 虛擬交換器是以程式設計方式管理和可擴充的功能，能讓您將虛擬機器連線到虛擬網路和實體網路。</p> 

                        <p>此外，Hyper-V 虛擬交換器提供安全性、隔離以及服務層級的原則強化。</p>
                    </div>
                </div>
            </div>
        </div>
       </a>
     </li>


<li>
       <a href="https://docs.microsoft.com/virtualization/windowscontainers">
          <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-access.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Windows 容器</h3>
                        <p>Windows 容器可提供作業系統層級的虛擬化，讓多個隔離的應用程式在單一系統上執行。 此功能包括兩種不同類型的容器執行階段，能提供不同程度的應用程式隔離。</p>
                    </div>
                </div>
            </div>
        </div>
       </a>
     </li>




## <a name="related"></a>相關

Hyper-V 需要特定硬體來建立虛擬化環境。 如需詳細資訊，請參閱 [Windows Server 2016 上 Hyper-V 的系統需求](./hyper-v/system-requirements-for-hyper-v-on-windows.md)。 

如需詳細資訊，請參閱 [Windows 10 上的 Hyper-V](https://docs.microsoft.com/virtualization/hyper-v-on-windows)。
