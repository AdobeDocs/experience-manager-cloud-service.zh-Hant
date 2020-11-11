---
title: AEM Developer Tools for Eclipse
description: AEM Developer Tools for Eclipse
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 1%

---


# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## 概覽 {#overview}

AEM Developer Tools for Eclipse是Eclipse外掛程式，以Apache License 2下發行的 [Eclipse plugin for Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) 為基礎。

它提供數種功能，讓AEM開發更輕鬆：

* 透過Eclipse Server Connector與AEM例項緊密整合
* 內容和OSGi捆綁包的同步
* 具備程式碼熱交換功能的除錯支援
* 透過特定專案建立精靈簡單引導AEM專案
* 輕鬆編輯JCR屬性

## 需求 {#requirements}

在使用AEM開發人員工具之前，您必須：

* 下載並安裝適 [用於企業Java開發人員的Eclipse IDE](https://www.eclipse.org/downloads/packages/)。
* 按照 `eclipse.ini` Eclipse常見問答集中的說明，編輯您的設定檔案，以設定您的Eclipse安裝，確 [保您至少擁有1GB的堆](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse)積記憶體。

>[!NOTE]
>
>在macOS上，您必須在 **Eclipse.app上按一下滑鼠右鍵** ，然後選取「 **Show Package Contents** 」（顯示套件內容）才能找到您的 `eclipse.ini`**。**

## 如何安裝適用於Eclipse的AEM Developer Tools {#how-to-install-the-aem-developer-tools-for-eclipse}

在您符合上述 [要求](#requirements) ，就可依下列方式安裝外掛程式：

1. 開啟 [AEM Developer Tools網站。](https://eclipse.adobe.com/aem/dev-tools/)

1. 複製安 **裝連結**。

   請注意，您也可以下載封存檔，而不是使用安裝連結。 這允許離線安裝，但您會漏掉自動更新通知。

1. 在Eclipse中，開啟「說 **明** 」功能表。
1. 按一下 **安裝新軟體**。
1. Click **Add...**.
1. 在名 **稱中** ，輸入 `AEM Developer Tools`。
1. 在 **位置** ，複製安裝URL。
1. 按一下&#x200B;**「新增」**。
1. 同時檢 **查AEM** 和 **Sling** plugins。
1. 按一下&#x200B;**下一步**。
1. 在「安裝詳 **細資訊** 」窗口中，再次 **按一下「下一步** 」。
1. 接受授權合約，然後按一下「 **完成**」。
1. 按一 **下RestartNow** ，以重新啟動Eclipse。

## AEM透視 {#the-aem-perspective}

在Eclipse中，透視可決定視窗中可用的動作和檢視，並啟用Eclipse中以任務為導向的資源互動。 如需透視的詳細資訊，請參閱 [Eclipse檔案。](https://help.eclipse.org)

AEM Development Tools for Eclipse提供AEM Perspective，讓您完全掌控AEM專案和例項。 若要開啟AEM透視：

1. 從Eclipse菜單欄中，選擇 **Window** -> **Perspective** -> **Open Perspective** - ****>其他OtherLight。
1. 在對 **話方塊中選取** 「AEM」，然後按一下「 **開啟」**。

![Eclipse中的AEM觀點](assets/eclipse-aem-perspective.png)

## 示例多模組項目 {#sample-multi-module-project}

AEM Developer Tools for Eclipse隨附範例、多模組專案，可協助您快速上手使用Eclipse中的專案設定，並提供數種AEM功能的最佳實務指南。 [進一步瞭解Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。

請依照下列步驟建立範例專案：

1. 在「文 **件** >新建 **>** 項目」菜單中，瀏覽至 ************「AEM Sample Multi-Module Project」和「AEM Select Ample Module Project」部分。

   ![AEM範例多模組專案](assets/aem-sample-project.png)

1. 按一下&#x200B;**下一步**。

   >[!NOTE]
   >
   >這個步驟可能需要一些時間，因為m2eclipse需要掃描原型型錄。

1. 從功 `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` 能表選擇，然後按一下「下 **一步**」。

   ![選擇原型版本](assets/select-archetype.png)

1. 為範例專案提供下列欄位：

   * **名稱**
   * **群組ID**
   * **對象ID**
   * **appId** —— 您可能需要展開「進階 **** 」選項來設定此值。
   * **appTitle** —— 您可能需要展開「進階」 **選項** ，才能設定此值。
   * **套件** -您可能需要展開「進階 **」選項** ，才能設定此值。

   ![定義原型屬性](assets/archetype-properties.png)

1. 按一下&#x200B;**下一步**。

1. 然後，您就可設定Eclipse將連線至的AEM伺服器。

   若要使用除錯程式功能，您必須在除錯模式中啟動AEM —— 這可透過將下列項目新增至命令列來達成：

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![連線至AEM伺服器](assets/connect-server.png)

1. 按一 **下完成**。 將建立項目結構。

   >[!NOTE]
   >
   >在新的安裝中（更具體地說，當從未下載過任何依賴項時），您可能會獲得建立有錯誤的項目。 在這種情況下，請遵循解決無效項目定 [義中描述的過程](#resolving-invalid-project-definition)。

## 如何匯入現有專案 {#how-to-import-existing-projects}

您可以使用「 **新建專案** 」功能為您建立正確的結構：

1. 請依照指示建立 [範例多模組專案](#sample-multi-module-project) ，您將為您建立下列專案，以便正常地分離疑慮：

   * `PROJECT.ui.apps` 適用於 `/apps` 和內 `/etc` 容
   * `PROJECT.ui.content` 的 `/content` ID
   * `PROJECT.core` for Java bundles（當您想要新增Java程式碼時，這些功能就會變得有趣）
   * `PROJECT.it.launcher` 和整 `PROJECT.it.tests` 合測試

1. 將專案的內容 `PROJECT.ui.apps` 取代為套件 `apps` 的和 `etc` 資料夾：

   1. 在「專案總管」面板中，展開 `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`。
   1. 按一下右鍵資料夾， `apps` 然後選擇「 **顯示在** >系 **統瀏覽器」**。
   1. 刪除您現 `apps` 在應該看 `etc` 到的和資料夾，並將其放 `apps` 置在內容套件 `etc` 的和資料夾中。
   1. 在Eclipse中，以滑鼠右鍵按一下專案， `PROJECT.ui.apps` 然後選擇「重 **新整理**」。

1. 然後，對資料夾執 `PROJECT.ui.content` 行相同操作，並將其內容資料夾替換為您的其中一個檔案包：

   1. 在「專案總管」面板中，展開 `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`。
   1. 按一下右鍵更深層的內容資料夾，然後選擇「 **Show In** -> **System Explorer**」。
   1. 刪除您現在應該看到的內容資料夾，並將其置於內容套件的內容資料夾。
   1. 在Eclipse中，以滑鼠右鍵按一下專案， `PROJECT.ui.content` 然後選擇「重 **新整理**」。

1. 現在，您必須更新這 `filter.xml` 兩個專案的檔案，才能對應您的內容套件內容。 為此，請在個別 `META-INF/vault/filter.xml` 的文字／程式碼編輯器中開啟內容套件的檔案。

   * 以下是檔案外觀的 `filter.xml` 範例：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. 至於分割為兩個專案的套件內容，您也必須將這些篩選規則分割為兩個專案，並據以更新兩個專 `filter.xml` 案的檔案。

   1. 在Eclipse中，開啟 `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`。
   1. 將元素的內 `<workspaceFilter>` 容取代為以和開頭的套件規則 `/apps` `/etc`
      * 例如：

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/apps/foo"/>
            <filter root="/apps/foundation/components/bar"/>
            <filter root="/etc/designs/foo"/>
         </workspaceFilter>
         ```
   1. 然後開啟 `PROJECT.ui.content/src/main/content/META-INF/filter.xml`。
   1. 將規則取代為以開頭的套件 `/content`。
      * 例如：

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/content/foo"/>
            <filter root="/content/dam/foo"/>
            <filter root="/content/usergenerated/content/foo"/>
         </workspaceFilter>
         ```


1. 請確定儲存您的所有變更。 您現在可以將新內容同步到您的AEM實例。

1. 在「伺服器」面板中，確保已啟動連接，如果未啟動連接。
1. 按一下「清 **除並發佈** 」圖示。

完成後，您的套件應該會在執行個體上執行，儲存時，任何變更都會自動同步至執行個體。

如果要從項目中重新生成包，請按一下右鍵或，然 `PROJECT.ui.apps` 後選 `PROJECT.ui.content` 擇 **Run As** -> **Maven Install**。

您現在有一個目標資料夾，其中已建立您的套件(例如 `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`)。

## 疑難排解 {#troubleshooting}

### 解決無效的項目定義 {#resolving-invalid-project-definition}

要解決無效的從屬關係和項目定義，請按如下步驟進行：

1. 選取所有已建立的專案。
1. 按一下右鍵。
1. 在上下文菜單中，選擇「 **Maven** ->更 **新項目」**。
1. 檢查 **Force Updates of Snapshot/Releases**。
1. 按一下&#x200B;**「確定」**。

Eclipse會下載所需的相依性。 這可能需要一些時間。

## More information {#more-information}

Eclipse網站的Apache Sling IDE官方工具提供您有用的資訊：

* 本文 [**件將引導您瞭解AEM Development Tools支援的整體概念、伺服器整合和部署功能** ,Apache Sling IDE工具for Eclipse](https://sling.apache.org/documentation/development/ide-tooling.html)User Guide。
* 疑難 [排解區](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)。
* 「已 [知問題」清單](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)。

以下正式 [的Eclipse](https://eclipse.org/) 檔案可協助您設定環境：

* [Eclipse快速入門](https://eclipse.org/users/)
* [Eclipse Luna幫助系統](https://help.eclipse.org/luna/index.jsp)
* [Maven整合(m2eclipse)](https://www.eclipse.org/m2e/)
