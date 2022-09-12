---
title: AEM Repo Tool
description: AEM Repo Tool是一個簡單的解決方案，可透過與FTP相仿的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 2%

---

# AEM Repo Tool {#aem-repo-tool}

AEM Repo Tool是一個簡單的解決方案，可透過與FTP相仿的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。 AEM Repo Tool類似於 [Jackrabbit FileVault Maven外掛程式](https://jackrabbit.apache.org/filevault-package-maven-plugin)，但速度較快、相依性最低，且是簡單的bash指令碼。

此工具可簡化開發人員的檔案傳輸，也可整合至Eclipse和IntelliJ，讓開發效率更高。

## 總覽 {#overview}

對於 `jcr_root` 檔案系統上的FileVault結構， AEM Repo Tool會為整個子樹建立一個包，並將其推送到伺服器(類似於FTP `put`)，從伺服器擷取( `get`)或比較差異( `status` 和 `diff`)。

此工具不支援多個篩選路徑或FileVault的 `filter.xml`.

>[!CAUTION]
>
>請注意，AEM Repo Tool一律會覆寫指定的整個檔案或目錄。

## 下載和檔案 {#download-and-documentation}

此 [AEM Repo Tool可透過此連結在GitHub上使用](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) 以及詳細的安裝和使用指示。

如果您想要下載AEM Repo Tool的來源，請參閱下方連結的GitHub專案。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟工具專案](https://github.com/Adobe-Marketing-Cloud/tools)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
