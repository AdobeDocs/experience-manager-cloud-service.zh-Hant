---
title: OSGi配置API
description: OSGi結構AEMas a Cloud Service表面描述
feature: Deploying
exl-id: 94d3df65-71d7-4442-8412-fe2cca7e79ff
source-git-commit: cba6648d7ef18f3cccbd9562f3a66d9c683ae852
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# OSGi配置API

下面的兩個清單反映AEM了as a Cloud Service的OSGi配置表面，描述了客戶可以配置什麼。

1. 不能由客戶代碼配置的OSGi配置清單
1. OSGi配置的清單，其屬性可以配置，但必須遵守指定的驗證規則。 這些規則包括是否需要聲明屬性、屬性類型，以及在某些情況下允許的值範圍。

如果未列出OSGI配置，則可能按客戶代碼配置。

這些規則在Cloud Manager生成過程中得到驗證。 可隨時間增加其他規則，表中註明了預期的執行日期。 客戶預期在目標實施日期之前遵守這些規則。 刪除日期後不遵守規則將在Cloud Manager生成過程中生成錯誤。 Maven項目應包括 [AEMas a Cloud ServiceSDK生成Analyzer Maven插件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html) 標籤本地SDK開發過程中的OSGI配置錯誤。

有關OSGI配置的其他資訊，請訪問 [此位置](/help/implementing/deploying/configuring-osgi.md)。

## 無法修改的OSGi配置 {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (公告日期：4/30/2021，實施日期：7/31/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (公告日期：4/30/2021，實施日期：7/31/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (公告日期：4/30/2021，實施日期：7/31/2021)
* **`org.apache.felix.http (Factory)`** (公告日期：4/30/2021，實施日期：7/31/2021)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** (公告日期：8/25/2021，實施日期：11/26/2021)

## 受生成驗證規則約束的OSGi配置 {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** (公告日期：4/30/2021，實施日期：7/31/2021)
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * 類型：整數
      * 所需範圍：2-100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * 類型：雙
   * `org.apache.felix.eventadmin.Timeout`
      * 類型：整數
   * `org.apache.felix.eventadmin.RequireTopic`
      * 類型：布爾
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * 必要
      * 類型：字串陣列
      * 所需範圍：必須至少包括 `org.apache.felix*`。 `org.apache.sling*`。 `come.day*`。 `com.adobe*`
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * 類型：字串陣列
* **`org.apache.felix.http`** (公告日期：4/30/2021，實施日期：7/31/2021)
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
      * 類型：布爾
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * 類型：布爾
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * 類型：字串
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * 類型：布爾
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
      * 類型：布爾
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * 類型：整數
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * 類型：整數
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * 類型：整數
   * `org.apache.felix.jetty.gzip.syncFlush`
      * 類型：布爾
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
      * 類型：布爾
   * `org.apache.felix.http.session.container.attribute`
      * 類型：字串陣列
   * `org.apache.felix.http.session.uniqueid`
      * 類型：布爾
* **`org.apache.sling.scripting.cache`** (公告日期：4/30/2021，實施日期：7/31/2021)
   * `org.apache.sling.scripting.cache.size`
      * 類型：整數
      * 所需範圍：>= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * 必要
      * 類型：字串陣列
      * 所需範圍：必須包括j
* **`com.day.cq.mailer.DefaultMailService`** (公告日期：4/30/2021，實施日期：7/31/2021)
   * `smtp.host`
      * 類型：字串
   * `smtp.port`
      * 類型：整數
      * 所需範圍：465、587或25
   * `smtp.user`
      * 類型：字串
   * `smtp.password`
      * 類型：字串
   * `from.address`
      * 類型：字串
   * `smtp.ssl`
      * 類型：字串
   * `smtp.starttls`
      * 類型：布爾
   * `smtp.requiretls`
      * 類型：布爾
   * `debug.email`
      * 類型：布爾
   * `oauth.flow`
      * 類型：布爾
* **`org.apache.sling.commons.log.LogManager.factory.config`** (公告日期：11/16/21，實施日期：2/16/21)
   * `org.apache.sling.commons.log.level`
      * 類型：枚舉
      * 所需範圍：資訊、調試或TRACE
   * `org.apache.sling.commons.log.names`
      * 類型：字串
   * `org.apache.sling.commons.log.file`
      * 類型：字串
   * `org.apache.sling.commons.log.additiv`
      * 類型：布爾