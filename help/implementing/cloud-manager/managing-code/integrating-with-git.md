---
title: 搭配Cloud Manager使用Git
description: 了解如何使用Cloud Manager的Git存放庫，以及如何將您自己的內部部署客戶管理的Git存放庫與Cloud Manager整合。
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 搭配Cloud Manager使用Git {#git-integration}

AdobeCloud Manager已布建單一Git存放庫，可用來使用Cloud Manager的CI/CD管道部署程式碼。

您可以立即使用Cloud Manager的Git存放庫，但也可選擇將客戶管理的Git存放庫與Cloud Manager整合。

## Git整合概述 {#git-integration-overview}

此影片系列探討將客戶管理的Git存放庫與Cloud Manager整合時的數種使用案例，包括：

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支開發](#feature-development)
* [生產部署](#production-deployment)
* [同步發行標籤](#sync-tags)

影片系列假設您具備Git和原始碼控制管理的基本知識。 請參閱 [以下其他資源](#additional-resources) 如需git的詳細資訊。

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

此影片系列中概述的步驟和命名慣例，代表使用Cloud Manager中由客戶管理的Git存放庫時的一些最佳實務。 預期所描述的慣例和工作流程會針對個別使用案例進行調整。

## 初始同步 {#initial-sync}

此影片將說明同步客戶管理的Git存放庫與Cloud Manager的Git存放庫的前幾個步驟。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

此影片會說明基本的分支策略。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支開發 {#feature-development}

使用功能分支，隔離客戶管理之Git存放庫中的程式碼變更，並與Cloud Manager的Git存放庫同步，以便使用非生產管道進行程式碼品質和驗證測試。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生產部署 {#production-deployment}

在客戶管理的Git存放庫中準備生產版本的程式碼，並與Cloud Manager的Git存放庫同步，以便部署至預備和生產環境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步發行標籤 {#sync-tags}

將Cloud Manager Git存放庫的發行標籤同步至客戶管理的Git存放庫，以便掌握哪些程式碼已部署至測試和生產環境。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他資源 {#additional-resources}

* [GitHub資源](https://try.github.io)
* [Atlassian GitTutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git速查表](https://education.github.com/git-cheat-sheet-education.pdf)
