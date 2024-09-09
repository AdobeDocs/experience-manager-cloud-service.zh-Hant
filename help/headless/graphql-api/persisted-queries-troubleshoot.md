---
title: 疑難排解持續性 GraphQL 查詢
description: 了解如何在 Adobe Experience Manager as a Cloud Service 中疑難排解持續性 GraphQL 查詢問題。
feature: Headless, Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: ht
source-wordcount: '363'
ht-degree: 100%

---

# 疑難排解持續性 GraphQL 查詢 {#troubleshoot-persisted-graphql-queries}

[動作中心](/help/operations/actions-center.md)包含 **GraphQL** 持續性查詢錯誤警報。這代表每當您的 GraphQL 持續性查詢出現錯誤時，您都會收到通知。

為了幫助您排除並解決這些問題，本頁面介紹了&#x200B;*最常見*&#x200B;的失敗原因，以及如何修正這些問題的步驟。

## 內容片段模型的變更 {#changes-to-content-fragment-model}

當 GraphQL 持續性查詢是根據已過時的 GraphQL 類型時，該查詢可能會失敗，這通常是由於底層內容片段模型發生了改變。

此類錯誤可能是由多種原因引起。例子包括 (但不限於) 當內容片段模型的作者：

* 移除或重新命名欄位
* 更新&#x200B;**模型類型**，該類型定義了片段參考允許的模型。
* 取消發佈被其他模型參考的模型

若要解決此類錯誤，您應該：

* 更新失敗的持續性查詢，以適應對內容片段模型所做的改變
* 還原引起問題的模型改變

## GraphQL 端點未設定 {#graphql-endpoint-not-configured}

當持續性查詢傳回 `404` 錯誤代碼，並顯示 `No suitable endpoint found` 資訊時，這表示 AEM 環境中未設定 GraphQL 端點。

若要修正此問題，請按照「[管理 AEM 中的 GraphQL 端點](/help/headless/graphql-api/graphql-endpoint.md)」中的步驟來啟用和發佈您的端點。

## GraphQL 持續性查詢 URL 中缺少路徑 {#missing-path-query-url}

如果持續性查詢回傳 `400` 錯誤代碼，並顯示 `Suffix: '/' does not contain a path` 資訊，則表示呼叫 GraphQL servlet 時不包含路徑尾碼。

該模式應為 `/graphql/execute.json/thePath`。

## 由於 IP 允許清單而遭到封鎖 {#blocked-due-to-ip-allow-list}

在這種情況下，查詢將傳回 `405` 錯誤代碼。

這類錯誤並非 GraphQL 特有的問題。請參閱知識庫文章「[405 錯誤：不允許](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-20824)」。

## 被 Dispatcher 封鎖 {#blocked-dispatcher}

如果 GraphQL 端點在發佈 `POST` 要求時傳回 `404` 錯誤，這意味著 GraphQL 查詢在 Dispatcher 層級遭到封鎖，需要手動啟用該端點。

預設情況下不應出現這種情況，但自訂 Dispatcher 設定可能會導致此問題。如需進一步了解，請參閱「[Dispatcher - 使用 AEM Headless 進行端點設定](/help/headless/deployment/dispatcher.md)」。
