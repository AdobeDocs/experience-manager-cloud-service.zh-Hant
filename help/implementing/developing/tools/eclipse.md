---
title: Eclipse 適用的 AEM 開發人員工具
description: 瞭解如何使用適用於Eclipse的AEM開發人員工具，這是以適用於Apache Sling的Eclipse外掛程式為基礎的Eclipse外掛程式。
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
feature: Developing
role: Admin, Architect, Developer
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 2%

---

# Eclipse 適用的 AEM 開發人員工具{#aem-developer-tools-for-eclipse}

![適用於Eclipse標誌的Experience Manager Developer Tools](assets/eclipse-logo.png)

## 概觀 {#overview}

_適用於Eclipse的Experience Manager Developer Tools_&#x200B;是以Apache授權2所發行適用於Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html)的[Eclipse外掛程式為基礎的Eclipse外掛程式。

它提供數項功能，讓AEM開發更容易：

* 透過Eclipse伺服器聯結器與AEM執行個體緊密整合
* 內容和OSGi套件組合的同步
* 使用程式碼熱交換功能提供除錯支援
* AEM專案的簡單Bootstrap，透過特定專案建立精靈
* 輕鬆編輯JCR屬性

## 要求 {#requirements}

使用AEM開發人員工具之前，您需要：

* 下載並安裝適用於Enterprise Java™開發人員的[Eclipse IDE](https://www.eclipse.org/downloads/packages/)。
* 依照[Eclipse常見問答集](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)中的說明，編輯您的`eclipse.ini`設定檔，設定Eclipse安裝，確保您至少有1 GB的棧積記憶體。

>[!NOTE]
>
>在macOS上，您必須用滑鼠右鍵按一下&#x200B;**Eclipse.app**，然後選取&#x200B;**顯示封裝內容**&#x200B;以尋找您的&#x200B;`eclipse.ini`**。**

## 如何安裝適用於Eclipse的AEM開發人員工具 {#how-to-install-the-aem-developer-tools-for-eclipse}

當您符合上述[需求](#requirements)時，您可以依照下列方式安裝外掛程式：

1. 開啟[AEM Developer Tools網站](https://eclipse.adobe.com/com.adobe.granite.ide.p2update-1.3.0.zip)。<!-- RB: OLD URL was (https://eclipse.adobe.com/aem/dev-tools/) This URL is generating a 404 error in the experience-manager-cloud-service.en LinkCheckExl report . The website appears to be dead; no redirects at all. Clicking "Installation Link" does not do anything. Only the link "Download archive" works. The "Online Documentation" link just takes you to the AEM Docs home page. Not sure if this topic is still needed?? -->

1. 複製&#x200B;**安裝連結**。

   您也可以下載封存，而不使用安裝連結。 此方法允許離線安裝，但您不會以這種方式收到遺漏自動更新通知。

1. 在Eclipse中，開啟&#x200B;**說明**&#x200B;功能表。
1. 按一下&#x200B;**安裝新軟體**。
1. 按一下&#x200B;**新增……**。
1. 在&#x200B;**名稱**&#x200B;欄位中，輸入`AEM Developer Tools`。
1. 在&#x200B;**位置**&#x200B;欄位中，複製安裝URL。
1. 按一下&#x200B;**新增**。
1. 檢查&#x200B;**AEM**&#x200B;和&#x200B;**Sling**&#x200B;外掛程式。
1. 按一下「**下一步**」。
1. 在&#x200B;**安裝詳細資料**&#x200B;視窗中，再按一下&#x200B;**下一步**。
1. 接受授權合約，然後按一下&#x200B;**完成**。
1. 按一下&#x200B;**立即重新啟動**&#x200B;以重新啟動Eclipse。

## AEM觀點 {#the-aem-perspective}

在Eclipse中，「透視」可決定視窗中可用的動作和檢視，並可與Eclipse中的資源進行以工作為導向的互動。 如需透視的詳細資訊，請參閱[Eclipse檔案](https://help.eclipse.org/latest/index.jsp)。

_適用於Eclipse的Experience Manager開發工具_&#x200B;提供AEM觀點，讓您完全控制您的AEM專案和執行個體。 若要開啟AEM透視：

1. 從Eclipse功能表列選取&#x200B;**視窗** > **透視** > **開啟透視** > **其他**。
1. 在對話方塊中選取&#x200B;**AEM**，然後按一下&#x200B;**開啟**。

![Eclipse中的AEM觀點](assets/eclipse-aem-perspective.png)

## 多模組專案範例 {#sample-multi-module-project}

適用於Eclipse的&#x200B;_Experience Manager Developer Tools_&#x200B;隨附範例、多模組專案，可協助您快速上手Eclipse中的專案設定。 它也是幾項AEM功能的最佳實務指南。 [進一步瞭解專案原型](https://github.com/adobe/aem-project-archetype)。

請依照下列步驟建立範例專案：

1. 在&#x200B;**檔案** > **新增** > **專案**&#x200B;功能表中，瀏覽至&#x200B;**AEM**&#x200B;區段並選取&#x200B;**AEM範例多模組專案**。

   ![AEM範例多模組專案](assets/aem-sample-project.png)

1. 按一下「**下一步**」。

   >[!NOTE]
   >
   >此步驟可能需要一些時間，因為m2eclipse必須掃描原型目錄。

1. 從功能表選擇`com.adobe.granite.archetypes : sample-project-archetype : <highest-number>`，然後按一下&#x200B;**下一步**。

   ![選取原型版本](assets/select-archetype.png)

1. 為範例專案提供下列欄位：

   * **名稱**
   * **群組識別碼**
   * **成品ID**
   * **appId** — 您可能需要展開&#x200B;**進階**&#x200B;選項才能設定此值。
   * **appTitle** — 您可能需要展開&#x200B;**進階**&#x200B;選項以設定此值。
   * **封裝** — 您可能需要展開&#x200B;**進階**&#x200B;選項以設定此值。

   ![定義原型屬性](assets/archetype-properties.png)

1. 按一下「**下一步**」。

1. 接著，您可以設定Eclipse連線的AEM伺服器。

   若要使用偵錯工具功能，您必須以偵錯模式啟動AEM — 這可以透過將下列專案新增到命令列來實現：

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![連線到AEM伺服器](assets/connect-server.png)

1. 按一下&#x200B;**完成**。 專案結構隨即建立。

   >[!NOTE]
   >
   >在全新安裝中（更具體地說，當從未下載maven相依性時），您可能會收到建立專案時出現的錯誤。 在此情況下，請依照[解決無效的專案定義](#resolving-invalid-project-definition)中說明的程式進行。

## 如何匯入現有的專案 {#how-to-import-existing-projects}

您可以使用&#x200B;**新專案**&#x200B;功能來建立正確的結構：

1. 請依照指示建立[範例多模組專案](#sample-multi-module-project)，您已為您建立下列專案，這些專案允許健康地分離問題：

   * `/apps`和`/etc`內容的`PROJECT.ui.apps`
   * 已編寫之`/content`的`PROJECT.ui.content`
   * 適用於Java™套件組合的`PROJECT.core` (當您想要新增Java™程式碼時，這些套件組合會變得有趣起來)
   * 整合測試的`PROJECT.it.launcher`和`PROJECT.it.tests`

1. 將`PROJECT.ui.apps`專案的內容取代為您的封裝的`apps`和`etc`資料夾：

   1. 在「專案總管」面板中，展開`PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`。
   1. 在`apps`資料夾上按一下滑鼠右鍵，然後選擇&#x200B;**顯示於** > **系統總管**。
   1. 刪除您現在應該看到的`apps`和`etc`資料夾，並將內容封裝的`apps`和`etc`資料夾放置在這裡。
   1. 在Eclipse中，以滑鼠右鍵按一下`PROJECT.ui.apps`專案，然後選擇&#x200B;**重新整理**。

1. 然後對`PROJECT.ui.content`執行相同操作，並將其內容資料夾取代為您其中一個封裝：

   1. 在「專案總管」面板中，展開`PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`。
   1. 用滑鼠右鍵按一下較深的內容資料夾，然後選擇&#x200B;**顯示於** > **系統總管**。
   1. 刪除您現在應該看到的內容資料夾，並在此處放置內容封裝的內容資料夾。
   1. 在Eclipse中，以滑鼠右鍵按一下`PROJECT.ui.content`專案，然後選擇&#x200B;**重新整理**。

1. 現在您必須更新這兩個專案的`filter.xml`個檔案，以對應至您內容封裝的內容。 為此，請在個別的文字/程式碼編輯器中開啟內容封裝的`META-INF/vault/filter.xml`檔案。

   * 以下範例說明您的`filter.xml`檔案外觀：

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

1. 至於您分割為兩個專案的套件內容，您也必須將這些篩選規則分割為兩個並相應地更新兩個專案的`filter.xml`檔案。

   1. 在Eclipse中，開啟`PROJECT.ui.apps/src/main/content/META-INF/filter.xml`。
   1. 將`<workspaceFilter>`元素的內容取代為您以`/apps`和`/etc`開頭的封裝規則
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
   1. 將規則取代為您以`/content`開頭的套件規則。
      * 例如：

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/content/foo"/>
           <filter root="/content/dam/foo"/>
           <filter root="/content/usergenerated/content/foo"/>
        </workspaceFilter>
        ```

1. 請務必儲存所有變更。 您現在可以將新內容同步至您的AEM執行個體。

1. 在「伺服器」面板中，確定您的連線已啟動，若未啟動，則確定已啟動連線。
1. 按一下&#x200B;**清除並發佈**&#x200B;圖示。

完成後，您應該在執行個體上執行套件，並在儲存時，任何變更都會自動同步到執行個體。

如果您想要從專案重新建置套件，請在`PROJECT.ui.apps`或`PROJECT.ui.content`上按一下滑鼠右鍵，然後選擇&#x200B;**執行身分** > **Maven安裝**。

您現在已建立目標資料夾，內含套件（例如`PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`）。

## 疑難排解 {#troubleshooting}

### 解析無效的專案定義 {#resolving-invalid-project-definition}

若要解決無效的相依性和專案定義，請依照下列步驟進行：

1. 選取所有已建立的專案。
1. 按一下滑鼠右鍵。
1. 在內容功能表中，選取&#x200B;**Maven** > **更新專案**。
1. 檢查&#x200B;**強制更新快照/版本**。
1. 按一下&#x200B;**「確定」**。

Eclipse會下載必要的相依性。 這可能需要一段時間。

## 詳細資訊 {#more-information}

Eclipse網站的官方Apache Sling IDE工具提供您實用資訊：

* 適用於Eclipse **的[** Apache Sling IDE工具使用手冊](https://sling.apache.org/documentation/development/ide-tooling.html)，此檔案會引導您瞭解AEM開發工具支援的整體概念、伺服器整合和部署功能。
* [疑難排解區段](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)。
* [已知問題清單](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)。

下列正式[Eclipse](https://www.eclipse.org/)檔案可協助您設定環境：

* [開始使用Eclipse](https://eclipseide.org/getting-started/)
* [Eclipse Luna說明系統](https://help.eclipse.org/latest/index.jsp)
* [Maven整合(m2eclipse)](https://www.eclipse.org/m2e/)
