---
title: AEM as a Cloud Service Developer Console (Beta)
description: 瞭解CRX/DE Lite和AEM as a Cloud Service Developer Console
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 16379d9cb7cdf876502205c12a233a95b410a67a
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 0%

---


# AEM as a Cloud Service Developer Console (Beta) {#developer-console}

>[!NOTE]
>
>本文說明AEM Cloud Service Developer Console的改版體驗，目前為測試版，並可按一下Classic UI頂端的按鈕提供給部分客戶使用。 感謝您傳送意見給`aemcs-new-devconsole-ui-beta@adobe.com`。 如需傳統AEM Developer Console的相關資訊，請參閱[本文章](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)。

## AEM as a Cloud Service 開發工具 {#aem-as-a-cloud-service-development-tools}

>[!NOTE]
>不應混淆AEM as a Cloud Service Developer Console與類似名稱的&#x200B;[*Adobe Developer Console*](https://developer.adobe.com/developer-console/)。
>

客戶可以在作者階層的開發環境中存取CRXDE Lite，但不能在預備或生產環境中存取。 無法在執行階段寫入不可變的存放庫(`/libs`， `/apps`)，因此嘗試這樣做將會導致錯誤。

您可以從AEM as a Cloud Service Developer Console啟動存放庫瀏覽器，為作者、發佈和預覽層級的所有環境提供存放庫的唯讀檢視。 如需詳細資訊，請參閱[存放庫瀏覽器](/help/implementing/developing/tools/repository-browser.md)。

AEM as a Cloud Service Developer Console中針對RDE、開發、測試和生產環境提供了一組用於偵錯AEM as a Cloud Service開發人員環境的工具。 可藉由調整作者或Publish服務URL來決定URL，如下所示：

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

下列Cloud Manager CLI命令當作捷徑，可用來根據下列所述的環境引數啟動AEM as a Cloud Service Developer Console：

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

如需詳細資訊，請參閱[發行資訊](/help/release-notes/home.md)。

開發人員可以產生狀態資訊，並解析各種資源。

如下圖所示，可用的狀態資訊包括套件組合、元件、OSGI設定、Oak索引、OSGI服務和Sling工作的狀態。

### OSGi組合 {#osgi-bundles}

![開發主控台中的新OSGi套件組合畫面](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* 這會產生在選定環境型別上部署的OSGI套件組合概覽。 它可啟用全文檢索搜尋。
* 取得環境中套件組合的實際狀態資訊會很有用。 您可以取得資訊，例如，匯出的套件、匯入的套件、使用的服務等。
* 開發人員想要在實際環境中驗證，並檢查套件組合是否確實如預期般運作。
* **範例使用案例：**&#x200B;已在您的套件組合中指定相依性的版本範圍。 相依性發生錯誤。 您想要檢查要連線至您的套件組合中的相依性版本。 若要檢查此問題，請前往套件組合詳細資料，並使用匯入套件/套件來檢查執行階段使用哪個套件組合版本或套件版本來找出問題。 有了這些資訊，您可以調整您的maven相依性版本範圍或調整您的程式碼。

### Java套件 {#java-packages}

開發主控台UI中的![Java套件索引標籤](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* 這會提供搜尋提示，讓您用來搜尋在環境的OSGI系統中作用中的套件。 在此位置中，您可以看到哪個套件組合匯出（或提供）套件，以及哪個套件組合匯入（或使用）套件。 您也可以檢查是否有重複的封裝（相同的封裝、不同的版本），這在某些情況下可能會造成問題。
* **範例使用案例：**&#x200B;使用[動態類別載入器](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html)的自訂服務正在載入類別，但未指定版本，而該版本是由不同版本的多個套件組合匯出，導致實作不同且行為變更。 開發人員想要檢視哪些套件位於環境中，而不分析功能模型，因此他們會搜尋此套件並檢視所有正在匯出的版本。 這可提供他們輸入較佳版本範圍的資訊。

### Servlet {#servlets}

開發主控台UI中的![Servlet索引標籤](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* 這會提供搜尋提示，您可以在其中指定帶有選取器的路徑以及帶有GET或POST的副檔名。 然後它會依照優先順序提供servlet的結果，以處理Sling中的請求。
* **範例使用案例：**&#x200B;您有OSGI servlet，應該在要求上啟動並列印一些內容到回應，但您收到的是空白回應。 您需要檢查由於更具體的選擇器、`resourceType`、擴充功能或排名，是否有其他servlet優先於您的servlet。 您可以搜尋預期的路徑，並找出另一個排名較高且作用中的servlet。 然後，您可以決定是否要新增選取器，讓您的servlet在排名中名列前茅。

### 服務 {#services}

Dev Console UI中的![Services標籤](/help/implementing/developing/introduction/assets/services-dev-console.png)

* 類似OSGI元件檢視，但以服務為基礎。 您可以快速搜尋哪些服務已提供特定屬性。

### OSGi元件 {#osgi-components}

Dev Console UI中的![OSGi元件索引標籤](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* 這會產生所選環境型別中存在的OSGI元件概觀。 它可啟用全文檢索搜尋。
* 您可以取得環境中OSGI元件的即時狀態。 您可以檢視它滿足哪些服務、提供服務的套件組合以及啟動型別（立即或延遲）。
* **範例使用案例1：**&#x200B;作為開發人員，您想要驗證使用設定啟動的元件是否於特定環境中作用中，因為您沒有獲得您預期的行為。 您只需在搜尋中查詢元件，並檢視元件是否處於作用中狀態。
* **使用案例2範例：**&#x200B;您想要瞭解環境中有哪些現成的元件，以及這些元件滿足哪些服務需求，以便深入瞭解Adobe Experience Manager as a Cloud Service。 您可以在元件清單中將其出庫。

### 整合 {#integrations}

![開發主控台UI中的整合標籤](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* 可讓管理員產生、重新命名和刪除服務憑證和開發人員權杖。

### 存放庫 {#repository}

* 開啟[存放庫瀏覽器](/help/implementing/developing/tools/repository-browser.md)。

### 狀態傾印/查詢 {#status-dumps-queries}

![開發主控台UI中的狀態傾印/查詢索引標籤](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* 提供套件、套件、設定、服務、元件、Sling作業或Oak定義之目前狀態的全文或JSON傾印。
* 如果開發人員發現一些未預期的狀態，並且想要與其他開發人員溝通或記錄此狀態，此功能會特別有用。 下載傾印會提供狀態的快照，以供您稍後參考。

### 設定 {#configurations}

Dev Console UI中的![組態標籤](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* 這可讓您搜尋在環境中作用中的設定清單。 您可以透過檢視詳細資訊頁面來檢視組態所提供的屬性。
* **範例使用案例：**&#x200B;開發人員想要確定他們指定的設定實際存在於環境中。 如果缺少組態，他們可以檢查特徵模型或組態執行模式或資料夾。

對於生產計畫，AEM as a Cloud Service Developer Console的存取權由Adobe Admin Console中的「Cloud Manager — 開發人員角色」定義，而對於沙箱計畫，AEM as a Cloud Service Developer Console則可供任何擁有產品設定檔並授與對AEM as a Cloud Service存取權的使用者使用。 對於所有程式，狀態傾印需要「Cloud Manager — 開發人員角色」，存放庫瀏覽器和使用者也必須在AEM使用者或AEM管理員產品設定檔中，針對作者和發佈服務進行定義，以便從這兩項服務檢視資料。 如需設定使用者許可權的詳細資訊，請參閱[Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)。