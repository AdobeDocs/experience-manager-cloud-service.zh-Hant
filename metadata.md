---
product: adobe experience manager
description: Adobe Experience Manager as a Cloud Service檔案。
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.zh-Hant
index: y
type: Documentation
solution: Experience Manager
version: Cloud Service
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
source-git-commit: 5bc43af20dc8893303b1d1f4dc70939631933eb7
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 6%

---


# 內部使用的中繼資料

GitHub創作系統中的元資料是分層的，並且定義了以下不斷增加的先例級別。

1. metadata.md
1. 至
1. 文章

元資料.md檔案中定義的元資料適用於整個回購，但可以在ToC和文章級別被覆蓋。 元資料的任何覆蓋都應在盡可能最低的級別執行。

體驗管理器 — cloud-service.en repo中的元資料是最低要求的。

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

目標

* `sub-product`
* `user-guide-title`

文章

* `title`
* `description`
* `contentOwner` (僅限於 `/help/assets`)
