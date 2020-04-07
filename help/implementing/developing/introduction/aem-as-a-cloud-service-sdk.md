---
title: AEM 雲端服務 SDK
description: '待完成 '
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# The AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

AEM as a Cloud Service SDK由下列物件組成：

* **Quickstart Jar** —— 用於本機開發的AEM執行時期
* **Java API Jar** - Java Jar/Maven Dependency，它公開所有可用來針對AEM進行開發的Java API（如雲端服務）。 先前稱為Uberjar
* **Javadoc Jar** - Java API Jar的javadoc
* **Dispatcher Tools** —— 用於對Dispatcher進行本地開發的工具集。 Unix和Windows的不同對象

此外，有些先前部署有AEM 6.5或更舊版本的客戶會使用下列物件。 如果本機編譯無法與Quickstartjar搭配使用，而您懷疑是由於已從AEM移除的介面，而且已部署為雲端服務，請聯絡客戶支援以判斷您是否需要存取。 這需要在後端進行變更。

* **6.5已過時的Java API Jar** —— 自AEM 6.5以來已移除的另一組介面
* **6.5不建議使用的Javadoc Jar** —— 用於其他介面集的Javadoc

## 以雲端服務SDK形式存取AEM {#accessing-the-aem-as-a-cloud-service-sdk}

* 您可以勾選AEM Admin Console的「關於 **Adobe Experience Manager** 」圖示，以瞭解您正在生產環境中執行的AEM版本。
* 快速啟動jar和Dispatcher Tools可從軟體分發入口網站下載為 [zip檔案](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)。 請注意，SDK清單的存取權限僅限於AEM Managed Services或AEM做為雲端服務環境的使用者。
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

> [!NOTE] SDK的版本項目應符合AEM的雲端服務版本。 您可以登入AEM，然後移至畫面右上角的問號並選取「關於 **[!UICONTROL Adobe Experience Manager」，以瞭解您使用的版本]**

* 裝載包的主儲存庫的遠程協調應包括在pom檔案中。

```
<repository>
    <id>adobe-aem-releases</id>
    <name>Adobe AEM Repository</name>
    <url>https://downloads.experiencecloud.adobe.com/content/maven/public</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

## 使用新的SDK版本重新整理本機專案 {#refreshing-a-local-prokect-with-a-new-skd-version}

建議何時使用新的SDK重新整理本機專案？

建議您 *至少在每月* 維護髮行後重新整理它。

在任何每日 *維護髮行* 後，都可選擇重新整理它。 當其生產實例已成功升級至新的AEM版本時，將會通知客戶。 對於每日維護髮行，新SDK預計不會大幅變更（如果完全變更）。 不過，建議您偶爾使用最新的SDK重新整理本機AEM開發人員環境，然後重建並測試自訂應用程式。 每月維護髮行通常包含更具影響力的變更，因此開發人員應立即重新整理、重建和測試。

以下是刷新本地環境的建議過程：

1. 請確定任何有用的內容已提交至來源控制中的專案，或是可變內容套件中的可用內容，以供稍後匯入
1. 本端開發測試內容需要個別儲存，以免部署在Cloud Manager管道建置中。 因為只要用於地方開發
1. 停止當前正在運行的快速啟動
1. 將資料 `crx-quickstart` 夾移至其他資料夾以保全
1. 請注意Cloud Manager中已注明的新AEM版本（此版本將用於識別要進一步下載的新QuickStart Jar版本）
1. 從軟體散發入口網站下載其版本與Production AEM版本相符的QuickStart JAR
1. 建立全新資料夾，並將新的QuickStart Jar放入
1. 以所需的執行模式（重新命名檔案或透過傳入執行模式）啟動新的快速 `-r`啟動。
   * 請確定資料夾中沒有舊快速啟動的殘餘部分。
1. 建立您的AEM應用程式
1. 透過PackageManager將您的AEM應用程式部署至本機AEM
1. 安裝通過PackageManager進行本地環境測試所需的任何可變內容包
1. 視需要繼續開發和部署變更

如果每個新AEM快速入門版本都應安裝內容，請將它加入內容套件，並納入專案的來源控制項中。 然後，每次安裝。

建議您頻繁更新SDK（例如每週兩次），並每日處置完整的本機狀態，以免意外依賴應用程式中的狀態資料。

如果您依賴CryptoSupport([透過在AEM中設定Cloudservices或SMTP Mail服務的憑證，或在應用程式中使用CryptoSupport API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html))，加密的屬性將會以在AEM環境的第一個啟動時自動產生的金鑰加密。 在雲設定負責自動重用特定環境的CryptoKey的同時，還需要將密鑰注入到本地開發環境中。

依預設，AEM會設定為將關鍵資料儲存在資料夾的資料夾中，但為方便在開發中重複使用，AEM程式可在首次啟動時以「`-Dcom.adobe.granite.crypto.file.disable=true`」初始化。 這將在&quot;`/etc/key`&quot;生成加密資料。

若要重複使用包含加密值的內容套件，您必須依照下列步驟進行：

* 當您最初啟動本地quickstart.jar時，請確保添加以下參數：「`-Dcom.adobe.granite.crypto.file.disable=true`」。 建議您隨時新增，但選購。
* 您第一次啟動例項時，會建立包含根&quot;`/etc/key`&quot;篩選的套件。 這將保留機密，以便在您希望重新使用的所有環境中重複使用
* 匯出任何包含機密的可變內容，或透過查找加密值，將 `/crx/de` 其新增至將在安裝後重複使用的套件
* 每當您啟動新執行個體（要取代為新版本或多個開發環境應共用測試憑證）時，請安裝步驟2和3中產生的套件，以便能夠重複使用內容，而不需手動重新設定。 這是因為現在加密密鑰正在同步。