---
title: 額外發佈區域
description: 了解 AEM as a Cloud Service 如何支援額外發佈區域以提高可用性並減少延遲。
exl-id: b9ac3c6a-eb8b-461d-8f1d-a0356046a3f9
feature: Operations
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 71%

---


# 額外發佈區域 {#additional-publish-regions}

可以在使用 AEM Sites 設定的計畫上授權和啟用額外發佈區域。設定後，中繼和生產環境中的流量會路由至多個發佈伺服器陣列，這樣可取得以下優勢：

* 減少延遲 - 會將從 CDN 路由至 AEM 發佈執行個體的請求導向最近的發佈區域，這有利於多個地理位置中的使用者所造訪的網站和應用程式。
* 更高的可用性 - 如果某個區域無法使用，CDN 會將流量導向到額外可用區域。

組織最多可授權三個額外的發佈區域。

>[!NOTE]
>
>* 此功能適用於Sites和Forms解決方案。
>* 此功能無法套用至[沙箱程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。
>* 此功能需要您的程式更新至AEM發行版本12142或更高版本。

## 使用案例 {#use-cases}

以下是一些組織可以從授權額外發佈區域中受惠的使用案例。

1. 對於接收到來自遠離主要區域的使用者的重要或業務關鍵型流量的組織，額外發佈區域可減少這些訪客的延遲體驗。
1. 對於若無法使用網站即可能蒙受重大金錢或聲譽損失的組織，使用額外的發佈區域可讓 AEM 發佈階層在面臨區域失敗時能更快恢復，並從而減少損失。
1. 對於內容作者遠離大多數發布層訪客的組織，可以選擇內容作者附近的位置為主要區域。可以在發布端流量附近配置其他發佈區域。此設定可確保雙方都能從優化的體驗中受益。

## 啟用和設定 {#enabling-and-configuring}

授權額外發佈區域後，可使用 Cloud Manager 設定這些區域。如需詳細說明，請參閱 [Cloud Manager 文件](/help/implementing/cloud-manager/manage-environments.md#multiple-regions)。

額外發佈區域適用於中繼和生產環境，但不適用於 RDE 或開發環境。

如果某個地區無法使用，客戶就不需要管理將流量路由到可用地區，因為它是由AdobeCDN管理。

如下方「進階網路考量事項」一節所述，建議使用進階網路的客戶針對每個額外的發佈區域進行設定，以便在區域無法使用時維持可用性。


## 進階網路考量事項 {#advanced-networking-considerations}

若在已設定進階網路的計畫中啟用額外發佈區域，和進階網路規則相符的額外發佈區域中的流量會依預設路由通過主要區域。為了善用提高的可用性，建議在額外區域啟用進階網路。

如需詳細資訊，請參閱進階網路文件中的[額外發佈區域的進階網路設定](/help/security/configuring-advanced-networking.md#advanced-networking-configuration-for-additional-publish-regions)章節，包括如何將進階網路設定新增到額外區域而不會失去連線能力。

## 記錄 {#logging}

如果啟用其他發佈區域，將透過Cloud Manager提供每個區域的個別記錄。 如需詳細資訊，請參閱[存取及管理其他Publish地區的](/help/implementing/cloud-manager/manage-logs.md)及[記錄](/help/implementing/developing/introduction/logging.md#logs-for-additional-publish-regions)。

## 限制 {#limitations}

在考慮使用額外發佈區域時，請謹記以下限制。

* 其他發佈區域只能新增到AEM Sites或AEM Forms。
   * 其他發佈區域不會延伸至相同方案中部署的其他AEM解決方案或相關功能(例如AEM Assets或Adobe Learning Manager)。
   * 不過，只要有至少一個Sites或Forms解決方案套用至計畫，您就可以將這些解決方案新增至計畫。
* 只有在租用戶中有相關權益且未使用時，才能新增額外區域。
* 最多可以向任何個別環境新增三個額外的發佈區域。
* 額外區域僅適用於生產計畫。此功能在沙箱計畫中無法使用。
* 額外發佈區域僅適用於中繼和生產環境，不適用於 RDE 或開發環境。
* 額外發佈區域會要求您的計畫需更新至 AEM 12142 版或更高版本。
