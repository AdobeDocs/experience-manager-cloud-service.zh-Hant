---
title: OSGi設定API
description: AEM as aCloud ServiceOSGi配置曲面的說明
feature: Deploying
source-git-commit: 5223d57377f5c00b090aee1ddd4dbfe2d7113181
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# OSGi設定API

以下兩個清單會將AEM反映為Cloud ServiceOSGi設定表面，說明客戶可以設定哪些項目。

1. 不得由客戶代碼設定的OSGi設定清單
1. OSGi設定的清單，其屬性可能已設定，但必須遵守指定的驗證規則。 這些規則包括是否需要屬性聲明、屬性類型，以及某些情況下允許的值範圍。

如果未列出OSGI設定，則可依客戶代碼進行設定。

這些規則會在Cloud Manager建置程式期間進行驗證。 可隨時間新增其他規則，表格會列出預期的執行日期。 客戶應在目標實施日期前遵守這些規則。 在移除日期後未遵守規則，會在Cloud Manager建置程式中產生錯誤。 Maven專案應包含[AEM作為Cloud ServiceSDK建置分析程式Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html)，以在本機SDK開發期間標幟OSGI設定錯誤。

有關OSGI配置的其他資訊，請參見[此位置](/help/implementing/deploying/configuring-osgi.md)。

## 無法修改的OSGi配置 {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (公告日期：4/30/2021，執行日期：7/31/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (公告日期：4/30/2021，執行日期：7/31/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (公告日期：4/30/2021，執行日期：7/31/2021)
* **`org.apache.felix.http (Factory)`** (公告日期：4/30/2021，執行日期：7/31/2021)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** (公告日期：8/25/2021，執行日期：11/26/2021)

## OSGi設定需遵循組建驗證規則 {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** (公告日期：4/30/2021，執行日期：7/31/2021)
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * 類型：整數
      * 必要範圍：2-100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * 類型：兩次
   * `org.apache.felix.eventadmin.Timeout`
      * 類型：整數
   * `org.apache.felix.eventadmin.RequireTopic`
      * 類型：布林值
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * 必要
      * 類型：字串陣列
      * 必要範圍：必須至少包含`org.apache.felix*`、`org.apache.sling*`、`come.day*`、`com.adobe*`中的所有內容
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * 類型：字串陣列
* **`org.apache.felix.http`** (公告日期：4/30/2021，執行日期：7/31/2021)
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
* **`org.apache.sling.scripting.cache`** (公告日期：4/30/2021，執行日期：7/31/2021)
   * `org.apache.sling.scripting.cache.size`
      * 類型：整數
      * 必要範圍：>= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * 必要
      * 類型：字串陣列
      * 必要範圍：必須包含js
* **`com.day.cq.mailer.DefaultMailService`** (公告日期：4/30/2021，執行日期：7/31/2021)
   * `smtp.host`
      * 類型：字串
   * `smtp.port`
      * 類型：整數
      * 必要範圍：465、587或25
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
