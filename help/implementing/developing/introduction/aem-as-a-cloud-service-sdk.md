---
title: AEM as a Cloud Service SDK
description: as a Cloud Service軟體開AEM發工具包概述
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 1%

---

# AEMas a Cloud ServiceSDK {#aem-as-a-cloud-service-sdk}

AEMas a Cloud ServiceSDK包括以下對象：

* **快速啟動Jar**  — 用於本AEM地開發的運行時
* **Java API Jar** - Java Jar/Maven Dependency，它顯示所有允許的Java API，這些API可用於開發，AEM作為Cloud Service。 以前稱為Uberjar
* **Javadoc Jar** - Java API Jar的javadoc
* **Dispatcher工具**  — 用於針對Dispatcher進行本地開發的工具集。 Unix和Windows的獨立對象

此外，以前部署了6.5或更AEM低版本的某些客戶將使用以下對象。 如果本地編譯不能與Quickstart jar一起使用，並且您懷疑是由於從已部署的as a Cloud Service中刪除的介面AEM，請聯繫客戶支援以確定您是否需要訪問。 這將需要後端更改。

* **6.5不建議使用的Java API Jar**  — 自6.5版起已移除的另AEM一組介面
* **6.5不建議使用的Javadoc Jar** - Javadocs，用於附加的介面集

## 生成SDK {#building-for-the-sdk}

as a Cloud ServiceAEMSDK用於生成和部署自定義代碼。 有關詳細資訊，請參閱 [項AEM目原型文檔](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en)。 在高級別上，將執行以下步驟：

* **編譯代碼**。 如預期，編譯原始碼，生成生成的內容包
* **生成對象**。 在此過程中生成對象
* **分析捆綁包**。 使用Maven分析器插件分析捆綁包，該插件會查找Maven項目中的問題，如缺少依賴項
* **部署對象**。 對象將部署到本地伺服器。

部署到雲環境時，雲管理器會執行相同的步驟。 在本地執行構建可進行本地開發和測試，因此開發人員可以在提交原始碼控制和觸發Cloud Manager部署之前很早就高效地發現代碼或結構問題，這可能需要更長的時間。

## 訪問AEMas a Cloud ServiceSDK {#accessing-the-aem-as-a-cloud-service-sdk}

* 你可以查AEM查Admin Console **關於Adobe Experience Manager** 表徵圖，以查AEM明您正在生產中運行的版本。
* 快速啟動jar和Dispatcher Tools可以作為zip檔案從 [軟體分發門戶](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)。 請注意，對SDK清單的訪問限於具有AEMManaged Services或AEMas a Cloud Service環境。
* Java API Jar和Javadoc Jar可通過多種工具（命令行或首選IDE）下載。
* 主項目窗體應引用以下API Jar包。 任何子軟體包中也應引用此依賴關係。

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version>
  <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>SDK的版本項應與as a Cloud Service的版本相AEM匹配。 通過登錄到，然後轉到螢幕右上角的問AEM號並選擇，您可以查看您使用的版本 **[!UICONTROL 關於Adobe Experience Manager]**


## 使用新SDK版本刷新本地項目 {#refreshing-a-local-project-with-a-new-skd-version}

建議何時使用新SDK刷新本地項目？

是 *建議* 以至少在每月維護版本後刷新它。

是 *可選* 以在任何日常維護版本後刷新它。 當客戶的生產實例已成功升級到新版本時，將通知AEM客戶。 對於每日維護版本，新SDK不會發生重大更改（如果完全更改）。 不過，建議偶爾使用最新的SDKAEM刷新本地開發人員環境，然後重建和test自定義應用程式。 每月維護版本通常包括更有影響的更改，因此開發人員應立即刷新、重建和test。

以下是刷新本地環境的建議步驟：

1. 確保將任何有用內容提交到原始碼管理中的項目，或在可變內容包中提供以供以後導入
1. 本地開發test內容需要單獨儲存，以便不將其部署為Cloud Manager管道構建的一部分。 因為只要用於地方開發
1. 停止當前正在運行的快速啟動
1. 移動 `crx-quickstart` 資料夾到其他資料夾以保存安全
1. 請注意Cloud ManagerAEM中注明的新版本（此版本將用於標識要進一步下載的新QuickStart Jar版本）
1. 從軟體分發門戶下載其版本與AEM生產版本匹配的QuickStart JAR
1. 建立全新資料夾並將新的QuickStart Jar放入
1. 使用所需運行模式(更名檔案或通過 `-r`)。
   * 確保資料夾中沒有舊快速啟動的殘餘。
1. 構建應用程AEM序
1. 通過PackageManager將AEM應用程式部署到AEM本地
1. 通過PackageManager安裝本地環境測試所需的任何可變內容包
1. 根據需要繼續開發和部署更改

如果每個新快速入門版本都應安裝AEM內容，請將其包含到內容包中，並包含在項目的原始碼管理中。 然後，每次安裝。

建議您頻繁更新SDK（例如每週兩次），並每天處理完整的本地狀態，以免意外依賴於應用程式中的狀態資料。

以防您依賴CryptoSupport([通過在中配置Cloudservices或SMTP郵件服務的憑據，或AEM者在應用程式中使用CryptoSupport API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html))，加密的屬性將通過在環境的第一個開始時自動生成的密鑰進AEM行加密。 在雲設定負責自動重用特定環境的CryptoKey的同時，需要將密鑰注入到本地開發環境中。

預設AEM情況下，配置為將關鍵資料儲存在資料夾的資料資料夾中，但為了便於在開發中重新使用，該進AEM程可在首次啟動時使用「`-Dcom.adobe.granite.crypto.file.disable=true`。 這將在「」處生成加密資料`/etc/key`。

要能夠重新使用包含加密值的內容包，您需要執行以下步驟：

* 初始啟動本地quickstart.jar時，請確保添加以下參數：&quot;`-Dcom.adobe.granite.crypto.file.disable=true`。 建議始終添加它，但是可選。
* 首次啟動實例時，建立包時，該包包含根&#39;&#39;的篩選器`/etc/key`。 這將保留機密，以便在您希望其重新使用的所有環境中重複使用
* 導出包含機密的任何可變內容，或通過 `/crx/de` 將其添加到將在安裝中重複使用的包中
* 只要啟動新實例（要替換為新版本，或者多個開發環境應共用用於測試的憑據），請安裝步驟2和步驟3中生成的包，以便能夠重新使用內容而無需手動重新配置。 這是因為現在加密密鑰處於同步狀態。
