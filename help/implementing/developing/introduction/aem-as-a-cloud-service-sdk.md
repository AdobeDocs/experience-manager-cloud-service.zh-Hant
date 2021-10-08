---
title: AEM as a Cloud Service SDK
description: AEMas a Cloud Service軟體開發套件概述
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# AEMas a Cloud ServiceSDK {#aem-as-a-cloud-service-sdk}

AEMas a Cloud ServiceSDK包含下列成品：

* **Quickstart Jar**  — 用於本機開發的AEM執行階段
* **Java API Jar**  — 公開所有允許的Java API(可用來針對AEM進行開發作為Cloud Service)的Java Jar/Maven相依性。先前稱為Uberjar
* **Javadoc Jar**  - Java API Jar的javadoc
* **Dispatcher工具**  — 用來針對本機Dispatcher開發的工具集。Unix和Windows的獨立對象

此外，有些先前透過AEM 6.5或更舊版本部署的客戶將使用下列成品。 如果本地編譯不能與Quickstart Jar一起使用，並且您懷疑是由於已從AEM部署的as a Cloud Service中刪除的介面，請聯繫客戶支援以確定您是否需要訪問。 這需要在後端進行變更。

* **6.5已棄用的Java API Jar**  — 自AEM 6.5起已移除的額外介面集
* **6.5已棄用的Javadoc Jar**  — 用於其他介面集的Javadoc

## 為SDK建置 {#building-for-the-sdk}

AEMas a Cloud ServiceSDK可用來建置和部署自訂程式碼。 如需詳細資訊，請參閱[AEM專案原型檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en)。 從高度來說，會執行下列步驟：

* **編譯程式碼**。如預期，會編譯原始碼，產生產生的內容套件
* **建立成品**。在此過程中將生成對象
* **分析套件組合**。使用Maven分析器外掛程式分析套件組合，該外掛程式會尋找Maven專案中的問題，例如缺少相依性
* **部署成品**。對象已部署到本地伺服器。

部署至雲端環境時，Cloud Manager會執行相同步驟。 在本機執行組建可進行本機開發和測試，讓開發人員在提交至原始碼控制項及觸發Cloud Manager部署前，即可先有效探索程式碼或結構問題，但可能需要更久的時間。

## 存取AEMas a Cloud ServiceSDK {#accessing-the-aem-as-a-cloud-service-sdk}

* 您可以檢查AEMAdmin Console的&#x200B;**關於Adobe Experience Manager**&#x200B;圖示，以了解您在生產環境中執行的AEM版本。
* 您可以從[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載快速入門Jar和調度程式工具的zip檔案。 請注意，SDK清單的存取權限僅限於具有AEM Managed Services或AEMas a Cloud Service環境的使用者。
* Java API Jar和Javadoc Jar可通過命令行或首選的IDE通過Maven工具下載。
* Maven專案模組應參考下列API Jar套件。 任何子套件中也應參考此相依性。

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
>SDK的版本項目應符合AEM as a Cloud Service的版本。 登入AEM，然後前往畫面右上角的問號並選取&#x200B;**[!UICONTROL 關於Adobe Experience Manager]**，即可查看您使用的版本


## 使用新SDK版本重新整理本機專案 {#refreshing-a-local-project-with-a-new-skd-version}

何時建議使用新SDK重新整理本機專案？

至少在每月維護髮行後，要重新整理它，建議&#x200B;*。*

在任何每日維護髮行後重新整理它是&#x200B;*optional*。 當客戶的生產執行個體成功升級至新的AEM版本時，系統會通知客戶。 若是每日維護髮行，新SDK預計不會有重大變更（若有）。 不過，建議您偶爾使用最新SDK重新整理本機AEM開發人員環境，然後重建並測試自訂應用程式。 每月維護版本通常包含更具影響力的變更，因此開發人員應立即重新整理、重建和測試。

以下是重新整理本機環境的建議程式：

1. 請確定任何有用的內容已提交至原始碼控制項中的項目，或可變內容包中的可用內容，以供以後導入
1. 本機開發測試內容需要個別儲存，才不會部署為Cloud Manager管道建置的一部分。 因為它只需要用於地方發展
1. 停止當前正在運行的快速入門
1. 將`crx-quickstart`資料夾移至其他資料夾以保存安全
1. 請注意Cloud Manager中說明的新AEM版本（將用於識別要進一步下載的新QuickStart Jar版本）
1. 從Software Distribution Portal下載與生產AEM版本相符的QuickStart JAR
1. 建立全新資料夾並將新的QuickStart Jar放入
1. 以所需的運行模式啟動新的QuickStart（更名檔案或通過`-r`傳入運行模式）。
   * 確保資料夾中沒有舊快速啟動的殘餘。
1. 建立您的AEM應用程式
1. 透過PackageManager將AEM應用程式部署至本機AEM
1. 通過PackageManager安裝本地環境測試所需的任何可變內容包
1. 視需要繼續開發和部署變更

如果每個新AEM快速入門版本都應安裝一些內容，請將其納入內容包和項目的原始碼控制項中。 然後，每次都安裝。

建議您經常更新SDK（例如每兩週），並每天處理完整的本機狀態，以免意外依賴應用程式中的狀態資料。

如果您依賴CryptoSupport([，通過配置AEM中的Cloudservices或SMTP Mail服務的憑據，或通過應用程式](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)中的CryptoSupport API)，則加密的屬性將通過在AEM環境的第一個啟動時自動生成的密鑰進行加密。 雖然cloudsetup會自動重複使用特定於環境的CryptoKey，但有必要將加密金鑰插入本地開發環境。

預設情況下，AEM會設定為將關鍵資料儲存在資料夾的資料夾內，但為了方便在開發中重複使用，AEM程式可在首次啟動時使用「`-Dcom.adobe.granite.crypto.file.disable=true`」初始化。 這將在「`/etc/key`」生成加密資料。

若要重複使用包含加密值的內容套件，請依照下列步驟操作：

* 最初啟動本地quickstart.jar時，請務必添加以下參數：&quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;。 建議一律新增，但選用。
* 您第一次啟動執行個體時，會建立包含根「`/etc/key`」篩選器的套件。 這將保留機密，以便在您希望重新使用的所有環境中重複使用
* 導出包含機密的任何可變內容，或通過`/crx/de`查找加密值，將其添加到將在安裝期間重複使用的包中
* 每當您回轉新執行個體（以新版本取代，或多個開發環境應共用用於測試的憑證）時，請安裝步驟2和3中產生的套件，以便能夠重複使用內容，而無需手動重新設定。 這是因為現在密碼正在同步。
