---
title: Maven 專案版本處理
description: 對於AEMas a Cloud Service的預備和生產部署，Cloud Manager會產生獨特的遞增版本。
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
source-git-commit: 21607fadf33dac038c7f794b933b92f60b8e20a9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 3%

---


# Maven 專案版本處理 {#maven-project-version-handling}

對於AEM as a Cloud Service的預備和生產部署，Cloud Manager會產生獨特的遞增版本

此版本會顯示在 [管道執行詳細資訊頁面](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) 以及活動頁面。 執行組建時，Maven專案會更新為使用此版本，並在Git存放庫中建立標籤，並以該版本為名稱。

如果原始專案版本符合特定條件，更新的Maven專案版本將會合併原始專案版本和Cloud Manager產生的版本。 不過，標籤一律會使用產生的版本。 要進行此合併，原始項目版本必須由三個版本段組成，例如 `1.0.0` 或 `1.2.3`，但不是 `1.0` 或 `1`，且原始版本不得結尾為 `-SNAPSHOT`.

>[!IMPORTANT]
>
>此原始項目版本值必須在 `<version>` 頂層的元素 `pom.xml` 檔案。

如果原始版本確實符合這些條件，則產生的版本會附加至原始版本，作為新版本區段。 產生的版本也會稍微修改，以包含正確的排序和版本處理。 例如，假設產生的 `2019.926.121356.0000020490` 會得到下列結果。

| 版本 | 版本於 `pom.xml` | 評論 |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | 正確格式的原始版本 |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | 快照版本，被覆蓋 |
| `1` | `2019.926.121356.0000020490` | 未完成版本，被覆蓋 |

>[!NOTE]
>
>無論原始版本是否整合至Cloud Manager初始化的版本，原始版本都可作為具有名稱的Maven屬性使用 `cloudManagerOriginalVersion`.
