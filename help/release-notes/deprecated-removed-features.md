---
title: 過時和移除的功能
description: 特定於  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 中已過時和已移除功能的版本注意事項。
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: cb2c883fbadc5347dbe5fc50337abc41d4f5cec3
workflow-type: ht
source-wordcount: '2068'
ht-degree: 100%

---

# 已過時和已移除的功能和 API {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEM as a Cloud Service 中已過時和已移除的功能"
>abstract="AEM as a Cloud Service 具有雲端原生部署模型。某些功能和特性已由對應的雲生原生功能取代，此標籤顯示了這些功能。"


Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。此外，由於 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 提供雲端原生部署模型，因此某些功能已由對應的雲端原生功能取代。

若要傳達 [!DNL Experience Manager] 功能即將移除/取代的訊息，請套用下列規則：

1. 首先需公告功能已過時。過時的功能仍可使用，但往後不會有所改善。
1. 已宣佈過時的功能最快會從後續的主要版本中移除。公告預定的實際移除日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節提供 [!DNL Experience Manager] as a [!DNL Cloud Service] 中標示為過時的功能。 日後版本通常會先將移除的功能設為過時，並提供其他選項。

建議客戶檢閱是否在目前的部署中使用這些功能，並規劃變更實作，改用所提供的替代方案。

