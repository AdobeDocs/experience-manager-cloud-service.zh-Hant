---
title: 內容轉移工具的必要條件
description: 內容轉移工具的必要條件
source-git-commit: ebe12a71df610a68c43048667136e331c1bd8f86
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 內容轉移工具的必要條件 {#prerequisites}

下表概述使用「內容轉移工具」的先決條件。 請檢閱下列所有考量事項：

| 考量事項 | 目前支援的項目 |
|--- |--- |
| AEM版本 | 「內容轉移工具」僅能在AEM 6.3或更新版本上執行。 若要搭配AEM 6.2或更舊版本使用「內容轉移工具」，需要將內容存放庫就地升級至AEM 6.5。 不需要將程式碼升級至AEM 6.5即可。 |
| 區段存放區大小 | 「內容轉移工具」目前在&#x200B;*Author*&#x200B;上支援高達83 GB，在&#x200B;*Publish*&#x200B;上支援高達31 GB。 |
| 內容存放庫總大小&#x200B;<br>*（內容存放區+資料存放區）* | 「內容轉移工具」的設計目的是將內容轉移至高達10 TB。 目前不支援高於10 TB的任何項目。 與Adobe客戶服務建立支援票證，討論大於10 TB內容的選項。 |
| 不可變路徑中的內容 | 「內容轉移工具」無法移轉不可變路徑（例如`“/etc”`）中的內容。 <br>請參考「 [共用資](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) 料庫重構」，深入了解存放庫重構和工作流程模型。 |