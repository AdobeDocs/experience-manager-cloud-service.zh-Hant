---
title: 與Git整合
description: 與Git整合——雲端服務
translation-type: tm+mt
source-git-commit: 57206e36725e28051b2468d47da726e318bd763b
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---


# 整合 Git 與 Adobe Cloud Manager {#git-integration}

Adobe Cloud Manager提供單一Git儲存庫，用來使用Cloud Manager的CI/CD管道部署程式碼。 客戶可以立即使用Cloud Manager的git儲存庫。 客戶也可以選擇將內部部署或客戶管理的 **Git儲存庫** 與Cloud Manager整合。

## Git整合概觀 {#git-integration-overview}

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

本影片系列探討在將客戶管理的Git儲存庫與Cloud Manager整合時的幾個使用案例，包括：

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支開發](#feature-development)
* [生產部署](#production-deployment)
* [同步發行標籤](#sync-tags)

視訊系列具備Git和來源控制管理的基本知識。 請參閱下 [面的其他資源](#additional-resources) ，以取得git的詳細資訊。

>[!NOTE]
>
> 此系列影片中概述的步驟和命名慣例代表使用客戶管理的Git儲存庫和Cloud Manager的一些最佳實務。 預計所說明的慣例和工作流程將適用於個別開發團隊。

## 初始同步 {#initial-sync}

將客戶管理的Git儲存庫與Cloud Manager的Git儲存庫同步的第一步。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

請依照以下影片瞭解基本分支策略。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支開發 {#feature-development}

使用功能分支隔離客戶管理的Git儲存庫中的程式碼變更，並與Cloud Manager的Git儲存庫同步，以便使用非生產管道進行程式碼品質和驗證測試。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生產部署 {#production-deployment}

在客戶管理的git儲存庫中準備生產版本的程式碼，並與Cloud Manager的git儲存庫同步，以便部署至存放和生產環境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步發行標籤 {#sync-tags}

將Cloud Manager Git儲存庫中的釋放標籤同步到客戶管理的git儲存庫中，以便能夠查看哪些代碼已部署到存放和生產環境。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他資源 {#additional-resources}

* [GitHub資源](https://try.github.io)
* [Atlassian Git教學課程](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)