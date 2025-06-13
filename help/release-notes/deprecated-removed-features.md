---
title: 過時和移除的功能
description: 特定於  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 中已過時和已移除功能的版本注意事項。
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
feature: Release Information
role: Admin
source-git-commit: 1f6aabc76551340ed296571e14daf2a1ef557717
workflow-type: tm+mt
source-wordcount: '3181'
ht-degree: 96%

---

# 已過時和已移除的功能和 API {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEM as a Cloud Service 中已棄用和已移除的功能"
>abstract="AEM as a Cloud Service 具有雲端原生部署模型。此索引標籤會醒目提示已由其對應之雲生原生功能取代的特色與功能。"

Adobe 會定期檢閱包括 API 和設定在內的功能，確保其符合 AEM as a Cloud Service 在效能、安全性和整體價值方面不斷演進的標準。根據這些評估，某些功能可能會標記為棄用。在可行的情況下，Adobe 會提供合適的替代方案。

當宣布棄用時，該功能便僅能再使用一定的期間，客戶必須在任何指定的移除日期之前移除所有使用。Adobe 會提供合理的通知和指引，支援您平穩地進行轉變。

在棄用的時間範圍內，Adobe 會透過電子郵件通知、行動中心警示，或 Cloud Manager 中的提醒功能，提醒客戶轉變為停止使用某項功能時所需採取的動作。

>[!WARNING]
>
>在某些情況下，部署新的 Cloud Manager 版本或升級至最新版本的 AEM as a Cloud Service 之前，可能有必要移除某項功能。

## 棄用的功能 {#deprecated-features}

以下表格中的功能已宣佈為棄用，但尚未被移除。必須在目標移除日期之前停止使用這些功能，否則您會面臨與效能、可用性和安全性相關之問題的風險。

