---
title: 與Git整合
description: 與Git整合 — Cloud Services
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
source-git-commit: 21669a29fbfd1072b637f407f5220825c4d1edbb
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---

# 整合 Git 與 Adobe Cloud Manager {#git-integration}

AdobeCloud Manager已布建單一Git存放庫，可用來使用Cloud Manager的CI/CD管道部署程式碼。 客戶可立即使用Cloud Manager的Git存放庫。 客戶也可以選擇將內部部署或&#x200B;**customer-managed** git存放庫與Cloud Manager整合。

## Git整合概述 {#git-integration-overview}

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

此影片系列探討將客戶管理的Git存放庫與Cloud Manager整合的數個使用案例，包括：

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支開發](#feature-development)
* [生產部署](#production-deployment)
* [同步發行標籤](#sync-tags)

影片系列假設您具備Git和原始碼控制管理的基本知識。 如需Git的詳細資訊，請參閱下方的[其他資源。](#additional-resources)

>[!NOTE]
>
>此影片系列中概述的步驟和命名慣例，代表使用客戶管理的Git存放庫和Cloud Manager時的一些最佳實務。 預計所描述的公約和工作流程將適用於個別開發小組。

## 初始同步 {#initial-sync}

將客戶管理的Git存放庫與Cloud Manager的Git存放庫同步化的第一步。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

請觀看以下影片，了解基本的分支策略。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支開發 {#feature-development}

使用功能分支，隔離客戶管理之Git存放庫中的程式碼變更，並與Cloud Manager的Git存放庫同步，以便使用非生產管道進行程式碼品質和驗證測試。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生產部署 {#production-deployment}

在客戶管理的Git存放庫中準備生產版本的程式碼，並與Cloud Manager的Git存放庫同步，以便部署至預備和生產環境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步發行標籤 {#sync-tags}

將Cloud Manager Git存放庫的發行標籤同步至客戶管理的Git存放庫，以便掌握已部署至預備和生產環境的程式碼。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他資源 {#additional-resources}

* [GitHub資源](https://try.github.io)
* [Atlassian GitTutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git速查表](https://education.github.com/git-cheat-sheet-education.pdf)