| 功能 | 汰除功能 | 替代方案 |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | **社交媒體狀態**&#x200B;的體驗片段屬性。 | 該功能不久將移除。 |
| [!DNL Sites] | 基於範例的簡單內容片段。 | 現在[基於模型的結構化內容片段](/help/assets/content-fragments/content-fragments-models.md)。 |
| [!DNL Assets] | 處理所擷取影像的 `DAM Asset Update` 工作流程。 | 資產擷取現在使用[資產微服務](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 直接將資產上傳到 [!DNL Experience Manager]。請參閱[已過時的資產上傳 API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)。 | 使用[直接二進位上傳](/help/assets/add-assets.md)。如需技術詳細資訊，請參閱[直接上傳 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | 不支援 [ 工作流程中的](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)某些工作流程步驟`DAM Asset Update`，包括呼叫命令列工具，例如 [!DNL ImageMagick]. | [資產微服務](/help/assets/asset-microservices-overview.md)可取代許多工作流程。若要自訂處理程序，請使用[後期處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 影片轉碼。 | 若要產生 FFmpeg 縮圖，請使用[資產微服務](/help/assets/asset-microservices-overview.md)。若是 FFmpeg 轉碼，請使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |
| [!DNL Foundation] | 複寫代理程式的「散發」標籤下的樹狀結構複寫 UI (2021 年 9 月 30 日後移除) | [管理出版物](/help/operations/replication.md#manage-publication)或[發佈內容樹工作流程](/help/operations/replication.md#publish-content-tree-workflow)方法 |
| [!DNL Foundation] | 複寫代理程式管理員畫面的「散發」標籤和複寫 API 都不能用於複寫超過 10MB 的內容套件。請改用[管理出版物](/help/operations/replication.md#manage-publication)或[發佈內容樹工作流程](/help/operations/replication.md#publish-content-tree-workflow) |

## 移除的功能 {#removed-features}

本節提供已從具 [!DNL Experience Manager] 之 [!DNL Experience Manager] as a [!DNL Cloud Service] 中移除的功能。

| 區域 | 功能 | 替代方案 | 目標移除日期 |
| ------------ | ------------------ | ----------- | ------------------- |
| 使用者介面 | 傳統 UI 已從產品使用者介面中移除。一些傳統 UI 對話框可用於一些選定的功能，例如連結檢查器、版本清除和一些 Cloud Service 設定。即將推出的[產品更新](/help/release-notes/home.md)可能會進一步移除傳統 UI 可用性。 | 標準 UI | 已移除 |
| [!DNL Dynamic Media] | 先前與 [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) 和 [Dynamic Media 混合模式](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic)整合無法在 [!DNL Experience Manager] as a [!DNL Cloud Service]中使用。 | 請使用 [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) (隨 [!DNL Experience Manager] as a [!DNL Cloud Service] 提供)。 | 已移除 |
| [!DNL Sites] | Portal Director 和 Portlet 元件 | 這些功能在 [!DNL Experience Manager] 6.4 中已過時，並已從 [!DNL Experience Manager] 中移除。 | 已移除 |
| [!DNL Sites] | Design Importer | 此功能已移除，因為無法在執行階段存取 [!DNL Experience Manager] 存放庫的不可修改區段。 | 已移除 |
| [!DNL Assets] | [!DNL Assets] 無法與 Marketing Cloud Assets 核心服務和 Creative Cloud 服務共用。 | 若要與 [!DNL Adobe Creative Cloud] 整合，請使用 [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。 | 已移除 |
| [!DNL Foundation] | 支援 Apache Sling 資料來源 (OSGi 套件組合 org.apache.sling.datasource) | 不適用 | 已移除 |
| [!DNL Foundation] | 支援 JST 指令碼範例 (OSGi 套件組合 org.apache.sling.scripting.jst) | 不適用 | 已移除 |
| [!DNL Foundation] | 支援 Apache Felix Http Whiteboard | OSGi Http Whiteboard | 2022 年 3 月 |
| [!DNL Foundation] | 支援 com.adobe.granite.oauth.server | Adobe IMS 整合  | 2023 年 3 月 |

## OSGI 設定 {#osgi-configuration}

以下兩個清單列出了 AEM as a Cloud Service OSGi 設定介面，說明客戶可以設定的內容。

1. 不得由客戶代碼設定的 OSGi 設定清單
1. 可以設定其屬性的 OSGi 設定清單，但必須遵守指定的驗證規則。這些規則包括是否需要聲明屬性、其類型以及在某些情況下允許的值範圍。

如果有 OSGI 設定未列出，則可由客戶代碼進行設定。

這些規則會在 Cloud Manager 建置程序中進行驗證。未來可能會新增其他規則，預計執行日期已註明在表格中。客戶應在目標執行日期後遵守這些規則。在移除日期之後不遵守規則將會在 Cloud Manager 建置程序中發生錯誤。Maven 專案應包含 [AEM as a Cloud Service SDK 建置分析器 Maven 外掛程式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html)，以在本機 SDK 開發期間標記 OSGI 設定錯誤。

有關 OSGI 設定的其他資訊可以在[此位置](/help/implementing/deploying/configuring-osgi.md)找到。

+++無法修改的 OSGi 設定。
* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`**(公告日期：2021 年 4 月 30 日，執行日期：2021 年 7 月 31 日)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`**(公告日期：2021 年 4 月 30 日，執行日期：2021 年 7 月 31 日)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`**(公告日期：2021 年 4 月 30 日，執行日期：2021 年 7 月 31 日)
* **`org.apache.felix.http (Factory)`**(公告日期：2021 年 4 月 30 日，執行日期：2021 年 7 月 31 日)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`**(公告日期：2021 年 8 月 25 日，執行日期：2021 年 11 月 26 日)
+++

+++OSGi 設定須遵守建置驗證規則。
* **`org.apache.felix.eventadmin.impl.EventAdmin`**(公告日期：2021 年 4 月 30 日，執行日期：2021 年 7 月 31 日)
* `org.apache.felix.eventadmin.ThreadPoolSize`
   * 類型：整數
   * 所需範圍：2-100
* `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
   * 類型：兩次
* `org.apache.felix.eventadmin.Timeout`
   * 類型：整數
* `org.apache.felix.eventadmin.RequireTopic`
   * 類型：布林值
* `org.apache.felix.eventadmin.IgnoreTimeout`
   * 必填
   * 類型：字串陣列
   * 所需範圍：必須至少包括全部 `org.apache.felix*`、`org.apache.sling*`、`come.day*`、`com.adobe*`
* `org.apache.felix.eventadmin.IgnoreTopic`
   * 類型：字串陣列
* **`org.apache.felix.http`**(公告日期：2021 年 4 月 30 日，執行日期：2021 年 7 月 31 日)
   * `org.apache.felix.http.timeout`
      * 類型：整數
   * `org.apache.felix.http.session.timeout`
      * 類型：整數
   * `org.apache.felix.http.jetty.threadpool.max`
      * 類型：整數
   * `org.apache.felix.http.jetty.headerBufferSize`
      * 類型：整數
   * `org.apache.felix.http.jetty.requestBufferSize`
      * 類型：整數
   * `org.apache.felix.http.jetty.responseBufferSize`
      * 類型：整數
   * `org.apache.felix.http.jetty.maxFormSize`
      * 類型：整數
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * 類型：布林值
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * 類型：布林值
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * 類型：字串
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * 類型：布林值
   * `org.eclipse.jetty.servlet.SessionCookie`
      * 類型：字串
   * `org.eclipse.jetty.servlet.SessionDomain`
      * 類型：字串
   * `org.eclipse.jetty.servlet.SessionPath`
      * 類型：字串
   * `org.eclipse.jetty.servlet.MaxAge`
      * 類型：整數
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * 類型：整數
   * `org.apache.felix.jetty.gziphandler.enable`
      * 類型：布林值
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * 類型：整數
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * 類型：整數
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * 類型：整數
   * `org.apache.felix.jetty.gzip.syncFlush`
      * 類型：布林值
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * 類型：字串
   * `org.apache.felix.jetty.gzip.includedMethods`
      * 類型：字串陣列
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * 類型：字串陣列
   * `org.apache.felix.jetty.gzip.includedPaths`
      * 類型：字串陣列
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * 類型：字串陣列
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * 類型：字串陣列
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * 類型：字串陣列
   * `org.apache.felix.http.session.invalidate`
      * 類型：布林值
   * `org.apache.felix.http.session.container.attribute`
      * 類型：字串陣列
   * `org.apache.felix.http.session.uniqueid`
      * 類型：布林值
* **`org.apache.sling.scripting.cache`**(公告日期：2021 年 4 月 30 日，執行日期：2021 年 7 月 31 日)
   * `org.apache.sling.scripting.cache.size`
      * 類型：整數
      * 所需範圍：>= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * 必填
      * 類型：字串陣列
      * 所需範圍：必須包含 js
* **`com.day.cq.mailer.DefaultMailService`**(公告日期：2021 年 4 月 30 日，執行日期：2021 年 7 月 31 日)
   * `smtp.host`
      * 類型：字串
   * `smtp.port`
      * 類型：整數
      * 所需範圍：465、587 或 25
   * `smtp.user`
      * 類型：字串
   * `smtp.password`
      * 類型：字串
   * `from.address`
      * 類型：字串
   * `smtp.ssl`
      * 類型：字串
   * `smtp.starttls`
      * 類型：布林值
   * `smtp.requiretls`
      * 類型：布林值
   * `debug.email`
      * 類型：布林值
   * `oauth.flow`
      * 類型：布林值
* **`org.apache.sling.commons.log.LogManager.factory.config`**(公告日期：2021 年 11 月 16 日，執行日期：2021 年 2 月 16 日)
   * `org.apache.sling.commons.log.level`
      * 類型：分項清單
      * 所需範圍：INFO、DEBUG 或 TRACE
   * `org.apache.sling.commons.log.names`
      * 類型：字串
   * `org.apache.sling.commons.log.file`
      * 類型：字串
   * `org.apache.sling.commons.log.additiv`
      * 類型：布林值
+++

## AEM API {#aem-apis}

以下是已過時的 AEM API 及其預期移除日期的詳盡清單。客戶應在目標移除日期之前從他們的程式碼中移除 API。在移除日期之後使用 API 將在本機 SDK/開發環境和 Cloud Manager 組建過程中產生錯誤。

<details>
  <summary>展開以查看已過時的 API 清單。</summary>
<table style="table-layout:auto">
  <tr>
    <th>套件/類別</th>
    <th>評論</th>
    <th>過時日期</th>
    <th>目標移除日期</th>
  </tr>
<tbody>
  <tr>
    <td>org.apache.sling.commons.auth<br> org.apache.sling.commons.auth.spi</td>
    <td>使用 Sling 的 Auth Core / Auth Core SPI 介面作為替代方法</td>
    <td>2015</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>使用 Sling 的 Discovery API 作為替代方法</td>
    <td>2015</td>
    <td>已移除</td>
  </tr>
  <tr>
    <td>org.apache.sling.settings</td>
    <td>AEM as a Cloud Service 在執行階段不支援執行模式或檔案系統存取。 </td>
    <td>10/5/20</td>
    <td>2021 年尾</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
    <td>3/1/21</td>
    <td>已移除</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
    <td>3/5/21</td>
    <td>已移除</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td>建議並應該使用 Apache Johnzon 的 <a href="https://johnzon.apache.org/index.html">javax.json</a> 實作。 </td>
    <td>4/30/21</td>
    <td>12/31/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>AEM as a Cloud Service 不支援自訂持續性管理員。</td>
    <td>4/30/21</td>
    <td>已移除</td>
  </tr>
  <tr>
    <td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>Commons Lang 2 處於維護模式。應該改用 Commons Lang 3。</td>
    <td>4/30/21</td>
    <td>12/31/21</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>Commons Collections 3 處於維護模式。應該改用 Collections 4。</td>
    <td>4/30/21</td>
    <td>12/31/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>建議您改用 Apache Felix HealthCheck API</td>
    <td>4/30/21</td>
    <td>已移除</td>
  </tr>
  <tr>
    <td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n</td>
    <td>雲端環境不支援 Felix Web 主控台</td>
    <td>4/30/21</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml<br>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.client.util</td>
    <td>不再支援 Eclipse Jetty 和 Felix Http Jetty 套件。</td>
    <td>5/27/21</td>
    <td>8/26/21</td>
  </tr>
  <tr>
    <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>AEM as a Cloud Service 不支持使用此 API。</td>
    <td>5/27/21</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>Apache Felix 中繼類型和 SCR API 已過時。請改用 OSGi 中繼類型和宣告式服務 API。</td>
    <td>5/27/21</td>
    <td>已移除</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>記錄實作類別與 AEM as a Cloud Service 不相容。</td>
    <td>7/4/21</td>
    <td>已移除</td>
  </tr>
  <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>此 API 已過時，因為 Apache Abdera 自 2017 年以來已為淘汰專案。</td>
    <td>7/29/21</td>
    <td>09/29/21</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>此 API 已過時，因為 Apache Abdera 自 2017 年以來已為淘汰專案。</td>
    <td>4/8/19</td>
    <td>09/29/21</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>舊版 AEM 6.x API。</td>
    <td>4/8/19</td>
    <td>已移除</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>Cloud Service 不支援此 API。</td>
    <td>9/30/21</td>
    <td>已移除</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>與 Apache Xerces 相關的 Util 類別已在後續版本中移除，導致主要版本變更。由於這些 Util 供 Filevault 內部使用，該 API 已從公用 API 表面淘汰。</td>
    <td>9/1/21</td>
    <td>已移除</td>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>舊版 AEM 6.x API。</td>
    <td>4/8/19</td>
    <td>09/29/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>不再支援 Apache Felix Http Whiteboard。將您的程式碼移轉到 OSGi Http Whiteboard。</td>
    <td>1/27/2022</td>
    <td>03/24/2022</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>此 API 已過時，將您的程式碼移轉到 JDK 提供的 XML API。</td>
    <td>1/27/2022</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>AEM as a Cloud Service 不支援此內部 Logback API。</td>
    <td>1/27/2022</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>AEM as a Cloud Service 不支援此內部 log4j API。</td>
    <td>1/27/2022</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>Apache Log4j 1 已於 2015 年結束生命週期，不再受支援。</td>
    <td>1/27/2022</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>AEM as a Cloud Service 不支援此內部 Logback API。</td>
    <td>1/27/2022</td>
    <td>已移除</td>
  </tr>
  <tr>
    <td>com.github.jknack.handlebars.js</td>
    <td>由於安全性漏洞，Handlebars 必須從 4.0.5 升級到 4.3.0。此套件不再出現在升級後的 Handlebars 中。</td>
    <td>5/5/2022</td>
    <td>8/5/2022</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>此 API 不再受支援。請改用 org.apache.sling.api.resource.ResourceResolverFactory。</td>
    <td>9/29/2022</td>
    <td>11/24/2022</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>此 API 已過時。請改用 Apache Sling 的產生器。</td>
    <td>10/31/2022</td>
    <td>01/01/2023</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>AEM as a Cloud Service 不支援此 API。</td>
    <td>5/15/2023</td>
    <td>6/15/2023</td>
  </tr><td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>Google Guava 核心程式庫已過時。</td>
    <td>5/15/2023</td>
    <td>6/15/2023</td>
  </tr>
</tbody>
</table>
</details>
