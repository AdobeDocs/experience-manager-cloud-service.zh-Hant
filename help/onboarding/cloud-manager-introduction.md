---
title: Cloud Manager 簡介
description: 瞭解Cloud Manager如何通過其程AEM序、環境和管道支援您的項目。
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 2d793f22e554c2a4bde8831b5053d1640ba07c70
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 4%

---

# Cloud Manager 簡介 {#intro-cloud-manager}

雲管理器是as a Cloud Service的AEM重要元件，是您團隊的單一入口點。 其專門構建的CI/CD管道可確保徹底的測試和最高的代碼質量，以提供卓越的體驗。 為確保客戶能夠快速啟動其項目，Cloud Manager以自助方式提供所需的一切，包括建立雲資源和環境並訪問您的Git儲存庫的能力。 這些功能支援企業開發設定，使團隊能夠努力頻繁地進行更改、快速提供卓越的數字型驗，並加快價值實現。

您的系統管理員負責設定雲管理器團隊，該團隊將包括將建立雲資源和開發人員的個人。 有關如何設定和擴展企業開發團隊以及瞭解AEMas a Cloud Service如何支援您的開發流程的詳細資訊，請參閱文檔 [用於AEMas a Cloud Service的Enterprise Team Development Setup。](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)

## 導航至Cloud Manager的概述頁 {#navigate-cloud-manager}

按照以下步驟導航至Cloud Manager。

1. 導航至Cloud Manager的登錄頁，網址為 [`https://my.cloudmanager.adobe.com`。](https://my.cloudmanager.adobe.com/)。

1. 從雲管理器的 **計畫和產品** 頁 **概述** 的子菜單。

您也可以通過以下步驟從Adobe Experience Cloud首頁導航到Cloud Manager的「程式和產品」頁面。

1. 導航到Adobe Experience Cloud，地址為 [`https://experience.adobe.com`](https://experience.adobe.com) 用你的Adobe ID登錄。

1. 通過參考工具欄右上角顯示的組織名稱，確保您處於正確的組織中。

1. 選擇 **Experience Manager**。

1. 在 **雲管理器** 卡，按一下 **啟動**

## 雲管理器中基於角色的權限 {#role-based-permissions}

| 權限 | 說明 | 業務所有者 | 部署管理器 | 程式管理器 | 開發人員 |
|--- |--- |--- |--- |--- |--- |
| 添加程式<br>編輯程式 | 添加新程式<br>添加或刪除解決方案或載入項 | x |  |  |  |
| 建立環境 | 建立生產+暫存和開發環境 | x | x |  |  |
| 更新環境 | 更新生產+暫存和開發環境 | x | x |  |  |
| 刪除開發環境 | 刪除開發環境 | x | x |  |  |
| 管道設定 | 設定和編輯管線 |  | x |  |  |
| 管道執行 | 啟動管線 | x | x |  |  |
| 管道執行 | 拒絕/批准重要的3層質量網關故障 | x | x | x |  |
| 管道執行 | 提供即時批准 | x | x | x |  |
| 管道執行 | 計畫生產部署 | x | x | x |  |
| 管道刪除 | 允許管道刪除 |  | x |  |  |
| 執行取消 | 取消當前執行 |  | x |  |  |
| 生成個人訪問令牌 | 訪問Git |  | x |  | x |

>[!NOTE]
>
>用戶可以分配到多個角色。 例如，同時分配 **業務所有者** 和 **部署管理器** 角色給用戶這些權限的總和。

## 雲管理器程式 {#cloud-manager-programs}

Cloud Manager程式表示支援業務計畫邏輯分組的Cloud Manager環境集。 這些分組通常對應於購買的服務級別協定(SLA)。 例如，一個程式可以表示支AEM持組織公共網站的資源，而另一個程式則表示內部DAM。


看這個 [視頻](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) 瞭解有關使用Cloud Manager程式的更多資訊。

用戶可以建立 **沙盒** 或 **生產** 的子菜單。

* A **生產程式** 將建立為在將來的適當時間啟用即時通信。
   * 請參閱文檔 [生產計畫簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) 的子菜單。

* A **沙盒程式** 通常建立目的是為培訓、運行演示、支援、建立POC或文檔提供服務。
   * 它不是用來承載即時流量的，而且會有一些限制，而製作程式是不會這樣做的。
   * 它包括站點和資產，並由自動填充的git分支提供，該分支包括示例代碼、開發環境和非生產管道。
   * 請參閱文檔 [沙盒程式簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) 的子菜單。

## 雲管理器環境 {#cloud-manager-environments}

您的雲環境將通過雲管理器建立、訪問和查看。 這些環境可以是生產、轉移或開發環境。 不同的環境用於不同的目的，可以與不同的CI/CD管道一起使用。 環境由以下服務組成：

* [創作AEM服務](#author-services)
* [發AEM布服務](#publish-services)
* [Dispatcher服務](#dispatcher-services)

>[!TIP]
>
> 請參閱視頻 [使用Adobe雲管理器環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) 概述可用環境。
>
>請參閱文檔 [管理環境](/help/implementing/cloud-manager/manage-environments.md) 瞭解有關用戶可以建立的環境類型以及用戶如何建立環境的詳細資訊。

### 創作AEM服務 {#author-services}

創AEM作服務包括在建立、管理和更新站點內容和數字資產的環境中。 通常，只有內部用戶才能訪問創作服務，並在登錄螢幕後進行維護。 創作服務充當創作和預覽環境。

### 發AEM布服務 {#publish-services}

發佈AEM服務包括在承載最終用戶體驗的環境中，如網站。 這是站點訪問者將查看並與之交互的服務。 通常，發佈服務是公開的。

### 調度AEM服務 {#dispatcher-services}

調度程式是 `Apache HTTP Web server` 模組，提供位於發佈服務前面的安全性和性AEM能層。
