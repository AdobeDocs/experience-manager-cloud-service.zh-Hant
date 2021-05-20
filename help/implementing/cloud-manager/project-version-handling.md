---
title: Maven 專案版本處理
description: Maven專案版本處理 — Cloud Services
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 6%

---

# Maven 專案版本處理 {#maven-project-version-handling}


## 了解Maven項目版本處理{#understanding-project-version}

對於預備和生產部署，Cloud Manager會產生獨特的遞增版本。

可在管道執行詳細資訊頁面和活動頁面上看到此版本。 執行組建時，Maven專案會更新為使用此版本，並在Git存放庫中建立標籤，並以該版本為名稱。

如果原始專案版本符合特定條件，更新的Maven專案版本將會合併原始專案版本和Cloud Manager產生的版本。 不過，標籤一律會使用產生的版本。 要進行此合併，原始項目版本必須由三個版本段（例如1.0.0或1.2.3，但不是1.0或1）組成，且原始版本不得以 — SNAPSHOT結束。

如果原始版本確實符合此條件，則產生的版本會附加至原始版本，作為新版本區段。 產生的版本也會稍微修改，以包含正確的排序和版本處理。 例如，假設產生的2019.926.121356.0000020490版：

| **版本** | **pom.xml中的版本** | **評論** |
|---|---|---|
| 1.0.0 | 1.0.0.2019_0926_121356_0000020490 | 正確格式的原始版本 |
| 1.0.0快照 | 2019.926.121356.0000020490 | 快照版本，被覆蓋 |
| 1 | 2019.926.121356.0000020490 | 未完成版本，被覆蓋 |

>[!NOTE]
>
>無論原始版本是否整合到Cloud Manager初始化的版本中，原始版本都可作為名稱為&#x200B;*cloudManagerOriginalVersion的Maven屬性使用。*
