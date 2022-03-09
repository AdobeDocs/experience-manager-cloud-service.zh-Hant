---
title: Maven 專案版本處理
description: '對於as a Cloud Service的暫存和生AEM產部署，Cloud Manager會生成一個唯一的增量版本。 '
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
source-git-commit: 21607fadf33dac038c7f794b933b92f60b8e20a9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 3%

---


# Maven 專案版本處理 {#maven-project-version-handling}

對於as a Cloud Service的暫存和生AEM產部署，Cloud Manager會生成一個唯一的增量版本

在 [管道執行詳細資訊頁面](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) 以及活動頁面。 運行生成時，將更新Maven項目以使用此版本，並在Git儲存庫中建立一個標籤，該版本將作為其名稱。

如果原始項目版本滿足某些條件，則更新的Maven項目版本將合併原始項目版本和Cloud Manager生成的版本。 但是，標籤始終使用生成的版本。 要進行此合併，原始項目版本必須正好由三個版本段組成，例如， `1.0.0` 或 `1.2.3`，但 `1.0` 或 `1`，且原始版本不能以 `-SNAPSHOT`。

>[!IMPORTANT]
>
>必須在 `<version>` 頂層元素 `pom.xml` 檔案。

如果原始版本確實滿足這些條件，則生成的版本將作為新版本段附加到原始版本。 生成的版本也將稍作修改，以包括正確的排序和版本處理。 例如，假定生成的版本 `2019.926.121356.0000020490` 會得到以下結果。

| 版本 | 版本 `pom.xml` | 評論 |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | 格式正確的原始版本 |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | 快照版本，已覆蓋 |
| `1` | `2019.926.121356.0000020490` | 版本不完整，已覆蓋 |

>[!NOTE]
>
>無論原始版本是否已合併到Cloud Manager初始化的版本中，原始版本都可以作為名稱為Maven的屬性使用 `cloudManagerOriginalVersion`。
