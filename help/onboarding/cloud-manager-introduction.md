---
title: Cloud Manager 簡介
description: 了解 Cloud Manager 如何透過其程序、環境和管道支援您的 AEM 專案。
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 2d793f22e554c2a4bde8831b5053d1640ba07c70
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 100%

---

# Cloud Manager 簡介 {#intro-cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要元件，可作為您團隊的單一入口點。其專門構建的 CI/CD 管道可確保進行徹底的測試和最高的計劃碼品質，從而提供卓越的體驗。為確保客戶能夠快速啟動他們的項目，Cloud Manager 以自助方式提供所需的一切，包括建立您的 cloud 資源和環境以及存取您的 git 存放庫的能力。這些功能支援企業開發設定，因此團隊可以致力於頻繁提交更改、快速提供卓越的數字體驗並加快實現價值的時間。

您的系統管理員負責建立您的 Cloud Manager 團隊，其中包括將建立您的 cloud 資源和開發人員的個人。有關如何設定和擴展您的企業開發團隊以及了解 AEM as a Cloud Service 如何支援您的開發流程的更多資訊，請參閱文件[AEM as a Cloud Service 的企業團隊開發設定。](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)

## 瀏覽到 Cloud Manager 的概覽頁面 {#navigate-cloud-manager}

依照這些步驟操作即可前往 Cloud Manager。

1. 瀏覽至 [`https://my.cloudmanager.adobe.com` Cloud Manager 登入頁面的概覽頁面。](https://my.cloudmanager.adobe.com/)

1. 從 Cloud Manager 中選擇程序&#x200B;**程序和產品**&#x200B;頁面啟動&#x200B;**總覽**&#x200B;頁。

您還可以按照以下步驟從 Adobe Experience Cloud 主頁瀏覽到 Cloud Manager 的程序和產品頁面。

1. 導覽至 [`https://experience.adobe.com`](https://experience.adobe.com) 的 Adobe Experience Cloud 並使用您的 Adobe ID 憑證登入。

1. 透過參考工具欄右上角顯示的組織名稱，確保您在正確的組織中。

1. 選擇&#x200B;**Experience Manager**。

1. 在&#x200B;**Cloud Manager**&#x200B;卡片，點擊&#x200B;**啟動**

## Cloud Manager 中基於角色的權限 {#role-based-permissions}

| 權限 | 說明 | 企業所有者 | 部署管理員 | 方案管理員 | 開發人員 |
|--- |--- |--- |--- |--- |--- |
| 新增程序<br>編輯程序 | 新增新程序<br>新增或刪除解決方案或附加組件 | x |  |  |  |
| 建立環境 | 建立生產+登台和開發環境 | x | x |  |  |
| 更新環境 | 更新生產+登台和開發環境 | x | x |  |  |
| 刪除裝置環境 | 刪除開發環境 | x | x |  |  |
| 管道設定 | 設定和編輯管道 |  | x |  |  |
| 管道執行 | 啟動管道 | x | x |  |  |
| 管道執行 | 拒絕/核准重要第三級品質閘道失敗 | x | x | x |  |
| 管道執行 | 提供上線核准 | x | x | x |  |
| 管道執行 | 生產部署排程 | x | x | x |  |
| 管道刪除 | 允許管道刪除 |  | x |  |  |
| 執行取消 | 取消目前的執行 |  | x |  |  |
| 產生個人存取權杖 | 存取 Git |  | x |  | x |

>[!NOTE]
>
>可以將一個使用者指派給多個角色。例如，同時指派&#x200B;**業務負責人**&#x200B;和&#x200B;**部署管理員**&#x200B;角色以賦予使用者的所有權限。

## Cloud Manager 計劃 {#cloud-manager-programs}

Cloud Manager 程序表示支援業務計劃的邏輯分組的 Cloud Manager 環境集。這些分組通常對應於購買的服務水平協議 (SLA)。例如，一個程序可能代表 AEM 資源以支援組織的公共網站，而另一個程序代表內部 DAM。


請觀看這段[影片](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=zh-Hant)了解有關使用 Cloud Manager 計劃的更多資訊。

使用者可以建立&#x200B;**沙箱**&#x200B;或&#x200B;**生產**&#x200B;計畫。

* 一個&#x200B;**生產計劃**&#x200B;是為了在未來的適當時間啟用實時流量而建立的。
   * 如需了解詳細資訊，請參閱文件：[生產計畫簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)。

* **沙箱計畫**&#x200B;通常建立的目的是提供培訓、執行示範、訓練、建立 POC 或文件。
   * 這不代表能承載即時流量，並且會有生產計畫沒有的限制。
   * 其中包含 Sites 和 Assets，且會透過 Git 分支自動填入，分支中包含範例計劃碼、開發環境及非生產管道。
   * 如需了解詳細資訊，請參閱文件：[沙箱計畫簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。

## Cloud Manager 環境 {#cloud-manager-environments}

您的雲端環境將透過 Cloud Manager 建立、存取和查看。環境包含生產、測試和開發。不同的環境有不同的用途，可以與不同的 CI/CD 管道一起使用。環境由以下服務組成：

* [AEM 創作服務](#author-services)
* [AEM 出版服務](#publish-services)
* [Dispatcher 服務](#dispatcher-services)

>[!TIP]
>
> 參考視頻[使用 Adobe Cloud Manager 環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=zh-Hant)可用環境的概覽。
>
>參考文件[管理環境](/help/implementing/cloud-manager/manage-environments.md)了解有關使用者可以建立的環境類型以及使用者如何建立環境的更多資訊。

### AEM 創作服務 {#author-services}

AEM 創作服務包含在建立、管理和更新網站內容和數位資產的環境中。通常只有內部使用者才能存取創作服務，並且在登入畫面後面進行維護。授權服務可作為創作和預覽環境。

### AEM 出版服務 {#publish-services}

AEM 發布服務包含在託管最終使用者體驗的環境中，例如網站。這是網站訪客將查看並與之交互的服務。通常，發布服務是公開可用的。

### AEM Dispatcher 服務 {#dispatcher-services}

Dispatcher 是一個`Apache HTTP Web server`提供位於 AEM 發布服務前面的安全和效能層的模組。
