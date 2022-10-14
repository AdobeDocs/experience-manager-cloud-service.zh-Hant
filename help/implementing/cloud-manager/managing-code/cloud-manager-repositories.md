---
title: Cloud Manager 存放庫
description: 了解如何在 Cloud Manager 中建立、檢視和刪除 Git 存放庫。
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 100%

---


# Cloud Manager 存放庫 {#cloud-manager-repos}

了解如何在 Cloud Manager 中建立、檢視和刪除 Git 存放庫。

>[!NOTE]
>
>任何指定公司或 IMS 組織中的所有計畫都存在 300 個存放庫的限制。

## 新增和管理存放庫 {#add-manage-repos}

依照下列步驟在 Cloud Manager 中檢視和管理存放庫。

1. 從&#x200B;**計畫總覽**&#x200B;頁面，按一下&#x200B;**存放庫**&#x200B;索引標籤，並瀏覽至&#x200B;**存放庫**&#x200B;頁面。

1. 按一下&#x200B;**新增存放庫**&#x200B;以開啟精靈。

   ![新增存放庫按鈕](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. 依照要求輸入名稱和說明，然後按一下&#x200B;**儲存**。

   ![新增存放庫對話框](/help/implementing/cloud-manager/assets/repos/repo-1.png)

當精靈關閉時，您的新存放庫將顯示在表格中。

您可以在資料表中選取存放庫，然後按一下省略符號按鈕，然後選取&#x200B;**複製存放庫 URL**、**檢視和更新**&#x200B;或&#x200B;**刪除**&#x200B;您的存放庫。

![存放庫選項](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

在新增或編輯管道時，您也可以選擇在 Cloud Manager 中建立的存放庫。如需了解詳細資訊，請參閱文件：[CI-CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

任何指定管道都有一個主要存放庫或一個分支。透過[Git 子模組支援](#git-submodule-support)，可以在建置階段包含許多次要分支。

>[!NOTE]
>
>使用者必須具備&#x200B;**部署管理員**&#x200B;或&#x200B;**企業所有者**&#x200B;角色才能新增存放庫。

## 刪除存放庫 {#delete-repo}

刪除存放庫將：

* 使已刪除的存放庫名稱無法用於將來可能建立的新存放庫。
   * 在這種情況下將顯示錯誤訊息 `Repository name should be unique within organization.`。
* 讓已刪除的存放庫在 Cloud Manager 中無法使用，並且無法連結到管道。

按照這些步驟即可刪除 Cloud Manager 中的存放庫。

1. 從&#x200B;**計畫總覽**&#x200B;頁面，按一下&#x200B;**存放庫**&#x200B;索引標籤，並瀏覽至&#x200B;**存放庫**&#x200B;頁面。

1. 選擇存放庫，按一下省略符號按鈕，然後選擇&#x200B;**刪除**&#x200B;以刪除存放庫。

   ![刪除存放庫](/help/implementing/cloud-manager/assets/repos/delete-repo.png)

## Git 子模組支援 {#git-submodule-support}

Git 子模組可用於在建置時間時跨越 Git 存放庫合併多個分支的內容。

當 Cloud Manager 的建置流程執行時，複製為管道設定的存放庫並簽出已設定的分支後，如果該分支包含根目錄中的 `.gitmodules` 檔案，則執行命令。

以下命令會將每個子模組簽出至適當的目錄中。

```
$ git submodule update --init
```

對於習慣使用 Git 子模組並且不想管理外部合併流程的組織來說，此技術是文件[使用多來源 Git 存放庫](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md)中所述解決方案的潛在替代計畫。

例如，我們假設有三個存放庫，每個都包含名為 `main` 的單一分支。在主要存放庫中 (即在管道中設定的那個)，`main` 分支有一個 `pom.xml` 檔案，宣告包含在其他兩個存放庫中的專案。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
   
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
   
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
   
</project>
```

然後，您將為其他兩個存放庫新增子模組。

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

這會產生一個類似於以下內容的 `.gitmodules` 檔案。

```text
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

有關 Git 子模組的更多資訊可以在 [Git 參考手冊](https://git-scm.com/book/en/v2/Git-Tools-Submodules)中找到。

### 限制和建議 {#limitations-recommendations}

使用 Git 子模組時，請留意以下限制：

* Git URL 必須完全符合上節所述語法。
* 僅支援分支根部的子模組。
* 由於安全理由，請勿在 Git URL 中嵌入憑證。
* 除非另有必要，否則強烈建議使用淺子模組。
   * 為此，需對每個子模組執行 `git config -f .gitmodules submodule.<submodule path>.shallow true`。
* 會將 Git 子模組參考資料儲存到特定的 Git 認可。因此，若對子模組存放庫進行變更，需要更新參考的認可。
   * 例如，使用 `git submodule update --remote`
