---
title: AEM as a Cloud Service SDK
description: Cloud Service軟AEM件開發工具包概述
translation-type: tm+mt
source-git-commit: 6b754a866be7979984d613b95a6137104be05399
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# The AEM as aCloud ServiceSDK {#aem-as-a-cloud-service-sdk}

作AEM為Cloud ServiceSDK由以下對象組成：

* **快速入門Jar**  —— 用於本AEM地開發的運行時
* **Java API Jar**  - Java Jar/Maven Dependency，它公開所有允許的Java API，可用來開發作為AEMCloud Service。先前稱為Uberjar
* **Javadoc Jar**  - Java API Jar的javadoc
* **Dispatcher Tools**  —— 用於對Dispatcher進行本地開發的工具集。Unix和Windows的不同對象

此外，某些先前部署為6.5或更AEM舊版本的客戶會使用下列物件。 如果本地編譯無法與快速啟動jar一起使用，並且您懷疑是由於介面已從作為Cloud Service的部AEM署中刪除，請聯繫客戶支援以確定您是否需要訪問。 這需要在後端進行變更。

* **6.5已過時的Java API Jar**  —— 自6.5以來已移除的另AEM一組介面
* **6.5不建議使用的Javadoc Jar**  —— 用於其他介面集的Javadoc

## 建立SDK {#building-for-the-sdk}

The AEM as aCloud ServiceSDK is used to build and deploy custom code. 有關詳細資訊，請參考[AEM Project Archetype文檔](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en)。 從高度來看，將執行以下步驟：

* **編譯代碼**。如預期，會編譯原始碼，並產生產生的內容封裝
* **建立工件**。在此過程中將生成對象
* **分析組合**。使用Maven分析器外掛程式來分析Bundles，它會尋找Maven專案中的問題，例如缺少相依性
* **部署對象**。對象將部署到本地伺服器。

部署至雲端環境時，Cloud Manager會執行相同的步驟。 在本端執行建置可讓開發人員進行本端開發和測試，讓開發人員在提交至原始碼控制並觸發Cloud Manager部署之前，能夠更有效率地發現程式碼或結構性問題，而Cloud Manager部署可能需要更長的時間。

## 以Cloud ServiceAEMSDK {#accessing-the-aem-as-a-cloud-service-sdk}的身分存取

* 您可以檢AEM查Admin Console的&#x200B;**關於Adobe Experience Manager**&#x200B;圖示，以瞭解您正在生產AEM中執行的版本。
* 快速啟動jar和Dispatcher Tools可以從[軟體分發入口](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載為zip檔案。 請注意，SDK清單的存取權限僅限於擁有AEMManaged Services或AEMCloud Service環境的使用者。
* Java API Jar和Javadoc Jar可通過任意工具（命令行或首選IDE）下載。
* 主要專案應參考下列API Jar套件。 在任何子包中也應引用此相關性。

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
>SDK的版本項目應與版本的版AEM本相符為Cloud Service。 您可以登入，然後移至畫面右上角的問號，並選取「關於Adobe Experience Manager」AEM **[!UICONTROL ，以瞭解您使用的版本]**


## 使用新的SDK版本{#refreshing-a-local-project-with-a-new-skd-version}重新整理本機專案

建議何時使用新的SDK重新整理本機專案？

建議至少在每月維護髮行後重新整理它。**

在任何每日維護髮行後重新整理它是&#x200B;*optional*。 當其生產實例成功升級至新版本時，將通知客戶。 對於每日維護髮行，新SDK預計不會大幅變更（如果完全變更）。 不過，建議您偶爾使用最新的SDK來重新整AEM理本機開發人員環境，然後重建並測試自訂應用程式。 每月維護髮行通常包含更具影響力的變更，因此開發人員應立即重新整理、重建和測試。

以下是刷新本地環境的建議過程：

1. 請確定任何有用的內容已提交至來源控制中的專案，或是可變內容套件中的可用內容，以供稍後匯入
1. 本端開發測試內容需要個別儲存，以免部署在Cloud Manager管道建置中。 因為只要用於地方開發
1. 停止當前正在運行的快速啟動
1. 將`crx-quickstart`資料夾移至其他資料夾以保全
1. 請注意Cloud Manager中AEM注明的新版本（此版本將用於標識要進一步下載的新QuickStart Jar版本）
1. 從軟體分發門戶下載其版本與生AEM產版本匹配的QuickStart JAR
1. 建立全新資料夾，並將新的QuickStart Jar放入
1. 使用所需的執行模式（重新命名檔案或透過`-r`傳入執行模式）啟動新的QuickStart。
   * 請確定資料夾中沒有舊快速啟動的殘餘部分。
1. 建立您的應AEM用程式
1. 透過PackageManager將您AEM的應用程式部AEM署至本機
1. 安裝通過PackageManager進行本地環境測試所需的任何可變內容包
1. 視需要繼續開發和部署變更

如果每個新的快速入門版本都應安裝AEM內容，請將其包含在內容包中，並在項目的原始碼控制中。 然後，每次安裝。

建議您頻繁更新SDK（例如每週兩次），並每日處置完整的本機狀態，以免意外依賴應用程式中的狀態資料。

如果您依賴CryptoSupport([，通過在中配置Cloudservices或SMTP郵件服務的憑據AEM，或通過在應用程式](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/granite/crypto/CryptoSupport.html)中使用CryptoSupport API)，則加密的屬性將通過在環境的第一個啟動時自動生成的密鑰進行加AEM密。 在雲設定負責自動重用特定環境的CryptoKey的同時，還需要將密鑰注入到本地開發環境中。

預設AEM配置為將密鑰資料儲存在資料夾的資料資料夾內，但為了便於在開發中重複使用，可AEM以使用&quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;在首次啟動時初始化該進程。 這將在&quot;`/etc/key`&quot;處生成加密資料。

若要重複使用包含加密值的內容套件，您必須依照下列步驟進行：

* 當您最初啟動本地quickstart.jar時，請確保添加以下參數：&quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;。 建議您隨時新增，但選購。
* 第一次啟動實例時，建立包時包含根&quot;`/etc/key`&quot;過濾器。 這將保留機密，以便在您希望重新使用的所有環境中重複使用
* 匯出任何包含機密的可變內容，或透過`/crx/de`查找加密值，將其新增至將在安裝期間重複使用的套件
* 每當您啟動新執行個體（要取代為新版本或多個開發環境應共用測試憑證）時，請安裝步驟2和3中產生的套件，以便能夠重複使用內容，而不需手動重新設定。 這是因為現在加密密鑰正在同步。
