---
title: 用AEM於Eclipse的開發人員工具
description: 用AEM於Eclipse的開發人員工具
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 1%

---

# 用AEM於Eclipse的開發人員工具{#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## 概覽 {#overview}

Developer AEM Tools for Eclipse是基於 [Apache Sling的Eclipse插件](https://sling.apache.org/documentation/development/ide-tooling.html) 已在Apache許可證2下發佈。

它提供了幾種使開發更AEM容易的功能：

* 通過Eclipse Server Connector與AEM實例無縫整合
* 內容和OSGi捆綁包的同步
* 具有代碼熱交換功能的調試支援
* 通過特定項AEM目建立嚮導簡單引導項目
* 易於編輯JCR屬性

## 要求 {#requirements}

使用開發AEM人員工具之前，您需要：

* 下載並安裝 [用於Enterprise Java開發人員的Eclipse IDE](https://www.eclipse.org/downloads/packages/)。
* 配置eclipse安裝，通過編輯您的 `eclipse.ini` 配置檔案（如所述） [Eclipse常見問題](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse)。

>[!NOTE]
>
>在macOS上，您需要右鍵 **Eclipse.app** ，然後選擇 **顯示包內容** 以便找到 `eclipse.ini`**。**

## 如何安裝EclipseAEM開發人員工具 {#how-to-install-the-aem-developer-tools-for-eclipse}

一旦你完成了 [要求](#requirements) 在上面，可以按如下方式安裝插件：

1. 開啟 [開發AEM人員工具網站。](https://eclipse.adobe.com/aem/dev-tools/)

1. 複製 **安裝連結**。

   請注意，您也可以下載存檔檔案，而不是使用安裝連結。 這允許離線安裝，但您會以這種方式錯過自動更新通知。

1. 在Eclipse中，開啟 **幫助** 的子菜單。
1. 按一下 **安裝新軟體**。
1. 按一下 **添加……**。
1. 在 **名稱** 輸入 `AEM Developer Tools`。
1. 在 **位置** 複製安裝URL。
1. 按一下&#x200B;**「新增」**。
1. 同時檢查 **AEM** 和 **吊帶** 插件。
1. 按一下&#x200B;**下一步**。
1. 在 **安裝詳細資訊** 窗口，按一下 **下一個** 的雙曲餘切值。
1. 接受許可協定，然後按一下 **完成**。
1. 按一下 **立即重新啟動** 來重新啟動Eclipse。

## 透AEM視 {#the-aem-perspective}

在Eclipse中，透視可確定窗口中可用的操作和視圖，並啟用面向任務的與Eclipse中資源的交互。 有關透視的詳細資訊，請參閱 [Eclipse文檔。](https://help.eclipse.org)

Development AEM Tools for Eclipse提供了AEM一個透視，讓您能夠完全控制AEM項目和實例。 要開啟透AEM視：

1. 從Eclipse菜單欄中選擇 **窗口** -> **透視** -> **開放透視** -> **其他**。
1. 選擇 **AEM** 中，按一下 **開啟**。

![《日蝕AEM》的透視](assets/eclipse-aem-perspective.png)

## 示例多模組項目 {#sample-multi-module-project}

Developer AEM Tools for Eclipse附帶了一個示例、多模組項目，它幫助您快速完成Eclipse中的項目設定，並作為幾項功能的最佳實踐指AEM南。 [瞭解有關項目原型的詳細資訊](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。

按照以下步驟建立示例項目：

1. 在 **檔案** > **新建** > **項目** 菜單，瀏覽至 **AEM** 選擇 **多模AEM塊項目示例**。

   ![多模AEM塊項目示例](assets/aem-sample-project.png)

1. 按一下&#x200B;**下一步**。

   >[!NOTE]
   >
   >此步驟可能需要一段時間，因為m2eclipse需要掃描原型目錄。

1. 選擇 `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` ，然後按一下 **下一個**。

   ![選擇原型版本](assets/select-archetype.png)

1. 為示例項目提供以下欄位：

   * **名稱**
   * **組ID**
   * **項目ID**
   * **應用ID**  — 您可能需要擴展 **高級** 選項來設定此值。
   * **appTitle**  — 您可能需要擴展 **高級** 選項來設定此值。
   * **包**  — 您可能需要擴展 **高級** 選項來設定此值。

   ![定義原型屬性](assets/archetype-properties.png)

1. 按一下&#x200B;**下一步**。

1. 然後配置EclipseAEM將連接到的伺服器。

   要使用調試器功能，您需要在調試AEM模式下啟動 — 這可以通過在命令行中添加以下內容來實現：

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![連接到服AEM務器](assets/connect-server.png)

1. 按一下 **完成**。 將建立項目結構。

   >[!NOTE]
   >
   >在新安裝（更具體地說，當從未下載過多個依賴項時），您可能會建立項目並出現錯誤。 在這種情況下，請按照中描述的過程操作 [解析無效的項目定義](#resolving-invalid-project-definition)。

## 如何導入現有項目 {#how-to-import-existing-projects}

您可以使用 **新建項目** 建立正確結構的特徵：

1. 按照說明建立 [示例多模組項目](#sample-multi-module-project) 您將為您建立以下項目，這將允許將關注事項進行健康分離：

   * `PROJECT.ui.apps` 為 `/apps` 和 `/etc` 內容
   * `PROJECT.ui.content` 為 `/content` 創作
   * `PROJECT.core` 對於Java捆綁包（一旦要添加Java代碼，這些將會變得有趣）
   * `PROJECT.it.launcher` 和 `PROJECT.it.tests` 用於整合test

1. 替換您的 `PROJECT.ui.apps` 項目 `apps` 和 `etc` 檔案包：

   1. 在「項目瀏覽器」面板中，展開 `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`。
   1. 按一下右鍵 `apps` 資料夾和 **顯示** > **系統瀏覽器**。
   1. 刪除 `apps` 和 `etc` 您現在應該看到的資料夾，並放在此處 `apps` 和 `etc` 內容包的資料夾。
   1. 在Eclipse中，按一下右鍵 `PROJECT.ui.apps` 項目和選擇 **刷新**。

1. 然後對 `PROJECT.ui.content` 並將其內容資料夾替換為包中的一個：

   1. 在「項目瀏覽器」面板中，展開 `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`。
   1. 按一下右鍵更深的內容資料夾並選擇 **顯示** -> **系統瀏覽器**。
   1. 刪除您現在應該看到的內容資料夾，並將內容包的內容資料夾放在此處。
   1. 在Eclipse中，按一下右鍵 `PROJECT.ui.content` 項目和選擇 **刷新**。

1. 現在您必須更新 `filter.xml` 這兩個項目的檔案與內容包的內容相對應。 為此，開啟 `META-INF/vault/filter.xml` 文本/代碼編輯器中的檔案。

   * 這是您 `filter.xml` 檔案可以查找：

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

1. 至於被拆分為兩個項目的包的內容，您還必須將這些篩選器規則拆分為兩個並相應地更新 `filter.xml` 兩個項目的檔案。

   1. 在日蝕中，開啟 `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`。
   1. 替換 `<workspaceFilter>` 元素，包的規則以 `/apps` 和 `/etc`
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
   1. 將規則替換為以 `/content`。
      * 例如：

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/content/foo"/>
            <filter root="/content/dam/foo"/>
            <filter root="/content/usergenerated/content/foo"/>
         </workspaceFilter>
         ```


1. 確保保存所有更改。 現在，您可以將新內容同步到實AEM例。

1. 在「伺服器」面板中，確保已啟動連接，如果未啟動連接，請確保已啟動連接。
1. 按一下 **清除並發佈** 表徵圖

完成後，您應在實例上運行包，在保存時，任何更改都會自動與實例同步。

如果希望從項目中重新生成包，請按一下右鍵 `PROJECT.ui.apps` 或 `PROJECT.ui.content` 選擇 **運行方式** -> **Maven安裝**。

現在，您有一個目標資料夾，它已在內部建立了包(例如， `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`)。

## 疑難排解 {#troubleshooting}

### 解析無效的項目定義 {#resolving-invalid-project-definition}

要解決無效的依賴項和項目定義，請按如下步驟進行：

1. 選擇所有已建立的項目。
1. 按一下右鍵。
1. 在上下文菜單中，選擇 **馬文** -> **更新項目**。
1. 檢查 **強制更新快照/版本**。
1. 按一下&#x200B;**「確定」**。

Eclipse下載所需的依賴項。 這可能需要一些時間。

## 詳細資訊 {#more-information}

用於Eclipse網站的Apache Sling IDE工具正式為您提供了有用的資訊：

* 的 [**用於Eclipse的Apache Sling IDE工具** 使用手冊](https://sling.apache.org/documentation/development/ide-tooling.html)，本文檔將指導您瞭解開發工具支援的總體概念、伺服器整合和部AEM署功能。
* 的 [「疑難解答」部分](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)。
* 的 [已知問題清單](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)。

以下官員 [日蝕](https://eclipse.org/) 文檔可幫助設定環境：

* [Eclipse入門](https://eclipse.org/users/)
* [Eclipse Luna幫助系統](https://help.eclipse.org/luna/index.jsp)
* [Maven整合(m2eclipse)](https://www.eclipse.org/m2e/)
