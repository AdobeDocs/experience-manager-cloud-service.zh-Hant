---
title: 了解什麼是Cloud Manager
description: 請詳閱本頁，了解Cloud Manager、Cloud Manager程式和環境。
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: c206bc241bccf6f8a5bfb4946d6231f53438861a
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 3%

---

# Cloud Manager 簡介 {#intro-cloud-manager}

Cloud Manager是AEM的必要元件，可作為Cloud Service，也是您團隊的單一進入點。

為了支援具有企業開發設定的Cloud Service,AEM as a Cloud已與Cloud Manager及其專門建立的CI/CD管道完全整合，這些管道可確保完整測試和最高的程式碼品質，以提供絕佳的體驗。

為確保客戶能以AEM as aCloud Service快速上手，Cloud Manager提供以自助方式開始使用所需的一切，包括建立雲端資源和環境的能力。 如此一來，您的AEM開發人員就能透過Cloud Manager存取Git存放庫。 使用Cloud Manager，開發團隊可以自助方式經常致力於提交變更。

您的系統管理員將負責設定您的Cloud Manager團隊，團隊中將包括將建立您雲端資源和開發人員的個人。 請參考[AEM as a Cloud Service的企業團隊開發設定](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)，了解Cloud Manager如何在企業團隊開發設定中支援。

## 導覽至Cloud Manager的概觀頁面 {#navigate-cloud-manager}

請依照下列步驟導覽至Cloud Manager:

1. 從[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)直接導覽至Cloud Manager的登入頁面。

   >[!NOTE]
   >請將此頁面加入書籤，以供日後參考，並協助您直接導覽至Cloud Manager的登陸頁面。

1. 從Cloud Manager的&#x200B;**方案和產品**&#x200B;頁面中選取方案，以啟動&#x200B;**概述**&#x200B;頁面。

此外，您也可以從Adobe Experience Cloud首頁導覽至Cloud Manager的方案和產品頁面。 請遵循下列步驟：

1. 直接導覽至[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home)並使用您的Adobe ID登入。

1. 選擇&#x200B;**Experience Manager**。

1. 按一下Cloud Manager卡片中的&#x200B;**Launch**。 成功登入Cloud Manager後，您就可以使用使用者介面(UI)。

   成功登入後，系統會將您導向至Cloud Manager的登陸頁面。

## Cloud Manager中的角色型權限 {#role-based-permissions}

| 權限 | 說明 | 業務負責人 | 部署管理員 | 計畫經理 | 開發人員 |
|--- |--- |--- |--- |--- |--- |
| 添加程式<br>編輯程式 | 新增方案。<br>編輯程式 — 添加或刪除解決方案或附加元件的 | x |  |  |  |
| 建立環境 | 建立Prod+Stage、Dev、Environments。 | x | x |  |  |
| 更新環境 | 更新Prod+Stage、Dev、Environments。 | x | x |  |  |
| 刪除開發環境 | 刪除開發環境。 | x | x |  |  |
| 管道設定 | 設定或編輯管道。 |  | x |  |  |
| 管道執行 | 啟動管道。 | x | x |  |  |
| 管道執行 | 拒絕/批准重要的3層故障。 | x | x | x |  |
| 管道執行 | 提供GoLive核准。 | x | x | x |  |
| 管道執行 | 排程生產部署。 | x | x | x |  |
| 管道刪除 | 允許刪除管道。 |  | x |  |  |
| 執行取消 | 取消當前執行。 |  | x |  |  |
| 產生個人存取權杖 | 存取Git。 |  | x |  | x |

>[!NOTE]
>可以將用戶分配給多個角色。 例如，將業務所有者和部署管理員角色分配給用戶時，會為其提供這些權限的組合或總和。

## Cloud Manager方案 {#cloud-manager-programs}

Cloud Manager計畫表示一組Cloud Manager環境，支援業務計畫的邏輯集，通常對應於購買的服務級別協定(SLA)。 例如，一個方案可代表支援全域公用網站的AEM資源，而另一個方案則代表內部中央DAM。 請觀看此[影片](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)，以進一步了解使用Cloud Manager程式。

使用者可以建立&#x200B;**沙箱**&#x200B;或&#x200B;**生產**&#x200B;程式。

* 建立&#x200B;*生產程式*以在將來的適當時間啟用即時流量。
如需詳細資訊，請參閱[生產程式簡介](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/production-programs/introduction-production-programs.html?lang=en) 。

* *沙箱方案*通常建立以用於培訓、執行示範、啟用、POC或檔案。 其用途不是攜帶即時流量，且生產計畫不會受到限制。 其中包含Sites和Assets，且會透過Git分支自動填入，該分支包含范常式式碼、開發環境及非生產管道。
如需詳細資訊，請參閱[沙箱方案簡介](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sandbox-programs/introduction-sandbox-programs.html?lang=en) 。

## Cloud Manager環境 {#cloud-manager-environments}

您的雲端環境將透過Cloud Manager建立、存取及檢視。 這些環境可以是生產環境、預備環境或開發環境。 不同環境支援不同用途，且可使用不同的CI/CD管道參與。 環境由下列服務組成：

* [AEM作者服務](#author-services)
* [AEM Publish Services](#publish-services)
* [Dispatcher服務](#dispatcher-services)

   >[!NOTE]
   > 請參閱影片[使用AdobeCloud Manager環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager)以深入了解可用環境。 此外，請參閱[管理環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en)以進一步了解使用者可建立的環境類型以及使用者如何建立環境。

### AEM Author Service {#author-services}

AEM作者服務隨附於建立、管理及更新網站內容和數位資產的環境中。 通常只有內部使用者可存取「作者服務」，且位於登入畫面後。 製作服務的設計方式為製作和預覽環境。

### AEM Publish Service {#publish-services}

AEM發佈服務包含在托管一般使用者體驗的環境中，例如網站。 這是網站訪客將檢視並與之互動的服務。 發佈服務通常可公開使用。

### AEM Dispatcher服務 {#dispatcher-services}

Dispatcher是`Apache HTTP Web server`模組，提供位於AEM Publish Service前面的安全性和效能層。
