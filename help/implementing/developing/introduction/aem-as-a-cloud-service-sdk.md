---
title: AEM as a Cloud Service SDK
description: AEM as a Cloud Service Software Development Kit概述
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 8ccf03ebcb4a96b66a15dc9a1161a857888278a7
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 1%

---

# AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

AEM as a Cloud Service SDK由下列成品組成：

* **快速入門Jar** — 用於本機開發的AEM執行階段
* **Java™ API Jar** — 此Java™ Jar/Maven相依性會公開所有可用於針對AEM as a Cloud Service開發的允許Java™ API。 先前稱為Uberjar
* **Javadoc Jar** - Java™ API Jar的Javadoc
* **Dispatcher工具** — 用來在本機針對Dispatcher開發的工具集。 為UNIX®和Windows分隔成品

此外，部分先前已部署AEM 6.5或更早版本的客戶則使用下列成品。 如果本機編譯無法搭配Quickstart jar使用，並且您懷疑這是由於從AEM部署的as a Cloud Service移除介面所造成，請聯絡客戶支援。 他們可決定您是否需要存取權。 它需要在後端進行變更。

* **6.5已棄用的Java™ API Jar** — 自AEM 6.5起已移除的額外一組介面
* **6.5已棄用的Javadoc Jar** — 其他一組介面的Javadoc

>[!NOTE]
> 
> AEM as a Cloud Service和SDK在許多不同方面有所差異。 對於需要快速反複變更的情況，Adobe已推出快速開發環境。 如需詳細資訊，請檢視[快速開發環境](/help/implementing/developing/introduction/rapid-development-environments.md)。

## 針對SDK進行建置 {#building-for-the-sdk}

AEM as a Cloud Service SDK可用來建置和部署自訂程式碼。 請參閱[AEM專案原型檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html)。 基本上，會執行下列步驟：

* **編譯程式碼**。 如預期般編譯原始程式碼，產生結果內容套件
* **建置成品**。 在此過程中會建立成品
* **分析組合**。 套件組合會使用Maven分析器外掛程式進行分析，這會尋找Maven專案中的問題，例如遺漏相依性
* **部署成品**。 將成品部署至本機伺服器。

Cloud Manager在部署至雲端環境時會執行相同的步驟。 在本機執行組建可允許本機開發和測試。 開發人員在認可原始檔控制並觸發Cloud Manager部署（可能需要更長的時間）之前，就能有效率地發現程式碼或結構問題。

>[!NOTE]
>
>AEM as a Cloud Service SDK應該以[Cloud Manager的建置環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)所支援的Java散發和版本建置。 由於AEM as a Cloud Service在Adobe Experience Manager專案中使用OracleJava技術的授權和支援條款，Adobe客戶可以從[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載OracleJDK，並擁有Java 11延長支援直到2026年9月。

## 存取AEM as a Cloud Service SDK {#accessing-the-aem-as-a-cloud-service-sdk}

* 您可以檢視AEMAdmin Console的&#x200B;**關於Adobe Experience Manager**&#x200B;圖示，瞭解您正在生產環境中執行的AEM版本。
* 快速入門jar和Dispatcher工具可以從[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載為zip檔。 只有在AEM Managed Services或AEM as a Cloud Service上擁有環境的人才能存取SDK清單。
* Java™ API Jar和Javadoc Jar可以透過maven工具下載，可以是命令列或搭配您偏好的IDE。
* Maven專案Pom應該參照以下API Jar套件。 任何子封裝pom的相依性也都應參考。

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
>SDK的版本專案應符合AEM as a Cloud Service的版本。 您可以透過登入AEM來檢視您使用的版本。 在熒幕的右上角，前往問號並選取&#x200B;**[!UICONTROL 關於Adobe Experience Manager]**。


## 使用新SDK版本重新整理本機專案 {#refreshing-a-local-project-with-a-new-skd-version}

何時建議使用新的SDK重新整理本機專案？

Adobe *建議*&#x200B;在每月維護發行後重新整理。

任何每日維護版本發行後，*可選擇*&#x200B;重新整理。 當客戶的生產執行個體成功升級至新的AEM版本時，系統會通知客戶。 對於每日維護發行，新的SDK預計不會有任何重大變更，如果有的話。 不過，建議您偶爾使用最新的SDK重新整理本機AEM開發人員環境，然後重建並測試自訂應用程式。 每月維護發行通常會包含更具影響力的變更，因此開發人員應立即重新整理、重建和測試。

以下是重新整理本機環境的建議程式：

1. 請確定任何有用的內容已提交至原始檔控制中的專案，或可在可變內容套件中取得以便稍後匯入。
1. 本機開發測試內容必須分開儲存，這樣它就不會部署為Cloud Manager管道建置的一部分。 原因是它只用於本機開發。
1. 停止目前執行中的快速入門。
1. 將`crx-quickstart`資料夾移至其他資料夾，以便安全儲存。
1. 請注意新的AEM版本，Cloud Manager中註明了該版本（用於識別新的QuickStart Jar版本以供進一步下載）。
1. 從軟體發佈入口網站下載版本符合生產AEM版本的QuickStart JAR。
1. 建立全新的資料夾，並將新的QuickStart Jar放進去。
1. 以所需的執行模式（重新命名檔案或透過`-r`在執行模式中傳遞）啟動新的QuickStart。
   * 確定資料夾中沒有遺留的舊快速入門。
1. 建置您的AEM應用程式。
1. 透過封裝管理程式將您的AEM應用程式部署到本機AEM。
1. 透過「封裝管理員」安裝本機環境測試所需的任何可變內容封裝。
1. 視需要繼續開發及部署變更。

如果有應隨每個新AEM快速入門版本一起安裝的內容，請將其納入內容套件和專案的原始檔控制中。 然後，每次都進行安裝。

建議時常更新SDK （例如每兩週），並每天處置完整的本機狀態，以免意外依賴應用程式中的狀態資料。

若您依賴CryptoSupport ([藉由在AEM中設定Cloud Services或SMTP Mail服務的認證，或使用應用程式](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)中的CryptoSupport API)，加密的內容會以金鑰加密。 此金鑰會在AEM環境首次啟動時自動產生。 雖然雲端設定會負責自動重複使用環境特定的CryptoKey，但必須將密碼金鑰插入本機開發環境中。

預設會將AEM設定為將金鑰資料儲存在資料夾的資料夾中，但為了方便在開發中重複使用，AEM程式可以在第一次啟動時使用&quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;初始化。 此程式會在&quot;`/etc/key`&quot;產生加密資料。

若要能夠重複使用包含加密值的內容套件，請執行下列步驟：

* 當您初次啟動本機quickstart.jar時，請務必新增以下引數：&quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;。 建議您一律新增此專案，但可省略。
* 第一次啟動執行個體時，請建立包含根&quot;`/etc/key`&quot;篩選器的套件。 此套件內含要在所有您想要重複使用的環境中重複使用的秘密。
* 匯出任何包含密碼的可變內容，或透過`/crx/de`查詢加密值，以便將其新增到安裝時可重複使用的封裝。
* 每當您啟動新的執行個體時（若要以新版本取代，或多個開發環境應共用認證進行測試），請安裝步驟2和3中產生的套件。 如此可讓您重複使用內容，而不需要手動重新設定。 原因是現在密碼金鑰處於同步中。
