---
title: AEM Repo Tool
description: AEM Repo Tool是簡單的解決方案，可透過類似FTP的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 2%

---

# AEM Repo Tool {#aem-repo-tool}

AEM Repo Tool是簡單的解決方案，可透過類似FTP的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。 AEM Repo工具類似於 [Jackrabbit FileVault Maven外掛程式](https://jackrabbit.apache.org/filevault-package-maven-plugin)，但速度更快、相依性最低，而且是簡單的bash指令碼。

此工具可為開發人員簡化檔案傳輸，也可整合至Eclipse和IntelliJ，讓開發更有效率。

## 概觀 {#overview}

針對內的指定路徑 `jcr_root` FileVault結構在檔案系統上，AEM Repo Tool會為整個子樹狀結構建立包含單一篩選器的套件，並將其推送到伺服器（類似FTP） `put`)，從伺服器擷取( `get`)或比較兩者之間的差異( `status` 和 `diff`)。

此工具不支援多個篩選路徑或FileVault的 `filter.xml`.

>[!CAUTION]
>
>AEM Repo Tool一律會覆寫指定的整個檔案或目錄。

## 下載和檔案 {#download-and-documentation}

此 [GitHub提供透過此連結使用的AEM Repo工具](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) 以及詳細的安裝和使用說明。

如果您想要下載AEM Repo工具的來源，請參閱下方連結的GitHub專案。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟工具專案](https://github.com/Adobe-Marketing-Cloud/tools)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
