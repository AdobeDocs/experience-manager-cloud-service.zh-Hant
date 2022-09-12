---
title: Cloud Manager儲存庫
description: 了解如何在Cloud Manager中建立、檢視和刪除您的Git存放庫。
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---


# Cloud Manager儲存庫 {#cloud-manager-repos}

了解如何在Cloud Manager中建立、檢視和刪除您的Git存放庫。

>[!NOTE]
>
>任何公司或IMS組織中所有計畫的存放庫都有300個的限制。

## 添加和管理儲存庫 {#add-manage-repos}

請依照下列步驟，在Cloud Manager中檢視及管理存放庫。

1. 從 **計畫概述** 頁面，按一下 **儲存庫** 標籤，並導覽至 **儲存庫** 頁面。

1. 按一下 **添加儲存庫** 啟動嚮導。

   ![添加儲存庫按鈕](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. 按一下「Name（請求）」和「Description（說明）」 **儲存**.

   ![添加儲存庫對話框](/help/implementing/cloud-manager/assets/repos/repo-1.png)

當嚮導關閉時，新儲存庫將顯示在表中。

您可以選取表格中的存放庫，然後按一下省略號按鈕並選取 **複製儲存庫URL**, **檢視與更新**，或 **刪除**.

![儲存庫選項](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

在Cloud Manager中建立的儲存庫也可供您在新增或編輯管道時選取。 請參閱該文檔 [CI-CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 了解更多。

任何指定管道都有單一主要存放庫或分支。 使用 [git子模組支援](#git-submodule-support)，建置時可包含許多次要分支。

>[!NOTE]
>
>使用者必須具有角色 **部署管理員** 或 **業務負責人** 來新增存放庫。

## 刪除儲存庫 {#delete-repo}

刪除儲存庫將：

* 使已刪除的儲存庫名稱無法用於將來可能建立的新儲存庫。
   * 錯誤訊息 `Repository name should be unique within organization.` 會在這種情況下顯示。
* 讓已刪除的存放庫在Cloud Manager中無法使用，且無法連結至管道。

請依照這些操作刪除Cloud Manager中的存放庫。

1. 從 **計畫概述** 頁面，按一下 **儲存庫** 標籤，並導覽至 **儲存庫** 頁面。

1. 選取存放庫，然後按一下省略號按鈕並選取 **刪除** 刪除儲存庫。

   ![刪除儲存庫](/help/implementing/cloud-manager/assets/repos/delete-repo.png)

## Git子模組支援 {#git-submodule-support}

Git子模組可用來在建置時合併Git存放庫間多個分支的內容。

當Cloud Manager的建置程式執行時，為管道設定的存放庫複製並簽出已設定的分支後(如果分支包含 `.gitmodules` 檔案，則執行命令。

以下命令將每個子模組檢出到相應目錄中。

```
$ git submodule update --init
```

此技術是本檔案中所述解決方案的潛在替代方案 [使用多個來源Git存放庫](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md) 對於熟悉使用git子模組且不想管理外部合併程式的組織。

例如，假設有三個存放庫，每個存放庫都包含名為的單一分支 `main`. 在主要存放庫中（亦即在管道中設定的存放庫），即 `main` 分支具有 `pom.xml` 檔案，聲明其他兩個儲存庫中包含的項目。

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

然後，您會為其他兩個存放庫新增子模組。

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

這會導致 `.gitmodules` 檔案。

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

如需Git子模組的詳細資訊，請參閱 [Git參考手冊。](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

### 限制和Recommendations {#limitations-recommendations}

使用Git子模組時，請注意下列限制。

* Git URL必須完全採用前一節所述的語法。
* 僅支援分支根的子模組。
* 基於安全考量，請勿在Git URL中內嵌憑證。
* 除非另有必要，強烈建議使用淺層子模組。
   * 要執行此操作，請運行 `git config -f .gitmodules submodule.<submodule path>.shallow true` 每個子模組。
* Git子模組參考會儲存至特定的Git提交項目。 因此，在對子模組存放庫進行變更時，需要更新參考的提交。
   * 例如，透過使用 `git submodule update --remote`
