---
title: 其他發佈區域
description: 瞭解AEMas a Cloud Service如何支援其他發佈區域，以提高可用性和減少延遲。
source-git-commit: 9fccc1672aad243b648115e657396be1ce4ed614
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---


# 其他發佈區域 {#additional-publish-regions}

透過AEM Sites設定的計畫，可以授權並啟用其他發佈區域。 設定後，中繼和生產環境中的流量會路由至多個發佈陣列，具備下列優點：

* 減少延遲 — 從CDN路由至AEM發佈執行個體的請求會導向到最近的發佈區域，對使用者在多個地理區域造訪的網站和應用程式有利。
* 可用性較高 — 如果區域無法使用，CDN會將流量導向其他可用區域。

組織最多可授權三個額外的發佈區域。

>[!NOTE]
>
>此功能目前僅適用於AEM Sites。 也無法套用至沙箱計畫。 此外，請注意，額外的發佈區域功能要求您的程式更新為AEM發行版本12142或更高版本。

## 使用案例 {#use-cases}

以下是一些組織可以從授權其他發佈區域受益的使用案例。

1. 對於從遠離主要區域的使用者接收大量或業務關鍵型流量的組織，其他發佈區域可以減少這些訪客所經歷的延遲。
1. 對於在網站無法使用時可能遭受重大金錢或聲譽損失的組織，可透過使用其他發佈區域來緩解，以使AEM發佈層級更能抵禦區域故障。
1. 對於其內容作者位在遠離大多數發佈層級訪客的地理位置的組織，可以在內容作者的位置附近選擇主要區域，而可以在發佈端流量附近設定其他發佈區域，使兩個受眾都受益於最佳化體驗。

## 啟用和設定 {#enabling-and-configuring}

授權其他發佈區域後，將使用Cloud Manager設定區域。 請參閱 [Cloud Manager檔案](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) 以取得詳細指示。

其他發佈區域會套用至中繼和生產環境，但不會套用至RDE或開發環境。

## 進階網路考量事項 {#advanced-networking-considerations}

在已設定進階網路的程式上啟用其他發佈區域時，符合進階網路規則的其他發佈區域中的流量預設會透過主要區域路由。 為了利用可用性增加的優勢，建議在其他區域啟用進階網路。

請參閱 [適用於其他發佈區域的進階網路設定](/help/security/configuring-advanced-networking.md#advanced-networking-configuration-for-additional-publish-regions) 詳細資訊，包括如何將進階網路設定新增到其他區域而不會造成連線中斷。

## 限制 {#limitations}

在考慮使用其他發佈區域時，請記住這些限制。

* 其他發佈區域只能新增到AEM Sites。 其他發佈區域不會延伸至部署在相同計畫中的其他AEM解決方案或相關功能(例如AEM Forms或Adobe Learning Manager)。
* 只有當租使用者中有可用的關聯權益且未使用時，才能新增其他區域。
* 任何個別環境最多可以新增三個額外的發佈區域。
* 其他區域僅適用於生產計畫。 沙箱程式中不提供此功能。
* 其他發佈區域僅會套用至中繼和生產環境，不會套用至RDE或開發環境。
* 其他發佈區域需要您的程式更新至AEM發行版本12142或更高版本。
