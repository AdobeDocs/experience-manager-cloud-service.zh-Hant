---
title: 瞭解什麼是雲管理器
description: 按照本頁瞭解Cloud Manager、Cloud Manager程式和環境。
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: c206bc241bccf6f8a5bfb4946d6231f53438861a
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 3%

---

# Cloud Manager 簡介 {#intro-cloud-manager}

雲管理器是as a Cloud Service的AEM重要元件，是您團隊的單一入口點。

為了支援具有企業開發設定的客戶，AEMas a Cloud Service與Cloud Manager及其專門構建的CI/CD管道完全整合，這些管道旨在確保全面測試和最高代碼質量，以提供卓越的體驗。

為確保客戶可以從AEMas a Cloud Service快速開始，Cloud Manager以自助方式提供啟動所需的一切，包括建立雲資源和環境的能力。 這樣，您的開發AEM人員就可以通過雲管理器訪問Git儲存庫。 使用Cloud Manager，開發團隊可以以自助方式頻繁執行更改。

您的系統管理員將負責設定您的雲管理器團隊，該團隊將包括將建立雲資源和開發人員的個人。 請參閱 [針對AEMas a Cloud Service的企業團隊開發設定](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md) 瞭解Cloud Manager如何在企業團隊開發設定中支援。

## 導航至Cloud Manager的概述頁 {#navigate-cloud-manager}

按照以下步驟導航至Cloud Manager:

1. 從直接導航到Cloud Manager的登錄頁 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)。

   >[!NOTE]
   >請將此頁面加入書籤以供將來參考，並幫助您直接導航至Cloud Manager的登錄頁。

1. 從雲管理器的 **計畫和產品** 頁 **概述** 的子菜單。

此外，您還可以從Adobe Experience Cloud首頁導航至Cloud Manager的「程式和產品」頁面。 請遵循下列步驟：

1. 直接導航到 [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) 用你的Adobe ID登錄。

1. 選擇 **Experience Manager**。

1. 按一下 **啟動** 從Cloud Manager卡中。 成功登錄到雲管理器後，您就可以使用用戶介面(UI)。

   成功登錄後，您將被定向到Cloud Manager的登錄頁。

## 雲管理器中基於角色的權限 {#role-based-permissions}

| 權限 | 說明 | 業務所有者 | 部署管理器 | 程式管理器 | 開發人員 |
|--- |--- |--- |--- |--- |--- |
| 添加程式<br>編輯程式 | 添加新程式。<br>編輯程式 — 添加或刪除解決方案或載入項 | x |  |  |  |
| 建立環境 | 建立Prod+Stage、Dev、環境。 | x | x |  |  |
| 更新環境 | 更新Prod+Stage、Dev、環境。 | x | x |  |  |
| 刪除開發環境 | 刪除開發環境。 | x | x |  |  |
| 管道設定 | 設定或編輯管線。 |  | x |  |  |
| 管道執行 | 啟動管線。 | x | x |  |  |
| 管道執行 | 拒絕/批准重要的3層故障。 | x | x | x |  |
| 管道執行 | 提供GoLive批准。 | x | x | x |  |
| 管道執行 | 計畫生產部署。 | x | x | x |  |
| 管道刪除 | 允許刪除管線。 |  | x |  |  |
| 執行取消 | 取消當前執行。 |  | x |  |  |
| 生成個人訪問令牌 | 訪問Git。 |  | x |  | x |

>[!NOTE]
>用戶可以分配到多個角色。 例如，將業務所有者和部署管理器角色分配給用戶時，會為用戶提供這些權限的組合或總和。

## 雲管理器程式 {#cloud-manager-programs}

Cloud Manager程式表示支援業務計畫邏輯集的Cloud Manager環境集，通常對應於購買的服務級別協定(SLA)。 例如，一個方案可以代表支援AEM全球公共網站的資源，而另一個方案則代表一個內部中央資料庫。 看這個 [視頻](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en) 瞭解有關使用Cloud Manager程式的更多資訊。

用戶可以建立 **沙盒** 或 **生產** 的子菜單。

* A *生產計畫* 將建立為在將來的適當時間啟用即時通信。
請參閱 [生產計畫簡介](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/production-programs/introduction-production-programs.html?lang=en) 的子菜單。

* A *沙盒程式* 通常建立目的是為培訓、運行演示、支援、POC或文檔提供服務。 它不是用來承載即時流量的，並且將具有生產計畫所不能的限制。 它將包括站點和資產，並將自動填充包含示例代碼、開發環境和非生產管道的Git分支。
請參閱 [沙盒程式簡介](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sandbox-programs/introduction-sandbox-programs.html?lang=en) 的子菜單。

## 雲管理器環境 {#cloud-manager-environments}

您的雲環境將通過雲管理器建立、訪問和查看。 這些環境可以是生產環境、階段環境或開發環境。 不同的環境支援不同的用途，可以使用不同的CI/CD管道進行使用。 環境由以下服務組成：

* [AEM作者服務](#author-services)
* [AEM發佈服務](#publish-services)
* [Dispatcher服務](#dispatcher-services)

   >[!NOTE]
   > 請參閱視頻 [使用Adobe雲管理器環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager) 瞭解有關可用環境的詳細資訊。 此外，請參見 [管理環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en) 瞭解有關用戶可以建立的環境類型以及用戶如何建立環境的詳細資訊。

### AEM作者服務 {#author-services}

AEM作者服務包含在建立、管理和更新站點內容和數字資產的環境中。 通常，只有內部用戶才有權訪問作者服務，並且位於登錄螢幕後。 創作服務設計為創作和預覽環境。

### AEM發佈服務 {#publish-services}

AEM發佈服務包含在承載最終用戶體驗的環境中，如網站。 這是站點訪問者將查看並與之交互的服務。 通常，發佈服務是公開的。

### 調度AEM服務 {#dispatcher-services}

調度程式是 `Apache HTTP Web server` 提供AEM發佈服務前面的安全性和效能層的模組。
