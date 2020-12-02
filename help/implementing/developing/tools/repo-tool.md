---
title: AEM Repo工具
description: AEM Repo Tool是一套簡單的解決方案，可讓您透過類似FTP的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# AEM Repo Tool {#aem-repo-tool}

AEM Repo Tool是一套簡單的解決方案，可讓您透過類似FTP的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。 AEM Repo Tool類似於[Jackrabbit FileVault Maven plugin](https://jackrabbit.apache.org/filevault-package-maven-plugin)，但速度更快、相依性最小，而且是簡單的bash指令碼。

此工具可簡化檔案的傳送，讓開發人員也能與Eclipse和IntelliJ整合，以提高開發效率。

## 概覽 {#overview}

對於檔案系統上`jcr_root` FileVault結構內的給定路徑，AEM Repo Tool會為整個子樹建立一個包含單個篩選器的包，並將其推送到伺服器（類似於FTP `put`），從伺服器中提取它(`get`)或比較差異（`status`和`diff`）。

該工具不支援多個篩選路徑或FileVault的`filter.xml`。

>[!CAUTION]
>
>請注意，AEM Repo Tool一律會覆寫指定的整個檔案或目錄。

## 下載和說明檔案{#download-and-documentation}

[AEM Repo Tool可透過此連結](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)在GitHub上取得，並附上詳細的安裝與使用指示。

如果您想要下載AEM Repo Tool的來源，請參閱下方連結的GitHub專案。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟工具專案](https://github.com/Adobe-Marketing-Cloud/tools)
* 將專案下載為[a ZIP file](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
