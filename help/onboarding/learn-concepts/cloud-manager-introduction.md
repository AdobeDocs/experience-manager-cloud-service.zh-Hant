---
title: 了解什麼是Cloud Manager
description: 請詳閱本頁，了解Cloud Manager、Cloud Manager程式和環境。
source-git-commit: 185a933e12ad81689168ad88574019ed219db06d
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Cloud Manager 簡介 {#intro-cloud-manager}

Cloud Manager是AEM的必要元件，可作為Cloud Service，也是您團隊的單一進入點。

為了支援具有企業開發設定的Cloud Service,AEM as a Cloud已與Cloud Manager及其專門建立的CI/CD管道完全整合，這些管道可確保完整測試和最高的程式碼品質，以提供絕佳的體驗。

為確保客戶能以AEM as aCloud Service快速上手，Cloud Manager提供以自助方式開始使用所需的一切，包括建立雲端資源和環境的能力。 如此一來，您的AEM開發人員就能透過Cloud Manager存取Git存放庫。 使用Cloud Manager，開發團隊可以自助方式經常致力於提交變更。

您的系統管理員將負責設定您的Cloud Manager團隊，團隊中將包括將建立您雲端資源和開發人員的個人。 請參考[AEM as a Cloud Service的企業團隊開發設定](/help/implementing/cloud-manager/enterprise-team-dev-setup.md)，了解Cloud Manager如何在企業團隊開發設定中支援。

## Cloud Manager程式{#cloud-manager-programs}

Cloud Manager計畫表示一組Cloud Manager環境，支援業務計畫的邏輯集，通常對應於購買的服務級別協定(SLA)。 例如，一個方案可代表支援全域公用網站的AEM資源，而另一個方案則代表內部中央DAM。 請觀看此[影片](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)，以進一步了解使用Cloud Manager程式。

使用者可以建立&#x200B;**沙箱**&#x200B;或&#x200B;**生產**&#x200B;程式。

* 建立&#x200B;*生產程式*以在將來的適當時間啟用即時流量。
如需詳細資訊，請參閱[生產程式簡介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md) 。

* *沙箱方案*通常建立以用於培訓、執行示範、啟用、POC或檔案。 其用途不是攜帶即時流量，且生產計畫不會受到限制。 其中包含Sites和Assets，且會透過Git分支自動填入，該分支包含范常式式碼、開發環境及非生產管道。
如需詳細資訊，請參閱[沙箱方案簡介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) 。

## Cloud Manager環境{#cloud-manager-environments}

您的雲端環境將透過Cloud Manager建立、存取及檢視。 這些環境可以是生產環境、預備環境或開發環境。 不同環境支援不同用途，且可使用不同的CI/CD管道參與。 環境由下列服務組成：

* [AEM作者服務](#author-services)
* [AEM Publish Services](#publish-services)
* [Dispatcher服務](#dispatcher-services)

   >[!NOTE]
   > 請參閱影片[使用AdobeCloud Manager環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager)以深入了解可用環境。 此外，請參閱[管理環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en)以進一步了解使用者可建立的環境類型以及使用者如何建立環境。

### AEM作者服務{#author-services}

AEM作者服務隨附於建立、管理及更新網站內容和數位資產的環境中。 通常只有內部使用者可存取「作者服務」，且位於登入畫面後。 製作服務的設計方式為製作和預覽環境。

### AEM發佈服務{#publish-services}

AEM發佈服務包含在托管一般使用者體驗的環境中，例如網站。 這是網站訪客將檢視並與之互動的服務。 發佈服務通常可公開使用。

### AEM Dispatcher服務{#dispatcher-services}

Dispatcher是`Apache HTTP Web server`模組，提供位於AEM Publish Service前面的安全性和效能層。