---
title: AEM as a Cloud Service SDK
description: AEMas a Cloud Service軟體開發套件概覽
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: 33ba3e88a4116674c70c44a29273a04544b6b39b
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 2%

---

# AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

AEMas a Cloud ServiceSDK由下列成品組成：

* **快速入門Jar**  — 用於本機開發的AEM執行階段
* **Java™ API Jar**  — 此Java™ Jar/Maven相依性會公開可用於針對AEMas a Cloud Service開發的所有已允許Java™ API。 先前稱為Uberjar
* **Javadoc Jar** - Java™ API Jar的Javadocs
* **Dispatcher工具**  — 針對本機Dispatcher開發的一組工具。 為UNIX®和Windows分隔成品

此外，先前部署了AEM 6.5或更早版本的部分客戶會使用下列成品。 如果本機編譯無法搭配Quickstart jar使用，而且您懷疑它是從已部署AEM的as a Cloud Service移除介面所造成，請聯絡客戶支援。 他們可決定您是否需要存取權。 它需要在後端進行變更。

* **6.5過時的Java™ API Jar**  — 自AEM 6.5之後已移除的一組額外介面
* **6.5已過時的Javadoc Jar**  — 其他已連線程式集的Javadoc

## 針對SDK進行建置 {#building-for-the-sdk}

AEMas a Cloud ServiceSDK可用來建置和部署自訂程式碼。 如需詳細資訊，請參閱 [AEM專案原型檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en). 基本上，會執行下列步驟：

* **編譯程式碼**. 如預期般編譯原始程式碼，產生結果內容套件
* **建置成品**. 在此過程中會建立成品
* **分析套件組合**. 套件組合會使用Maven分析器外掛程式進行分析，外掛程式會尋找Maven專案中的問題，例如遺漏相依性
* **部署成品**. 成品會部署至本機伺服器。

Cloud Manager在部署至雲端環境時也會執行相同的步驟。 在本機執行組建可進行本機開發和測試。 開發人員在認可原始檔控制並觸發Cloud Manager部署（可能需要更長的時間）之前，就能有效率地發現程式碼或結構問題。

>[!NOTE]
>
>AEMas a Cloud ServiceSDK應使用所支援的Java散發和版本建置 [Cloud Manager的組建環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). AEMas a Cloud Service客戶可從「 」下載OracleJDK [軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 並依據Adobe在Adobe Experience Manager專案中使用的Oracle Java技術授權和支援條款，將Java 11支援延長至2026年9月。

## 存取AEMas a Cloud ServiceSDK {#accessing-the-aem-as-a-cloud-service-sdk}

* 您可以檢查AEMAdmin Console **關於Adobe Experience Manager** 圖示來瞭解您正在生產環境中執行的AEM版本。
* 快速入門jar和Dispatcher工具可以從 [軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). SDK清單的存取權僅限於AEM Managed Services或AEMas a Cloud Service上擁有環境的人員。
* Java™ API Jar和Javadoc Jar可以透過maven工具下載，可以是命令列或是使用您偏好的IDE。
* Maven專案Pom應該參考以下API Jar套件。 也應參考任何子套件Pom的相依性。

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
>SDK的版本專案應符合AEMas a Cloud Service的版本。 您可以登入AEM檢視您使用的版本。 在畫面的右上角，前往問號並選取 **[!UICONTROL 關於Adobe Experience Manager]**.


## 使用新SDK版本重新整理本機專案 {#refreshing-a-local-project-with-a-new-skd-version}

何時建議使用新的SDK重新整理本機專案？

Adobe *建議* 在每月維護發行後重新整理。

它是 *可選* 以在每日維護發行後重新整理。 當客戶的生產執行個體成功升級至新的AEM版本時，會通知客戶。 對於每日維護發行，新的SDK可能不會有重大變更，如果有的話。 不過，建議您偶爾使用最新的SDK重新整理本機AEM開發人員環境，然後重建並測試自訂應用程式。 每月維護發行通常包含更具影響力的變更，因此開發人員應立即重新整理、重建和測試。

以下是重新整理本機環境的建議程式：

1. 請確定已將任何有用的內容提交到原始檔控制中的專案，或是可在可變內容套件中取得，以便稍後匯入。
1. 本機開發測試內容必須單獨儲存，這樣它就不會部署為Cloud Manager管道建置的一部分。 原因是它僅用於本機開發。
1. 停止目前執行中的快速入門。
1. 移動 `crx-quickstart` 資料夾放入不同的資料夾以便安全儲存。
1. 請注意新的AEM版本，在Cloud Manager中會有相關說明（用於識別新的QuickStart Jar版本，以便進一步下載）。
1. 從軟體發佈入口網站下載版本符合生產AEM版本的QuickStart JAR。
1. 建立全新的資料夾，並將新的QuickStart Jar放在裡面。
1. 以所需的執行模式啟動新的QuickStart (重新命名檔案或透過以下方式在執行模式中傳遞： `-r`)。
   * 確定資料夾中沒有遺留的舊快速入門。
1. 建置您的AEM應用程式。
1. 透過封裝管理程式將您的AEM應用程式部署到本機AEM。
1. 透過「封裝管理員」安裝本機環境測試所需的任何可變內容封裝。
1. 視需要繼續開發及部署變更。

如果有應隨每個新AEM快速入門版本一起安裝的內容，請將其納入內容套件和專案的原始檔控制中。 然後，每次都進行安裝。

建議時常更新SDK （例如每兩週），並每天處置完整的本機狀態，以免意外依賴應用程式中的狀態資料。

如果您依賴CryptoSupport ([透過在AEM中設定Cloud Services或SMTP郵件服務的認證，或在您的應用程式中使用CryptoSupport API](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html))，則加密的屬性會以金鑰加密。 此金鑰會在AEM環境首次啟動時自動產生。 雖然雲端設定會負責自動重複使用環境特定的CryptoKey，但必須將密碼金鑰插入本機開發環境中。

預設情況下，AEM設定為將關鍵資料儲存在資料夾的資料夾中，但為了方便在開發中重複使用，AEM程式可以在第一次啟動時以「`-Dcom.adobe.granite.crypto.file.disable=true`「。 此程式會在「 」產生加密資料`/etc/key`「。

若要能夠重複使用包含加密值的內容套件，請遵循下列步驟：

* 當您最初啟動本機quickstart.jar時，請務必新增以下引數： 」`-Dcom.adobe.granite.crypto.file.disable=true`「。 建議一律新增此專案，但可省略。
* 第一次啟動執行個體時，請建立包含根「 」篩選器的套件`/etc/key`「。 此套件包含要在您希望重複使用它們的所有環境中重複使用的秘密。
* 匯出任何包含密碼的可變內容，或透過以下方式查詢加密值： `/crx/de` 因此您可以將它新增至套件中，以便在安裝時重複使用。
* 每當您啟動新的執行個體時（要以新版本取代，或多個開發環境應共用認證進行測試），請安裝步驟2和3中產生的套件。 如此可讓您重複使用內容，而不需要手動重新設定。 原因是加密金鑰現在正在同步。
