---
title: 疑難排解持續的GraphQL查詢
description: 瞭解如何疑難排解Adobe Experience Manager as a Cloud Service中的持續性GraphQL查詢問題。
feature: Content Fragments,GraphQL API
source-git-commit: c8ea9846600d1773e6f269973635f5338f31906f
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# 疑難排解持續的GraphQL查詢 {#troubleshoot-persisted-graphql-queries}

此 [動作中心](/help/operations/actions-center.md) 包含 **GraphQL持續查詢錯誤** 警報。 這表示只要您的其中一個GraphQL持續查詢擲回錯誤，就會通知您。

為協助您疑難排解並解決這類問題，我們將 *最常見* 失敗的原因，以及如何修正的步驟。

## 內容片段模式的變更 {#changes-to-content-fragment-model}

GraphQL持續查詢如果以過時的GraphQL型別為基礎，則可能會失敗，通常是因為基礎內容片段模式發生變更。

發生此狀況可能有各種原因。 例如，當內容模型作者時：

* 移除或重新命名欄位
* 更新為片段參考定義的允許模型
* 取消發佈由其他模型參考的模型
* 其他動作和原因

若要解決此問題，請執行下列其中一個動作：

* 失敗的持續查詢應更新以容納內容片段模型的變更
* 或導致問題的模型變更應恢復

## 未設定GraphQL端點 {#graphql-endpoint-not-configured}

當持續查詢傳回 `400` 或 `500` 錯誤代碼，以及資訊 `No suitable endpoint found`，這表示在AEM環境中未設定任何GraphQL端點。

若要修正此問題，請依照啟用和發佈端點的步驟操作 [在AEM中管理GraphQL端點](/help/headless/graphql-api/graphql-endpoint.md).

## GraphQL持續查詢URL中缺少路徑 {#missing-path-query-url}

如果持續查詢傳回 `400` 或 `500` 含資訊的錯誤碼 `Suffix: '/' does not contain a path`，則呼叫GraphQL servlet時不含路徑尾碼。

模式應為 `/graphql/execute.json/thePath`.

## 由於IP允許清單而遭到封鎖 {#blocked-due-to-ip-allow-list}

在這種情況下，查詢會傳回 `405` 錯誤碼。

這不是GraphQL專屬的行為。 請參閱知識庫文章 [405不允許錯誤](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-20824.html).

## 已被Dispatcher封鎖 {#blocked-dispatcher}

如果GraphQL端點傳回 `404` 下列專案的發佈錯誤： `POST` 這表示GraphQL查詢在Dispatcher層級遭到封鎖，且端點需要手動啟用。

根據預設，不應該是這種情況，但自訂Dispatcher設定可能會導致此問題。 檢視下方的更多資訊 [Dispatcher — 使用AEM Headless進行端點設定](/help/headless/deployment/dispatcher.md).
