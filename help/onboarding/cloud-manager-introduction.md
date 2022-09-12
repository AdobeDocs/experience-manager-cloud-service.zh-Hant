---
title: Cloud Manager 簡介
description: 了解Cloud Manager如何透過其方案、環境和管道支援您的AEM專案。
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 2d793f22e554c2a4bde8831b5053d1640ba07c70
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 4%

---

# Cloud Manager 簡介 {#intro-cloud-manager}

Cloud Manager是AEMas a Cloud Service的必要元件，是您團隊的單一進入點。 其專門建立的CI/CD管道可確保徹底測試和最高的程式碼品質，以提供優越的體驗。 為確保客戶能快速啟動其專案，Cloud Manager以自助方式提供所需的一切，包括建立雲端資源和環境並存取Git存放庫的能力。 這些功能可支援企業開發設定，讓團隊能夠經常致力於提交變更、快速提供卓越的數位體驗，並加快實現價值的速度。

您的系統管理員負責設定您的Cloud Manager團隊，團隊中將包括將建立您雲端資源和開發人員的人員。 有關如何設定和擴展企業開發團隊以及查看AEM as a Cloud Service如何支援您的開發流程的詳細資訊，請參閱本檔案 [AEMas a Cloud Service的企業團隊開發設定。](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)

## 導覽至Cloud Manager的概觀頁面 {#navigate-cloud-manager}

請依照下列步驟導覽至Cloud Manager。

1. 導覽至Cloud Manager的登入頁面，網址為 [`https://my.cloudmanager.adobe.com`.](https://my.cloudmanager.adobe.com/).

1. 從Cloud Manager的 **方案和產品** 頁面來啟動 **概述** 頁面。

您也可以依照下列步驟，從Adobe Experience Cloud首頁導覽至Cloud Manager的方案和產品頁面。

1. 導覽至Adobe Experience Cloud，網址為 [`https://experience.adobe.com`](https://experience.adobe.com) 並使用Adobe ID登入。

1. 參考工具列右上角顯示的組織名稱，確定您位於正確的組織。

1. 選擇 **Experience Manager**.

1. 在 **Cloud Manager** 卡片，按一下 **Launch**

## Cloud Manager中的角色型權限 {#role-based-permissions}

| 權限 | 說明 | 業務負責人 | 部署管理員 | 計畫經理 | 開發人員 |
|--- |--- |--- |--- |--- |--- |
| 添加程式<br>編輯方案 | 新增方案<br>添加或刪除解決方案或附加元件 | x |  |  |  |
| 建立環境 | 建立生產+測試和開發環境 | x | x |  |  |
| 更新環境 | 更新生產+測試和開發環境 | x | x |  |  |
| 刪除開發環境 | 刪除開發環境 | x | x |  |  |
| 管道設定 | 設定和編輯管道 |  | x |  |  |
| 管道執行 | 啟動管道 | x | x |  |  |
| 管道執行 | 拒絕/批准重要的3層質量門故障 | x | x | x |  |
| 管道執行 | 提供上線批准 | x | x | x |  |
| 管道執行 | 排程生產部署 | x | x | x |  |
| 管道刪除 | 允許刪除管道 |  | x |  |  |
| 執行取消 | 取消當前執行 |  | x |  |  |
| 產生個人存取權杖 | 存取Git |  | x |  | x |

>[!NOTE]
>
>可以將用戶分配給多個角色。 例如，指派兩者 **業務負責人** 和 **部署管理員** 使用者的角色會提供這些權限的總和。

## Cloud Manager方案 {#cloud-manager-programs}

Cloud Manager計畫代表一組Cloud Manager環境，支援業務計畫的邏輯分組。 這些分組通常對應於購買的服務級別協定(SLA)。 例如，一個方案可代表AEM資源以支援組織的公開網站，而另一個方案則代表內部DAM。


看這個 [影片](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) 進一步了解使用Cloud Manager計畫。

使用者可以建立 **沙箱** 或 **生產** 程式。

* A **生產計畫** 會建立，以便在未來的適當時間啟用即時流量。
   * 請參閱該文檔 [生產計畫簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) 以取得更多詳細資訊。

* A **沙箱方案** 通常建立的目的是提供培訓、運行演示、培訓、建立POC或文檔。
   * 它不是用來傳輸即時流量，且會有生產計畫無法使用的限制。
   * 其中包含Sites和Assets，且會以Git分支自動填入，該分支包含范常式式碼、開發環境和非生產管道。
   * 請參閱該文檔 [沙箱方案簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) 以取得更多詳細資訊。

## Cloud Manager環境 {#cloud-manager-environments}

您的雲端環境將透過Cloud Manager建立、存取及檢視。 這些環境可以是生產、測試或開發環境。 不同的環境有不同的用途，可搭配不同的CI/CD管道使用。 環境由下列服務組成：

* [AEM Authoring Services](#author-services)
* [AEM Publishing Services](#publish-services)
* [Dispatcher服務](#dispatcher-services)

>[!TIP]
>
> 請參閱影片 [使用AdobeCloud Manager環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) 可用環境的概觀。
>
>請參閱檔案 [管理環境](/help/implementing/cloud-manager/manage-environments.md) 若要進一步了解使用者可建立的環境類型，以及使用者如何建立環境。

### AEM Authoring Service {#author-services}

在建立、管理及更新網站內容和數位資產的環境中，會包含AEM製作服務。 通常只有內部使用者能存取製作服務，並會在登入畫面後面維護。 製作服務可同時作為製作和預覽環境。

### AEM Publishing Service {#publish-services}

托管一般使用者體驗的環境（例如網站）中包含AEM發佈服務。 這是網站訪客將檢視並與之互動的服務。 發佈服務通常可公開使用。

### AEM Dispatcher服務 {#dispatcher-services}

Dispatcher是 `Apache HTTP Web server` 提供安全性與效能層，且位於AEM發佈服務之前的模組。
