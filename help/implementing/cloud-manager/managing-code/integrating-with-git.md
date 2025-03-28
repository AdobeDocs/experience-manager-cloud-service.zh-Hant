---
title: 搭配使用Git與Cloud Manager
description: 了解如何使用 Cloud Manager 的 Git 存放庫以及如何將您內部部署客戶管理的 Git 存放庫與 Cloud Manager 整合。
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 80206fc1396896fe45e2c959c78a0bf30eba71c5
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 95%

---

# 搭配使用Git與Cloud Manager {#git-integration}

Adobe Cloud Manager 佈建了一個 Git 存放庫，用於使用 Cloud Manager 的 CI/CD 管道部署程式碼。

您可以直接使用 Cloud Manager 的 Git 存放庫，也可以選擇將客戶管理的 Git 存放庫和 Cloud Manager 整合。

## Git 整合概觀 {#git-integration-overview}

本影片系列會介紹幾個整合客戶管理的 Git 存放庫與 Cloud Manager 的使用案例，包含：

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支開發](#feature-development)
* [生產部署](#production-deployment)
* [同步版本標記](#sync-tags)

本影片系列會假定您具備 Git 和原始程式碼控制管理的基本知識。如需有關 Git 的更多詳細資訊，請參閱[下列附加資源](#additional-resources)。

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

本影片系列中概述的步驟和命名慣例代表在 Cloud Manager 中使用客戶管理的 Git 存放庫的一些最佳做法。預計所描述的慣例和工作流程將適用於個別使用案例。

## 初始同步 {#initial-sync}

在本影片中，您將了解將客戶管理的 Git 存放庫和 Cloud Manager 的 Git 存放庫同步處理的第一步。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

在本影片中，您將學習基本的分支原則。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支開發 {#feature-development}

使用功能分支隔離客戶管理的 Git 存放庫中的程式碼變更並和 Cloud Manager 的 Git 存放庫同步，以便使用非生產管道進行程式碼品質和驗證測試。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生產部署 {#production-deployment}

在客戶管理的 Git 存放庫中為生產版本準備程式碼，並與 Cloud Manager 的 Git 存放庫同步，以便部署到測試和生產環境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步版本標籤 {#sync-tags}

將 Cloud Manager Git 存放庫中的版本標記同步到客戶管理的 Git 存放庫中，以便提供有關已將哪些程式碼部署到中繼和生產環境的可見度。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他資源 {#additional-resources}

* [GitHub 資源](https://docs.github.com/en/get-started/getting-started-with-git/set-up-git)
* [Atlassian Git 教學課程](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git 速查表](https://education.github.com/git-cheat-sheet-education.pdf)
