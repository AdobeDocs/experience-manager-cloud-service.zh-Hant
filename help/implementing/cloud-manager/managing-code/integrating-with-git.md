---
title: 將Git與雲管理器一起使用
description: 瞭解如何使用Cloud Manager的Git儲存庫，以及如何將您自己的內部客戶管理的Git儲存庫與Cloud Manager整合。
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 將Git與雲管理器一起使用 {#git-integration}

AdobeCloud Manager配置了單個Git儲存庫，用於使用Cloud Manager的CI/CD管道部署代碼。

您可以使用Cloud Manager的Git儲存庫，但您也可以選擇將客戶管理的Git儲存庫與Cloud Manager整合。

## Git整合概述 {#git-integration-overview}

此視頻系列探討了在將客戶管理的Git儲存庫與Cloud Manager整合時的幾個使用情形，包括：

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支開發](#feature-development)
* [生產部署](#production-deployment)
* [同步釋放標籤](#sync-tags)

該視頻系列假設了Git和原始碼管理的基本知識。 查看 [其他資源](#additional-resources) 的子菜單。

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

此視頻系列中概述的步驟和命名約定代表了在Cloud Manager中使用客戶管理的Git儲存庫時的一些最佳做法。 預計所描述的公約和工作流將適用於個別使用案例。

## 初始同步 {#initial-sync}

在此視頻中，瞭解將客戶管理的Git儲存庫與Cloud Manager的Git儲存庫同步的第一步。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

在本視頻中，學習基本的分支策略。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支開發 {#feature-development}

使用功能分支隔離客戶管理的Git儲存庫中的代碼更改，並與Cloud Manager的Git儲存庫同步，以便使用非生產流水線進行代碼質量和驗證測試。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生產部署 {#production-deployment}

在客戶管理的git儲存庫中為生產版本準備代碼，並與Cloud Manager的git儲存庫同步，以便部署到舞台和生產環境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步釋放標籤 {#sync-tags}

將Cloud Manager Git儲存庫中的發行標籤同步到客戶管理的git儲存庫中，以便查看已部署到暫存和生產環境的代碼。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他資源 {#additional-resources}

* [GitHub資源](https://try.github.io)
* [阿特拉西安·吉特Tutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git作弊表](https://education.github.com/git-cheat-sheet-education.pdf)
