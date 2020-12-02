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

AEM Developer Tools for Eclipse是Eclipse外掛程式，以Apache License 2下發行的[Eclipse plugin for Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html)為基礎。

它提供數種功能，讓AEM開發更輕鬆：

* 透過Eclipse Server Connector與AEM例項緊密整合
* 內容和OSGi捆綁包的同步
* 具備程式碼熱交換功能的除錯支援
* 透過特定專案建立精靈簡單引導AEM專案
* 輕鬆編輯JCR屬性

## 要求{#requirements}

在使用AEM開發人員工具之前，您必須：

* 下載並安裝[適用於企業Java開發人員的Eclipse IDE](https://www.eclipse.org/downloads/packages/)。
* 按照[Eclipse常見問答集](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse)中所述，編輯您的`eclipse.ini`設定檔，以設定您的Eclipse安裝以確保您至少擁有1GB的堆積記憶體。

>[!NOTE]
>
>在macOS上，您必須在&#x200B;**Eclipse.app**&#x200B;上按一下滑鼠右鍵，然後選取&#x200B;**顯示封裝內容**，才能找到您的&#x200B;`eclipse.ini`**。**

## 如何安裝AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

完成上述[要求](#requirements)後，您可以按如下方式安裝插件：

1. 開啟[AEM Developer Tools網站。](https://eclipse.adobe.com/aem/dev-tools/)

1. 複製&#x200B;**安裝連結**。

   請注意，您也可以下載封存檔，而不是使用安裝連結。 這允許離線安裝，但您會漏掉自動更新通知。

1. 在Eclipse中，開啟&#x200B;**Help**&#x200B;功能表。
1. 按一下「安裝新軟體」 ****。
1. 按一下&#x200B;**添加……**。
1. 在&#x200B;**名稱**&#x200B;中輸入`AEM Developer Tools`。
1. 在&#x200B;**Location**&#x200B;中複製安裝URL。
1. 按一下&#x200B;**「新增」**。
1. 同時檢查&#x200B;**AEM**&#x200B;和&#x200B;**Sling**&#x200B;增效模組。
1. 按一下&#x200B;**下一步**。
1. 在&#x200B;**安裝詳細資訊**&#x200B;窗口中，再次按一下&#x200B;**Next**。
1. 接受授權合約，然後按一下「完成&#x200B;**」。**
1. 按一下&#x200B;**RestartNow**&#x200B;以重新啟動Eclipse。

## AEM Perspective {#the-aem-perspective}

在Eclipse中，透視可決定視窗中可用的動作和檢視，並啟用Eclipse中以任務為導向的資源互動。 如需透視的詳細資訊，請參閱[Eclipse檔案。](https://help.eclipse.org)

AEM Development Tools for Eclipse提供AEM Perspective，讓您完全掌控AEM專案和例項。 若要開啟AEM透視：

1. 從Eclipse菜單欄中，選擇&#x200B;**Window** -> **Perspective** -> **Open Perspective** -> **Other**。
1. 在對話方塊中選取&#x200B;**AEM**，然後按一下「開啟&#x200B;**a3/>」。**

![Eclipse中的AEM觀點](assets/eclipse-aem-perspective.png)

## 多模組項目示例{#sample-multi-module-project}

AEM Developer Tools for Eclipse隨附範例、多模組專案，可協助您快速上手使用Eclipse中的專案設定，並提供數種AEM功能的最佳實務指南。 [進一步瞭解Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。

請依照下列步驟建立範例專案：

1. 在&#x200B;**File** > **New** > **Project**&#x200B;功能表中，瀏覽至&#x200B;**AEM**&#x200B;區段並選取&#x200B;**AEM Sample Multi-Module Project**。

   ![AEM範例多模組專案](assets/aem-sample-project.png)

1. 按一下&#x200B;**下一步**。

   >[!NOTE]
   >
   >這個步驟可能需要一些時間，因為m2eclipse需要掃描原型型錄。

1. 從菜單中選擇`com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` ，然後按一下&#x200B;**Next**。

   ![選擇原型版本](assets/select-archetype.png)

1. 為範例專案提供下列欄位：

   * **名稱**
   * **群組ID**
   * **對象ID**
   * **appId**  —— 您可能需要展開「進階」 **** 選項來設定此值。
   * **appTitle**  —— 您可能需要展開「進 **** 階」選項來設定此值。
   * **套件** -您可能需要展開「進階」 **** 選項來設定此值。

   ![定義原型屬性](assets/archetype-properties.png)

1. 按一下&#x200B;**下一步**。

1. 然後，您就可設定Eclipse將連線至的AEM伺服器。

   若要使用除錯程式功能，您必須在除錯模式中啟動AEM —— 這可透過將下列項目新增至命令列來達成：

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![連線至AEM伺服器](assets/connect-server.png)

1. 按一下&#x200B;**完成**。 將建立項目結構。

   >[!NOTE]
   >
   >在新的安裝中（更具體地說，當從未下載過任何依賴項時），您可能會獲得建立有錯誤的項目。 在這種情況下，請遵循[解決無效項目定義](#resolving-invalid-project-definition)中描述的過程。

## 如何導入現有項目{#how-to-import-existing-projects}

您可以使用&#x200B;**New Project**&#x200B;功能為您建立正確的結構：

1. 按照說明建立[示例多模組項目](#sample-multi-module-project)，您將為您建立以下項目，這樣可以健康地分開關注點：

   * `PROJECT.ui.apps` for  `/apps` and  `/etc` content
   * `PROJECT.ui.content` for  `/content` that is authored
   * `PROJECT.core` for Java bundles（當您想要新增Java程式碼時，這些功能就會變得有趣）
   * `PROJECT.it.launcher` 和整 `PROJECT.it.tests` 合測試

1. 將`PROJECT.ui.apps`專案的內容取代為套件的`apps`和`etc`資料夾：

   1. 在「項目瀏覽器」面板中，展開`PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`。
   1. 按一下右鍵`apps`資料夾，然後選擇「Show In **>** System Explorer **（在&lt;a2/>中顯示> &lt;a3/>系統資源管理器&lt;a4/>）」。**
   1. 刪除您現在應該看到的`apps`和`etc`資料夾，並將其放置在內容套件的`apps`和`etc`資料夾中。
   1. 在Eclipse中，按一下右鍵`PROJECT.ui.apps`項目，然後選擇&#x200B;**刷新**。

1. 然後，對`PROJECT.ui.content`執行相同動作，並將其內容資料夾取代為其中一個套件：

   1. 在「項目瀏覽器」面板中，展開`PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`。
   1. 按一下右鍵更深層的內容資料夾，然後選擇&#x200B;**顯示在** -> **系統資源管理器**。
   1. 刪除您現在應該看到的內容資料夾，並將其置於內容套件的內容資料夾。
   1. 在Eclipse中，按一下右鍵`PROJECT.ui.content`項目，然後選擇&#x200B;**刷新**。

1. 現在，您必須更新這兩個專案的`filter.xml`檔案，才能對應內容套件的內容。 為此，請在個別的文字／程式碼編輯器中開啟內容套件的`META-INF/vault/filter.xml`檔案。

   * 以下是`filter.xml`檔案外觀的範例：

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

1. 至於分割為兩個專案的套件內容，您也必須將這些篩選規則分割為兩個專案，並據以更新兩個專案的`filter.xml`檔案。

   1. 在Eclipse中，開啟`PROJECT.ui.apps/src/main/content/META-INF/filter.xml`。
   1. 將`<workspaceFilter>`元素的內容取代為以`/apps`和`/etc`開頭的套件規則
      * 例如：

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/apps/foo"/>
            <filter root="/apps/foundation/components/bar"/>
            <filter root="/etc/designs/foo"/>
         </workspaceFilter>
         ```
   1. 然後開啟`PROJECT.ui.content/src/main/content/META-INF/filter.xml`。
   1. 將規則取代為以`/content`開頭的套件。
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
1. 按一下&#x200B;**清除和發佈**&#x200B;表徵圖。

完成後，您的套件應該會在執行個體上執行，儲存時，任何變更都會自動同步至執行個體。

如果希望從項目中重新生成軟體包，請按一下右鍵`PROJECT.ui.apps`或`PROJECT.ui.content`並選擇&#x200B;**以** -> **方式運行**。

您現在有一個目標資料夾，其中已建立您的套件(例如`PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`)。

## 疑難排解 {#troubleshooting}

### 解決無效的項目定義{#resolving-invalid-project-definition}

要解決無效的從屬關係和項目定義，請按如下步驟進行：

1. 選取所有已建立的專案。
1. 按一下右鍵。
1. 在上下文菜單中，選擇&#x200B;**Maven** -> **更新項目**。
1. 檢查&#x200B;**強制更新快照／版本**。
1. 按一下&#x200B;**「確定」**。

Eclipse會下載所需的相依性。 這可能需要一些時間。

## 更多資訊{#more-information}

Eclipse網站的Apache Sling IDE官方工具提供您有用的資訊：

* 本檔案將引導您瞭解AEM Development Tools支援的整體概念、伺服器整合和部署功能，以及Eclipse **使用指南](https://sling.apache.org/documentation/development/ide-tooling.html)的[** Apache Sling IDE工具。
* [疑難排解部分](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)。
* [已知問題清單](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)。

以下正式的[Eclipse](https://eclipse.org/)文檔可幫助設定環境：

* [Eclipse快速入門](https://eclipse.org/users/)
* [Eclipse Luna幫助系統](https://help.eclipse.org/luna/index.jsp)
* [Maven整合(m2eclipse)](https://www.eclipse.org/m2e/)
