---
title: AEM AS A CLOUD SERVICE DEVELOPER CONSOLE - BETA
description: 瞭解CRXDE Lite和AEM as a Cloud Service Developer Console。
feature: Developing
role: Admin, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 1%

---

# AEM as a Cloud Service Developer Console (Beta) {#developer-console}

>[!NOTE]
>
>本文說明AEM Cloud Service Developer Console （目前為測試版）的改良體驗。 有些客戶可以按一下傳統UI頂端的按鈕來存取它。 Adobe歡迎您傳送意見回饋給「`aemcs-new-devconsole-ui-beta@adobe.com`」。 如需傳統AEM Developer Console的相關資訊，請參閱[本文章](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)。

AEM as a Cloud Service Developer Console包含一組可在雲端環境中除錯的工具。 您可透過Cloud Manager中的每個環境連結加以存取。

>[!NOTE]
>不應混淆AEM as a Cloud Service Developer Console與類似名稱的&#x200B;[*Adobe Developer Console*](https://developer.adobe.com/developer-console/)。
>


<!--
There are multiple ways of accessing it:

1. Launch from Cloud Manager  

1. Type a url that can be determined by adjusting the Author or Publish service urls as follows:
   ```  
   https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com
   ```  

1. As a shortcut, the following Cloud Manager CLI command can be used to launch the AEM as a Cloud Service Developer Console based on an environment parameter described below:    
   ```
   aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>
   ```
-->

開發人員可以存取以下所述的功能：

## OSGi組合 {#osgi-bundles}

![開發主控台中的新OSGi套件組合畫面](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* 所選環境型別中部署的OSGI套件組合概觀。 它可啟用全文檢索搜尋。
* 取得環境中套件組合的實際狀態資訊會很有用。 您可以取得資訊，例如，匯出的套件、匯入的套件、使用的服務等。
* 開發人員想要在實際環境中驗證，並檢查套件組合是否確實如預期般運作。
* **範例使用案例：**&#x200B;已在您的套件組合中指定相依性的版本範圍。 相依性發生錯誤。 您想要檢查要連線至您的套件組合中的相依性版本。 若要檢查，請移至套件組合詳細資料，並使用匯入套件/套件來檢查執行階段正在使用的套件組合版本或套件版本。 有了這些資訊，您可以調整您的maven相依性版本範圍或調整您的程式碼。

## Java套件 {#java-packages}

開發主控台UI中的![Java套件索引標籤](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* 可用來搜尋環境OSGI系統中作用中之套件的搜尋提示。 在此位置中，您可以看到哪個套件組合匯出（或提供）套件，以及哪個套件組合匯入（或使用）套件。 您也可以檢查是否有重複的封裝（相同的封裝、不同的版本），這在某些情況下可能會造成問題。
* **範例使用案例：**&#x200B;使用[動態類別載入器](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html)的自訂服務載入類別而不指定版本。 由於多個套件組合匯出不同的版本，實作會有所不同，導致行為變更。 開發人員想要檢查哪些套件位於環境中，而不分析功能模型。 他們搜尋套件並檢視所有匯出的版本。 此功能可讓使用者輸入更佳版本範圍的資訊。

## Servlet {#servlets}

開發主控台UI中的![Servlet索引標籤](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* 搜尋提示，您可以在其中指定包含選取器的路徑，以及包含GET或POST的副檔名。 然後會依優先順序提供servlet的結果，以處理Sling中的請求。
* **範例使用案例：**&#x200B;您有OSGI servlet，應該根據要求啟動，並將輸出列印到回應。 然而，回應會傳回空白，而不是預期的輸出。 您需要檢查由於更具體的選擇器、`resourceType`、擴充功能或排名，是否有其他servlet優先於您的servlet。 您可以搜尋預期的路徑，並找出另一個排名較高且作用中的servlet。 然後，您可以決定是否要新增選取器，讓您的servlet在排名中名列前茅。

## 服務 {#services}

Dev Console UI中的![Services標籤](/help/implementing/developing/introduction/assets/services-dev-console.png)

* 類似OSGI元件檢視，但以服務為基礎。 您可以快速搜尋哪些服務已提供特定屬性。

## OSGi元件 {#osgi-components}

Dev Console UI中的![OSGi元件索引標籤](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* 所選環境型別中存在的OSGI元件概觀。 它可啟用全文檢索搜尋。
* 您可以取得環境中OSGI元件的即時狀態。 您可以檢視它滿足哪些服務、提供服務的套件組合以及啟動型別（立即或延遲）。
* **範例使用案例1：**&#x200B;作為開發人員，您必須檢查使用設定啟用的元件在特定環境中是否作用中。 原因是預期的行為未發生。 您只需在搜尋中查詢元件，並檢查元件是否處於活動狀態。
* **範例使用案例2：**&#x200B;您想要檢視環境中可用的現成元件，並識別其支援的服務。 此功能可協助您進一步瞭解Adobe Experience Manager as a Cloud Service。 您可以在元件清單中將其出庫。

## 整合 {#integrations}

![開發主控台UI中的整合標籤](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* 管理員能夠產生、重新命名和刪除服務憑證和開發人員權杖。

## 存放庫 {#repository}

* 開啟[存放庫瀏覽器](/help/implementing/developing/tools/repository-browser.md)。

## 狀態傾印/查詢 {#status-dumps-queries}

![開發主控台UI中的狀態傾印/查詢索引標籤](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* 套件、套件、設定、服務、元件、Sling作業或Oak定義之目前狀態的全文或JSON傾印。
* 如果開發人員發現一些非預期的狀態，並想要與其他開發人員通訊或記錄此狀態，這個方法就特別有用。 下載傾印會提供狀態的快照，以供您稍後參考。

## 設定 {#configurations}

Dev Console UI中的![組態標籤](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* 可在環境中啟用的設定清單。 您可以透過檢視詳細資訊頁面來檢視組態所提供的屬性。
* **使用案例範例：**&#x200B;開發人員想要確定他們指定的設定確實存在於環境中。 如果缺少組態，他們可以檢查特徵模型或組態執行模式或資料夾。

對於生產計畫，Adobe Admin Console中的「Cloud Manager — 開發人員角色」可控制AEM as a Cloud Service Developer Console的存取權。 對於沙箱計畫，任何擁有授予AEM存取權的產品設定檔的使用者都可以使用Developer Console。 對於所有計畫，狀態傾印和存取存放庫瀏覽器需要「Cloud Manager — 開發人員角色」。 若要檢視來自作者與發佈服務的資料，使用者也必須同時被指派給這兩項服務上的AEM使用者或AEM管理員產品設定檔。

如需設定使用者許可權的詳細資訊，請參閱[Cloud Manager檔案](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles)。

