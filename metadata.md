---
product: adobe experience manager
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.zh-Hant
index: y
type: Documentation
solution-title: Adobe Experience Manager 雲端服務
solution-hub-url: https://docs.adobe.com/content/help/en/experience-manager-cloud-service/landing/home.html
getting-started-title: 快速入門
getting-started-url: https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/overview/home.html
tutorials-title: 教學課程
tutorials-url: https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html
translation-type: tm+mt
source-git-commit: d311c87c1ae1cdfe9f50d41750aecbab960dc7ef
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 20%

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

有關中繼資料的其他資訊，請參閱內 [部製作指南。](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/markdown/metadata.html#solution-metadata)
