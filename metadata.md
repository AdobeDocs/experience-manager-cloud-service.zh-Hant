---
product: adobe experience manager
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.zh-Hant
index: y
type: Documentation
solution-title: 'Adobe Experience Manager as a Cloud Service '
solution-hub-url: https://experienceleague.adobe.com/docs/experience-manager-cloud-service/landing/home.html
getting-started-title: 快速入門
getting-started-url: https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/home.html
tutorials-title: 教學課程
tutorials-url: https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html
translation-type: tm+mt
source-git-commit: 8832307a96160a3d45cc85942473a5ada288a74f
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 10%

---


# 內部使用的中繼資料

GitHub製作系統中的中繼資料是階層式的，並定義了下列不斷提升的先例等級。

1. metadata.md
1. ToC
1. 文章

中繼資料。md檔案中定義的中繼資料會套用至整個回購區，但可在ToC和文章層級覆寫。 任何對中繼資料的覆寫都應盡可能在最低層級進行。

experience-manager-cloud-service.en repo中的中繼資料是最低要求。

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

ToCs

* `sub-product`
* `user-guide-title`

文章

* `title`
* `description`
* `contentOwner` (僅限核心資產內容於 `/help/assets`)
