---
title: AEM AS A CLOUD SERVICE DEVELOPER CONSOLE - BETA
description: 瞭解AEM as a Cloud Service Developer Console及其一組針對雲端環境除錯的唯讀工具。
feature: Developing
role: Admin, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: 51c14ba3c15e0136911003752253d21ed673a0eb
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---


# AEM as a Cloud Service Developer Console (Beta) {#developer-console}

AEM as a Cloud Service Developer Console包含一組唯讀工具，可用於偵錯雲端環境。 可透過Cloud Manager中的每個環境連結存取該區域，並提供功能來檢視套件組合、OSGi設定、服務和servlet等。

>[!NOTE]
>
>本文說明AEM Cloud Service Developer Console （目前為測試版）的改良體驗。
>
>* 有限的使用者可以透過目前Developer Console頂端的按鈕存取新主控台。
>* Adobe歡迎您傳送意見回饋給「`aemcs-new-devconsole-ui-beta@adobe.com`」。
>* 如需有關目前AEM Developer Console的檔案，請參閱[本文章。](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)
>* 不應混淆AEM as a Cloud Service Developer Console與類似名稱的&#x200B;[*Adobe Developer Console*.](https://developer.adobe.com/developer-console/)

>[!TIP]
>
>Developer Console是唯讀的。 如果您使用SDK進行本機開發，並且需要修改OSGi設定或存放庫內容，您可以使用：
>
>* [CRXDE Lite](/help/implementing/developing/tools/crxde.md)

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

## 先決條件 {#prerequisites}

Developer Console僅供在某些程式中擁有特定角色的使用者存取。

* 對於生產計畫，Adobe Admin Console中的「Cloud Manager — 開發人員角色」會控制Developer Console的存取權。
* 對於沙箱計畫，任何擁有授予AEM存取權的產品設定檔的使用者都可以使用Developer Console。
* 對於所有計畫，狀態傾印和存取存放庫瀏覽器需要「Cloud Manager — 開發人員角色」。

若要檢視來自作者與發佈服務的資料，使用者也必須同時被指派給這兩個服務上的「AEM使用者」或「AEM管理員產品設定檔」。

如需設定使用者許可權的詳細資訊，請參閱[Cloud Manager檔案。](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles)

## OSGi套件組合標籤 {#osgi-bundles}

**OSGi組合**&#x200B;索引標籤提供在選定環境中部署的OSGi組合概覽，並提供全文檢索搜尋。

![Developer Console中的新OSGi套件組合畫面](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* 索引標籤提供有關環境中套件組合實際狀態的資訊，例如匯出的套件、匯入的套件、使用的服務等。
* 理想的做法是檢查套件組合的狀態，檢視套件組合是否如預期般運作。

**範例使用案例：**&#x200B;假設您為套件組合中的相依性指定版本範圍。 但相依性發生問題，您需要檢查該套件實際使用了哪個相依性版本。 若要檢查，請開啟Developer Console，然後按一下&#x200B;**OSGi組合**&#x200B;標籤上的組合名稱以存取組合詳細資料，並使用&#x200B;**匯入組合**&#x200B;摺疊式功能表來檢查執行階段正在使用的組合版本或套件版本。 有了這些資訊，您可以調整您的maven相依性版本範圍或調整您的程式碼。

## Java封裝標籤 {#java-packages}

**Java套件**&#x200B;索引標籤提供搜尋欄位，可搜尋在環境的OSGi系統中作用中的套件。

Developer Console UI中的![Java套件索引標籤](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* 您可以看到哪個套件組合匯出（或提供）套件，以及哪些套件組合匯入（或使用）套件。
* 您也可以檢查是否有重複的封裝（相同的封裝、不同的版本），這在某些情況下可能會造成問題。

**範例使用案例：**&#x200B;假設自訂服務使用[動態類別載入器](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html)載入類別而不指定版本。 由於多個套件組合匯出不同的版本，實作會有所不同，導致行為變更。 您想要檢查哪些封裝位於環境中，而不分析特徵模型。 使用此索引標籤，您可以搜尋套件並檢視所有匯出的版本，然後使用更好的版本範圍。

## 「組態」標籤 {#configurations}

**組態**&#x200B;索引標籤提供環境中作用中組態的可搜尋清單。 您可以檢視每個設定所提供的屬性，方法是按一下該設定並檢視詳細資訊頁面。

Developer Console UI中的![設定索引標籤](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* **使用案例範例：**&#x200B;假設您想要確定指定的設定確實存在於環境中。 如果您在主控台中搜尋&#x200B;**組態**&#x200B;標籤，但組態遺失，您可以檢查功能模型、組態執行模式或資料夾。

## Servlet索引標籤 {#servlets}

**Servlet**&#x200B;索引標籤提供搜尋欄位，您可以在其中指定包含選取器的路徑以及包含GET或POST的副檔名。 然後會依優先順序提供servlet清單，以處理Sling中的請求。

Developer Console UI中的![Servlet索引標籤](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

**使用案例範例：**&#x200B;假設您有OSGi servlet，應該根據要求啟動並列印輸出至回應。 不過，您會收到空白回應，而不是預期的輸出。 您需要檢查由於更具體的選擇器、`resourceType`、擴充功能或排名，是否有其他servlet優先於您的servlet。 您會搜尋預期的路徑，並找到另一個排名較高且作用中的servlet。 然後，您可以決定是否可新增選取器來增加servlet的排名。

## 服務標籤 {#services}

**服務**&#x200B;索引標籤提供所選環境中服務的概觀，並提供全文檢索搜尋。

Developer Console UI中的![服務標籤](/help/implementing/developing/introduction/assets/services-dev-console.png)

按一下服務即可檢視其詳細資訊。

## OSGi元件標籤 {#osgi-components}

**OSGi元件**&#x200B;索引標籤提供存在於所選環境型別中的OSGi元件概觀，並提供全文檢索搜尋。 您可以檢視環境中OSGi元件的即時狀態，以及它滿足哪些服務、提供服務的套件組合以及啟動型別（立即或延遲）。

Developer Console UI中的![OSGi元件索引標籤](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* **範例使用案例1：**&#x200B;假設您需要檢查使用設定啟用的元件在特定環境中是否有效，因為您遇到非預期的行為。 您只需在搜尋中查詢元件，並檢查元件是否處於活動狀態。
* **使用案例範例2：**&#x200B;假設您想檢視環境中有哪些現成的元件，並識別這些元件支援的服務，以進一步瞭解Adobe Experience Manager as a Cloud Service。 您可以檢查元件清單中的元件。

## 整合功能索引標籤 {#integrations}

**整合**&#x200B;索引標籤可讓管理員產生、重新命名和刪除服務認證和開發人員權杖。

![Developer Console UI中的「整合」索引標籤](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

## 存放庫索引標籤 {#repository}

**存放庫**&#x200B;索引標籤會開啟[存放庫瀏覽器。](/help/implementing/developing/tools/repository-browser.md)

## 狀態傾印/查詢標籤 {#status-dumps-queries}

**狀態傾印/查詢**&#x200B;索引標籤可讓您下載套裝、套件、設定、服務、元件、sling工作或Oak定義之目前狀態的全文或JSON傾印。

Developer Console UI中的![狀態傾印/查詢索引標籤](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

您也可以開啟[查詢效能工具。](/help/operations/query-and-indexing-best-practices.md#query-performance-tool)

* **範例使用案例：**&#x200B;如果您遇到未預期的狀態並想要與其他開發人員通訊或記錄它，此標籤會特別有用。 下載傾印會提供狀態的快照，以供您稍後參考。
