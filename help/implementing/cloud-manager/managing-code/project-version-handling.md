---
title: Maven 專案版本處理
description: 為了進行 AEM as a Cloud Service 的測試和生產部署，Cloud Manager 會產生一個唯一且遞增的版本。
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
source-git-commit: 21607fadf33dac038c7f794b933b92f60b8e20a9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 100%

---


# Maven 專案版本處理 {#maven-project-version-handling}

為了進行 AEM as a Cloud Service 的測試和生產部署，Cloud Manager 會產生一個唯一且遞增的版本

在[管道執行詳細資訊頁面](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)以及活動頁面上可看見此版本。執行組建時，會更新 Maven 專案以使用此版本，並在 Git 存放庫中建立一個標記，且以該版本命名。

如果原始專案版本滿足特定條件，則更新後的 Maven 專案版本會將原始專案版本和 Cloud Manager 產生的版本合併。但上述標記則會一直使用產生的版本。為了讓這種合併發生，原始專案版本必須由三個版本區段組成，例如，`1.0.0` 或 `1.2.3`，而非 `1.0` 或 `1`，且原始版本的末尾不得為 `-SNAPSHOT`。

>[!IMPORTANT]
>
>必須在 Git 存放庫分支中的`<version>`頂層元素`pom.xml`檔案中以靜態方式設定此原始專案版本值。

如果原始版本符合這些標準，則產生的版本將以新版本區段附加到原始版本。產生的版本也將受到微幅修改，以包括正確的排序和版本處理。例如，假設產生的版本 `2019.926.121356.0000020490` 會有以下結果。

| 版本 | 在 `pom.xml` 中的版本 | 評論 |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | 正確形成的原始版本 |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | 快照版本，被覆寫 |
| `1` | `2019.926.121356.0000020490` | 不完整的版本，被覆寫 |

>[!NOTE]
>
>無論原始版本是否合併到 Cloud Manager 初始化版本中，都可將原始版本用為 Maven 屬性，並命名為 `cloudManagerOriginalVersion`。
