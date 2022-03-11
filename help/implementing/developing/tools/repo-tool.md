---
title: AEM Repo Tool
description: 回購工AEM具是一種簡單的解決方案，可以通過與FTP類似的命令行在本地檔案系統AEM和伺服器之間傳輸JCR內容。
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 2%

---

# 回AEM購工具 {#aem-repo-tool}

回購工AEM具是一種簡單的解決方案，可以通過與FTP類似的命令行在本地檔案系統AEM和伺服器之間傳輸JCR內容。 回AEM購工具與 [Jackrabbit FileVault Maven插件](https://jackrabbit.apache.org/filevault-package-maven-plugin)，但速度較快，具有最小的依賴項，並且是一個簡單的bash指令碼。

此工具簡化了開發人員的檔案傳輸，還可以整合到Eclipse和IntelliJ中，使開發更加高效。

## 概覽 {#overview}

對於在 `jcr_root` 檔案系統上的FileVault結構AEM，「回購工具」為整個子樹建立一個包含單個篩選器的包，並將其推送到伺服器（類似於FTP） `put`)，從伺服器中讀取( `get`)或比較差異( `status` 和 `diff`)。

該工具不支援多個篩選器路徑或FileVault `filter.xml`。

>[!CAUTION]
>
>請注意，回AEM購工具將始終覆蓋指定的整個檔案或目錄。

## 下載和文檔 {#download-and-documentation}

的 [GitHubAEM上可通過此連結提供回購工具](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) 以及詳細的安裝和使用說明。

如果要下載回購工具的AEM源，請參閱下面連結的GitHub項目。

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟工具項目](https://github.com/Adobe-Marketing-Cloud/tools)
* 將項目下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