| 功能 | 汰除功能 | 替代方案 |
| ------------ | ------------------ | ----------- |
| Sites | [Assets HTTP API 中的內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md) | [透過 OpenAPI 傳遞 AEM 內容片段](/help/headless/aem-content-fragment-delivery-with-openapi.md)<br>以及<br> [內容片段與內容片段模型管理 OpenAPI](/help/headless/content-fragment-openapis.md) |
| Sites | [PWA 功能](/help/sites-cloud/authoring/sites-console/enable-pwa.md) | 無 |
| Sites | [SPA 編輯器](/help/implementing/developing/hybrid/introduction.md) | AEM 中用於管理 Headless 內容的首選編輯器為：<br>- [通用編輯器](/help/edge/wysiwyg-authoring/authoring.md)，用於視覺化編輯。<br>- [內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md)，用於表單型編輯。 |
| [!DNL Sites] | [JavaScript Use API](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) | [Java Use API](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-htl/content/java-use-api) |
| [!DNL Sites] | **社交媒體狀態**&#x200B;的體驗片段屬性。 | 此功能規劃於近日移除。 |
| Sites | [Experience Cloud 設定自動化](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md) | 無 |
| [!DNL Sites] | 基於範例的簡單內容片段。 | 現在[基於模型的結構化內容片段](/help/assets/content-fragments/content-fragments-models.md)。 |
| [!DNL Assets] | 處理所擷取影像的 `DAM Asset Update` 工作流程。 | 資產擷取現在使用[資產微服務](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 直接將資產上傳到 [!DNL Experience Manager]。請參閱[已過時的資產上傳 API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)。 | 使用[直接二進位上傳](/help/assets/add-assets.md)。如需技術詳細資訊，請參閱[直接上傳 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | 不支援 [ 工作流程中的](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)某些工作流程步驟`DAM Asset Update`，包括呼叫命令列工具，例如 [!DNL ImageMagick]. | [資產微服務](/help/assets/asset-microservices-overview.md)可取代許多工作流程。若要自訂處理程序，請使用[後期處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 影片轉碼。 | 若要產生 FFmpeg 縮圖，請使用[資產微服務](/help/assets/asset-microservices-overview.md)。若是 FFmpeg 轉碼，請使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |
| [!DNL Foundation] | 複寫代理程式之「散發」索引標籤下的樹狀結構複寫使用者介面 (2021 年 9 月 30 日後移除) | [管理發佈](/help/operations/replication.md#manage-publication)或[啟用樹狀工作流程步驟](/help/operations/replication.md#tree-activation)方法。 |
| [!DNL Foundation] | 複寫代理程式管理員畫面的「散發」標籤和複寫 API 無法用來複寫超過 10MB 的內容封裝。 | [管理發佈](/help/operations/replication.md#manage-publication)或[啟用樹狀工作流程步驟](/help/operations/replication.md#tree-activation) |
| [!DNL Foundation] | 使用自 Adobe Developer Console 專案產生的憑證進行整合，已逐漸不再具備對服務帳戶 (JWT) 認證的支援。自 2024 年 5 月 1 日起，無法在 Adobe Developer Console 中建立新的服務帳戶 (JWT) 認證。現有的服務帳戶 (JWT) 認證在 2025 年 1 月 1 日之前仍可用於已設定的整合，之後將停止運作，且會要求客戶移轉至 OAuth 伺服器對伺服器認證。[了解更多](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console)。 | [移轉](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration#migration-overview)至 OAuth Server-to-Server 憑證。 |
| [!DNL Foundation] | 用於複寫內容階層的發佈內容樹狀工作流程和相關的發佈內容樹狀工作流程步驟。 | 使用[啟用樹狀工作流程步驟](/help/operations/replication.md#tree-activation)，其效能更佳。 |
| [!DNL Foundation] | 使用 YUI 壓縮/縮小 JavaScript 用戶端資料庫。Adobe 不打算進一步更新 YUI 資料庫。 | Adobe 建議客戶切換至 Google Closure Compiler (GCC) 來進行實施。 |

## 移除的功能 {#removed-features}

本區段列出已移除的功能。

| 區域 | 功能 | 替代方案 | 目標移除日期 |
| ------------ | ------------------ | ----------- | ------------------- |
| 使用者介面 | 傳統 UI 已從產品使用者介面中移除。一些傳統 UI 對話框可用於一些選定的功能，例如連結檢查器、版本清除和一些 Cloud Service 設定。即將推出的[產品更新](/help/release-notes/home.md)可能會進一步移除傳統 UI 可用性。 | 標準 UI | 已移除 |
| [!DNL Dynamic Media] | 先前與 [Dynamic Media Classic](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/sites/administering/integration/scene7#integration) 和 [Dynamic Media 混合模式](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/assets/dynamic/config-dynamic#dynamic)整合無法在 [!DNL Experience Manager] as a [!DNL Cloud Service]中使用。 | 請使用 [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) (隨 [!DNL Experience Manager] as a [!DNL Cloud Service] 提供)。 | 已移除 |
| [!DNL Sites] | Portal Director 和 Portlet 元件 | 這些功能在 [!DNL Experience Manager] 6.4 中已過時，並已從 [!DNL Experience Manager] 中移除。 | 已移除 |
| [!DNL Sites] | Design Importer | 此功能已移除，因為無法在執行階段存取 [!DNL Experience Manager] 存放庫的不可修改區段。 | 已移除 |
| [!DNL Assets] | [!DNL Assets] 無法與 Assets 核心服務和 Creative Cloud 服務共用。 | 若要與 [!DNL Adobe Creative Cloud] 整合，請使用 [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。 | 已移除 |
| [!DNL Foundation] | 支援 Apache Sling 資料來源 (OSGi 套件組合 org.apache.sling.datasource) | 不適用 | 已移除 |
| [!DNL Foundation] | 支援 JST 指令碼範例 (OSGi 套件組合 org.apache.sling.scripting.jst) | 不適用 | 已移除 |
| [!DNL Foundation] | 支援 Apache Felix Http Whiteboard | OSGi Http Whiteboard | 2022 年 3 月 |
| [!DNL Foundation] | 支援 com.adobe.granite.oauth.server | Adobe IMS 整合  | 2023 年 3 月 |
| [!DNL Foundation] | 支援 org.apache.sling.serviceusermapping 功能以[取得服務使用者 ID](https://sling.apache.org/apidocs/sling12/org/apache/sling/serviceusermapping/ServiceUserMapper.html#getServiceUserID-org.osgi.framework.Bundle-java.lang.String-) | 不適用 | 2024 年 8 月 30 日 |
| [!DNL Foundation] | Java 11 執行階段已棄用，且 Adobe 已將其替換為 Java 21 執行階段。請注意，仍然可以使用 Java 11 建置程式碼 (Java 17 和 21 是其他選項) | Java 21 執行階段已套用。為了確保相容性，請務必按照[執行階段需求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)中所述更新資料庫版本。 | 3 月 2025 年 5 月 29 日 |

## 棄用的 API {#aem-apis}

下方表格中的 API (按一下將其展開查看內容) 已宣佈為棄用，但尚未移除。必須在目標移除日期之前停止使用這些 API，否則您會面臨與效能、可用性和安全性相關之問題的風險。部分 API 參照下方的 API 移除指引區段。

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
    <td>使用 Sling 的 Auth Core/Auth Core SPI 介面作為替代方法。<a href="#org.apache.sling.commons.auth">請參閱下面的移除說明。</a></td>
    <td>2015 年</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
<td>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.util<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread</td>
    <td>不再支援 Eclipse Jetty 和 Felix Http Jetty 套件。<a href="#org.eclipse.jetty">請參閱下面的移除說明。</a></td>
    <td>2021/5/27</td>
    <td>2025/8/31</td>
  </tr>
 <tr>     <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>AEM as a Cloud Service 不支援使用此 API。<a href="#com.mongodb">請參閱下面的移除說明。</a></td>
    <td>2021/5/27</td>
    <td>2025/8/31</td>
  </tr>
   <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>此 API 已過時，因為 Apache Abdera 自 2017 年以來已為淘汰專案。<a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">請參閱下面的移除說明。</a></td>
    <td>2021/7/29</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>此 API 已過時，因為 Apache Abdera 自 2017 年以來已為淘汰專案。<a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">請參閱下面的移除說明。</a></td>
    <td>2019/4/8</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>不再支援 Apache Felix Http Whiteboard。將您的程式碼移轉到 OSGi Http Whiteboard。<a href="#org.apache.felix.http.whiteboard">請參閱下面的移除說明。</a></td>
    <td>2022/1/27</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>此 API 已過時。請將您的程式碼移轉至 JDK 提供的 XML API。</td>
    <td>2022/1/27</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>AEM as a Cloud Service 不支援此內部 Logback API。<a href="#ch.qos.logback">請參閱下面的移除說明。</a></td>
    <td>2022/1/27</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>AEM as a Cloud Service 不支援此內部 log4j API。<a href="#org.slf4j">請參閱下面的移除說明。</a></td>
    <td>2022/1/27</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>Apache Log4j 1 已於 2015 年結束其生命週期，不再支援。<a href="#org.apache.log4j">請參閱下面的移除說明。</a></td>
    <td>2022/1/27</td>
    <td>2025/8/31</td>
  </tr>
  <tr>  <td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>Google Guava核心程式庫在Cloud Service中已過時。 <a href="#com.google.common">請參閱下面的移除說明。</a></td>
    <td>2023/5/15</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.slf4j.event</td>
    <td>AEM as a Cloud Service 不支援此內部 slf4j API。<a href="#org.slf4j">請參閱下面的移除說明。</a></td>
    <td>2022/4/11</td>
    <td>2025/8/31</td>
  </tr> 
    <tr>
    <td>com.drew.*</td>
    <td>若要從影像和影片中擷取中繼資料，應透過 Cloud Service 中的 Asset Compute 或透過 Apache POI 或 Apache Tika 完成。</td>
    <td>2024 年 9 月 17 日</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.blob。*</td>
    <td>此 API 僅供內部使用。</td>
    <td>2024/9/23</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.memory</td>
    <td>此 API 僅供內部使用。</td>
    <td>2024/9/23</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
<td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n<br>org.apache.felix.webconsole.spi</td>
    <td>雲端環境不支援 Felix 網頁控制台。<a href="#org.apache.felix.webconsole">請參閱下面的移除說明。</a></td>
    <td>2021/4/30</td>
    <td>2025/8/31</td>
  </tr>
<td>org.bson<br/>org.bson.assertions<br/>org.bson.codecs<br/>org.bson.codecs.configuration<br/>org.bson.codecs.pojo<br/>org.bson.codecs.pojo.annotations<br/>org.bson.conversions<br/>org.bson.diagnostics<br/>org.bson.internal<br/>org.bson.io<br/>org.bson.json<br/>org.bson.types<br/>org.bson.util</td>
    <td>AEM as a Cloud Service 不支援使用此 API。</td>
    <td>2022/10/31</td>
    <td>2025/8/31</td>
  </tr>  
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>待定</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td>建議並應該使用 Apache Johnzon 的 <a href="https://johnzon.apache.org/index.html">javax.json</a> 實作。 </td>
    <td>2021/4/30</td>
    <td>待定</td>
  </tr>
  <tr>
<td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>Commons Lang 2 處於維護模式。應該改用 Commons Lang 3。<a href="#apache.commons">請參閱下面的移除說明。</a></td>
    <td>2021/4/30</td>
    <td>待定</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>Commons Collections 3 處於維護模式。應該改用 Collections 4。<a href="#apache.commons">請參閱下面的移除說明。</a></td>
    <td>2021/4/30</td>
    <td>待定</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>此 API 已過時。請改用 Apache Sling 的產生器。</td>
    <td>10/31/2022</td>
    <td>待定</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>AEM as a Cloud Service 不支援此 API。</td>
    <td>2023/5/15</td>
    <td>待定</td>
  </tr>
  <tr>
    <td>com.day.cq.xss<br>com.day.cq.xss.taglib<br>com.day.cq.xss.impl</td>
    <td>請改用 org.apache.sling.xss。</td>
    <td>2023 年 12 月 12 日</td>
    <td>待定</td>
  </tr>
  <tr>
    <td>com.adobe.granite.xss<br>com.adobe.granite.xss.impl</td>
    <td>請改用 org.apache.sling.xss。</td>
    <td>2023 年 12 月 12 日</td>
    <td>待定</td>
  </tr>
  </tbody>
</table>
</details>

## 移除的 API {#removed-apis}

本區段列出已棄用及移除的 API。部分 API 參照下方的 API 移除指引區段。

<details>
  <summary>展開以查看已移除的 API 清單。</summary>
<table style="table-layout:auto">
  <tr>
    <th>套件/類別</th>
    <th>評論</th>
  </tr>
<tbody>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>使用 Sling 的 Discovery API 作為替代方法</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>AEM as a Cloud Service 不支援自訂持續性管理員。</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>建議您改用 Apache Felix HealthCheck API</td>
  </tr>
  <tr> <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml</td>
    <td>不再支援 Eclipse Jetty 和 Felix Http Jetty 套件。</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>Apache Felix 中繼類型和 SCR API 已過時。請改用 OSGi 中繼類型和宣告式服務 API。</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>記錄實作類別與 AEM as a Cloud Service 不相容。</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>舊版 AEM 6.x API。</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>Cloud Service 不支援此 API。</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>與 Apache Xerces 相關的 Util 類別已在後續版本中移除，導致主要版本變更。由於這些公用程式是供檔案保存庫內部使用，該 API 將從公用 API 表面淘汰。</td>
  </tr>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>舊版 AEM 6.x API。<a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">請參閱下面的移除說明。</a></td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>AEM as a Cloud Service 不支援此內部 Logback API。</td>
  </tr>
  <tr>
    <td>com.github.jknack.handlebars.js</td>
    <td>由於一項安全性弱點，Handlebars 必須從 4.0.5 升級到 4.3.0。此封裝不會再出現於升級後的 Handlebars 中。</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>此 API 不再受支援。請改用 org.apache.sling.api.resource.ResourceResolverFactory。</td>
  </tr>
  <tr>
    <td>org.apache.sling.repoinit.jcr<br>org.apache.sling.repoinit.parser.operations</td>
    <td>AEM as a Cloud Service 不支援使用此 API。</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.cache</td>
    <td>此 API 僅供內部使用。</td>
  </tr>
</tbody>
</table>
</details>

## API 移除指引 {#api-removal-guidance}

本區段反映上表中各種 API 的 API 移除指引。

### 移除 `org.apache.sling.commons.auth*` {#org.apache.sling.commons.auth}

如果您正在使用 `org.apache.sling.commons.auth` 或 `org.apache.sling.commons.auth.spi`，或兩者皆使用，可以分別透過將程式碼移轉至 `org.apache.sling.auth` 來取代。`org.apache.sling.auth.spi`。如果您使用的是舊版本的 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)，請務必更新至最新版本。

動作清單：

* 將 ACS AEM Commons 更新至最新版本 (至少應為 6.11.0)
* 從 `org.apache.sling.commons.auth` 和/或 `org.apache.sling.commons.auth.spi` 分別移轉至 `org.apache.sling.auth`、`org.apache.sling.auth.spi`。

### 移除 `org.apache.felix.webconsole*` {#org.apache.felix.webconsole}

若您使用來自 `org.apache.felix.webconsole*` 的封裝，請自專案中移除此程式碼。無法在 Cloud Service 中存取網頁控制台。

動作清單：

* 使用來自 `org.apache.felix.webconsole*` 的封裝移除程式碼

### 移除 `org.eclipse.jetty*` {#org.eclipse.jetty}

如果您使用封裝 `org.eclipse.jetty` 中的任何項目或其子封裝中的一項，您可能會想要移轉至具備類似功能的其他第三方程式庫。如果移轉不可行，請將下面清單中所需的套件組合新增至您的專案。

動作清單：

* 將使用的 `org.eclipse.jetty` 封裝取代為其他第三方程式庫/自己的程式碼或
* 從此清單中選取所需的套件組合，並將其新增至您的專案：
   * `org.eclipse.jetty:jetty-client:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-http:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-io:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-security:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-servlet:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-server:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util-ajax:9.4.54.v20240208`

### 移除 `com.mongodb` {#com.mongodb}

將 Mongo 用戶端 API 新增到您的專案中。

動作清單：

* 將此套件組合新增至您的專案
   * `org.mongodb:mongo-java-driver:3.12.7`

您可能會想要根據自己的需求，挑選不同的版本。

### 移除 `com.google.common*` {#com.google.common}

移除Google Guava Core Libraries的使用，或在您的專案中加入適當的版本。 在許多情況下，可以從JDK或Apache Commons Collections4的集合類別取代此程式庫的使用方式。 如果您找不到替代程式，請在專案中納入最新版的Google Guave核心程式庫。 如果您使用的是舊版本的 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)，請務必更新至最新版本。

動作清單：

* 將 ACS AEM Commons 更新至最新版本 (至少應為 6.11.0)
* 將Google Guava Core Library取代為JDK集合或Apache Commons集合4
* 如果仍然需要，請將此套件組合新增至您的專案（以最新可用版本取代）：
   * `com.google.guava:guava:33.4.8-jre`

### 移除 `Apache Commons Lang 2 and Apache Commons Collections 3` {#apache.commons}

移除未維護的 Apache Commons 資料庫使用，並以支援版本取代。在大多數情況下，只需要調整封裝匯入，唯有在某些情況下類別或方法才需要重新命名。如果您使用的是舊版本的 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)，請務必更新至最新版本。

動作清單：

* 將 ACS AEM Commons 更新至最新版本 (至少應為 6.11.0)
* 以 `org.apache.commons.lang3` 取代匯入 `org.apache.commons.lang*`
* 以 `org.apache.commons.collecitons4` 取代匯入 `org.apache.commons.collections*`

### 使用 `org.apache.abdera*` 和 `org.apache.sling.atom.taglib` {#org.apache.abdera_or_org.apache.sling.atom.taglib}

將使用來自 `org.apache.abdera` 和 `org.apache.sling.atom.taglib` 的任何封裝，取代為提供類似功能的第三方程式庫或您自己的程式碼。

動作清單：

* 將使用來自 `org.apache.abdera` 和 `org.apache.sling.atom.taglib` 的封裝取代為其他第三方程式庫/自己的程式碼。

### 使用 `org.apache.felix.http.whiteboard` {#org.apache.felix.http.whiteboard}

將使用 `org.apache.felix.http.whiteboard` 更換為 [OSGi Http Whiteboard](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)。官方 OSGi API 具備類似的功能，且更換通常只需要變更服務註冊屬性。

動作清單：

* 將使用 `org.apache.felix.http.whiteboard` 更換為 [OSGi Http Whiteboard](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)

### 使用 `ch.qos.logback*` {#ch.qos.logback}

Cloud Service 不支援 Logback，請移除其所有使用。如果您使用的是舊版本的 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)，請務必更新至最新版本。

動作清單：

* 將 ACS AEM Commons 更新至最新版本 (至少應為 6.11.0)
* 使用來自 `ch.qos.logback` 的封裝移除程式碼

### 使用 `org.slf4j.event and org.slf4j.spi` {#org.slf4j}

若您正在使用 `org.slf4j.event` 或者 `org.slf4j.spi`，請移除其所有使用。如果您使用的是舊版本的 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)，請務必更新至最新版本。

動作清單：

* 將 ACS AEM Commons 更新至最新版本 (至少應為 6.11.0)
* 使用 `org.slf4j.event` 和 `org.slf4j.spi` 移除程式碼

### 使用 `org.apache.log4j` {#org.apache.log4j}

若您正在使用 `org.apache.log4j` 切換至 SLF4J (`org.slf4j`) 或 Log4J 2.x (`org.apache.logging.log4j`)。

動作清單：

* 使用 `org.slf4j` (建議) 或 `org.apache.logging.log4j` 取代 `org.apache.log4j` 的使用

## OSGI 設定 {#osgi-configuration}

以下區段呈現 AEM as a Cloud Service OSGi 設定介面，說明客戶可以設定的內容。

1. 客戶程式碼不得設定所列出的 OSGi 設定。
1. 可以設定其屬性的 OSGi 設定清單，但必須遵守指定的驗證規則。這些規則包括是否需要聲明屬性、其類型以及在某些情況下允許的值範圍。

客戶程式碼可以設定任何未列出的 OSGi 設定。

這些規則會在 Cloud Manager 建置程序中進行驗證。未來可能會新增其他規則，預計執行日期已註明在表格中。客戶應在目標執行日期後遵守這些規則。若在移除日期之後未遵守規則，就會在 Cloud Manager 建置程序中產生錯誤。Maven 專案應包含 [AEM as a Cloud Service SDK 建置分析器 Maven 外掛程式](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin)，以在本機 SDK 開發期間標記 OSGI 設定錯誤。

有關 OSGI 設定的其他資訊可以在[此位置](/help/implementing/deploying/configuring-osgi.md)找到。

### 棄用的 OSGi 屬性 (即將轉為不可修改) {#deprecated-unmodifiable-osgi-properties}

以下 OSGi 元件 PID 的屬性已棄用，且應於執行日期前停止使用。

| **OSGI 元件 ID** | **不可修改的屬性** | **棄用** | **執行** |
|---|---|---|---|
| **`org.apache.sling.commons.log.LogManager`** | 全部 | 2025/4/24 | 2025/8/31 (於 6 月忽略設定) |
| **`org.apache.sling.commons.log.LogManager.factory.config`** | org.apache.sling.commons.log.file、org.apache.sling.commons.log.pattern | 2025/4/24 | 2025/8/31 (於 6 月忽略設定) |
| **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** | 全部 | 2024 | 2025/8/31 |
| **`com.adobe.granite.toggle.impl.dev.DynamicToggleProviderImpl`** | 全部 | 2025/6/3 | 2025/8/31 |
| **`org.apache.http.proxyconfigurator`** | 全部 | 2025/6/3 | 2025/8/31 |

### 不可修改的 OSGi 屬性 {#unmodifiable-osgi-properties}

如下所述，以下 OSGi 元件 PID 的屬性無法修改。

| **OSGI 元件 ID** | **不可修改的屬性** |
|---|---|
| **`com.day.cq.auth.impl.cug.CugSupportImpl`** |
| **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** | 全部 |
| **`com.adobe.granite.toggle.impl.ToggleRouterImpl`** | 全部 |
| **`org.apache.sling.engine.impl.log.RequestLoggerFilter`** | 全部 |
| **`org.apache.sling.feature.apiregions.impl`** | 全部 |
| **`org.apache.sling.jcr.resource.internal.helper.jcr.BinaryDownloadUriProvider`** | 全部 |
| **`com.adobe.cq.unifiedshell.impl.discovery.DiscoveryServlet`** | 全部 |
| **`com.adobe.cq.unifiedshell.impl.ui.FrameErrorHandler`** | 全部 |
| **`com.adobe.cq.unifiedshell.impl.config.UnifiedShellConfService`** | 全部 |
| **`com.adobe.cq.unifiedshell.impl.config.RepositoryIdentifier`** | 全部 |
| **`org.apache.sling.feature.apiregions.factory`** | 全部 |
| **`com.adobe.granite.toggle.monitor.systemproperty`** | 全部 |


### 未來將強制執行的 OSGi 屬性限制 {#future-restrictions-osgi-properties}

未來，Adobe 會強制執行以下 OSGi 屬性限制，因此應停止其使用。

| OSGi 元件 PID |   | 必要 | 類型 | 限制 (如適用) |
|---|---|---|---|---|
| `com.day.cq.mailer.DefaultMailService` | `smtp.host` |   | 字串 |   |
|   | `smtp.port` | 是 | 整數 | 「465」、「587」或「25」 |
|   | `smtp.user` |   | 字串 |   |
|   | `smtp.password` |   | 字串 |   |
|   | `from.address` |   | 字串 |   |
|   | `smtp.ssl` |   | 字串 |   |
|   | `smtp.starttls` |   | 布林值 |   |
|   | `smtp.requiretls` |   | 布林值 |   |
|   | `debug.email` |   | 布林值 |   |
|   | `oauth.flow` |   | 布林值 |   |
| `org.apache.sling.commons.log.LogManager.factory.config` | `org.apache.sling.commons.log.level` | 是 | 字串 | 「INFO」、「DEBUG」或「TRACE」 |
|   | `org.apache.sling.commons.log.names` |   | 字串陣列 |   |
|   | `org.apache.sling.commons.log.additiv` |   | 布林值 |   |
| `com.day.cq.commons.impl.ExternalizerImpl` | `externalizer.domains` | 否 | 字串[] |   |
|   | `externalizer.encodedpath` | 否 | 布林值 |   |
|   | `externalizer.host` | 否 | 字串 |   |
|   | `externalizer.contextpath` | 否 | 字串 |   |

### OSGi 屬性限制 {#restrictions-osgi-properties}

這些 OSGi 屬性的值會受到下方所述之規則的限制。

| OSGi 元件 PID |   | 必要 | 類型 | 限制 (如適用) |
|---|---|---|---|---|
| `org.apache.felix.eventadmin.impl.EventAdmin` | `org.apache.felix.eventadmin.ThreadPoolSize` | 是 | 整數 | 2-100 |
|   | `org.apache.felix.eventadmin.AsyncToSyncThreadRatio` |   | 雙精度浮點數 | -- |
|   | `org.apache.felix.eventadmin.AsyncToSyncThreadRatio` |   | 整數 | -- |
|   | `org.apache.felix.eventadmin.RequireTopic` |   | 布林值 | -- |
|   | `org.apache.felix.eventadmin.IgnoreTimeout` | 是 | 字串陣列 | 必須至少包括全部 `org.apache.felix*`、`org.apache.sling*`、`come.day*`、`com.adobe*` |
|   | `org.apache.felix.eventadmin.IgnoreTopic` |   | 字串陣列 | -- |
| `org.apache.felix.http` | `org.apache.felix.http.timeout` |   | 整數 |   |
|   | `org.apache.felix.http.session.timeout` |   | 整數 |   |
|   | `org.apache.felix.http.jetty.threadpool.max` |   | 整數 |   |
|   | `org.apache.felix.http.jetty.headerBufferSize` |   | 整數 |   |
|   | `org.apache.felix.http.jetty.requestBufferSize` |   | 整數 |   |
|   | `org.apache.felix.http.jetty.responseBufferSize` |   | 整數 |   |
|   | `org.apache.felix.http.jetty.maxFormSize` |   | 整數 |   |
|   | `org.apache.felix.https.jetty.session.cookie.httpOnly` |   | 布林值 |   |
|   | `org.apache.felix.https.jetty.session.cookie.secure` |   | 布林值 |   |
|   | `org.eclipse.jetty.servlet.SessionIdPathParameterName` |   | 字串 |   |
|   | `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding` |   | 布林值 |   |
|   | `org.eclipse.jetty.servlet.SessionCookie` |   | 字串 |   |
|   | `org.eclipse.jetty.servlet.SessionDomain` |   | 字串 |   |
|   | `org.eclipse.jetty.servlet.SessionPath` |   | 字串 |   |
|   | `org.eclipse.jetty.servlet.MaxAge` |   | 整數 |   |
|   | `org.eclipse.jetty.servlet.SessionScavengingInterval` |   | 整數 |   |
|   | `org.apache.felix.jetty.gziphandler.enable` |   | 布林值 |   |
|   | `org.apache.felix.jetty.gzip.minGzipSize` |   | 整數 |   |
|   | `org.apache.felix.jetty.gzip.compressionLevel` |   | 整數 |   |
|   | `org.apache.felix.jetty.gzip.inflateBufferSize` |   | 整數 |   |
|   | `org.apache.felix.jetty.gzip.syncFlush` |   | 布林值 |   |
|   | `org.apache.felix.jetty.gzip.excludedUserAgents` |   | 字串 |   |
|   | `org.apache.felix.jetty.gzip.includedMethods` |   | 字串陣列 |   |
|   | `org.apache.felix.jetty.gzip.excludedMethods` |   | 字串陣列 |   |
|   | `org.apache.felix.jetty.gzip.includedPaths` |   | 字串陣列 |   |
|   | `org.apache.felix.jetty.gzip.excludedPaths` |   | 字串陣列 |   |
|   | `org.apache.felix.jetty.gzip.includedMimeTypes` |   | 字串陣列 |   |
|   | `org.apache.felix.http.session.invalidate` |   | 布林值 |   |
|   | `org.apache.felix.http.session.container.attribute` |   | 字串陣列 |   |
|   | `org.apache.felix.http.session.uniqueid` |   | 布林值 |   |
| `org.apache.sling.scripting.cache` | `org.apache.sling.scripting.cache.size` | 是 | 整數 | >= 2048 |
|   | `org.apache.sling.scripting.cache.additional_extensions` | 是 | 字串陣列 | 必須包含「js」 |
| `org.apache.sling.engine.impl.log.RequestLogger` | `request.log.output` | 否 | 字串 |   |
|   | `request.log.outputtype` | 否 | 字串 |   |
|   | `request.log.entry.format` | 否 | 字串 |   |
|   | `request.log.exit.format` | 否 | 字串 |   |
|   | `request.log.enabled` | 否 | 字串 |   |
|   | `access.log.output` | 否 | 字串 |   |
|   | `access.log.outputtype` | 否 | 字串 |   |
|   | `access.log.enabled` | 否 | 字串 |   |
| `org.apache.sling.servlets.resolver.SlingServletResolver` | `servletresolver.servletRoot` | 否 | 字串 |   |
|   | `servletresolver.cacheSize` | 否 | 整數 |   |
|   | `servletresolver.paths` | 否 | 字串[] |   |
|   | `servletresolver.defaultExtensions` | 否 | 字串 |   |
|   | `servletresolver.mountProviders` | 否 | 布林值 |   |
|   | `servletresolver.scriptUser` | 否 | 字串 | 已棄用，請勿使用 |

## Java Runtime 更新至 21 版 {#java-runtime-update-21}

Adobe Experience Manager as a Cloud Service 已轉變為 Java 21 執行階段。為確保相容性，請務必按照[執行階段需求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)中所述更新資料庫版本。

