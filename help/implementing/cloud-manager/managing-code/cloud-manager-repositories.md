---
title: Cloud Manager資料庫
description: 瞭解如何在雲管理器中建立、查看和刪除您的Git儲存庫。
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---


# Cloud Manager資料庫 {#cloud-manager-repos}

瞭解如何在雲管理器中建立、查看和刪除您的Git儲存庫。

>[!NOTE]
>
>在任何給定的公司或IMS組織中，所有程式都有300個儲存庫。

## 添加和管理儲存庫 {#add-manage-repos}

按照這些步驟查看和管理Cloud Manager中的儲存庫。

1. 從 **計畫概述** ，按一下 **儲存庫** 頁籤並導航至 **儲存庫** 的子菜單。

1. 按一下 **添加儲存庫** 的子菜單。

   ![「添加儲存庫」按鈕](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. 按請求輸入名稱和說明，然後按一下 **保存**。

   ![「添加儲存庫」對話框](/help/implementing/cloud-manager/assets/repos/repo-1.png)

嚮導關閉後，新儲存庫將顯示在表中。

可以選擇表中的儲存庫，然後按一下省略號按鈕並選擇 **複製儲存庫URL**。 **查看和更新**&#x200B;或 **刪除**。

![儲存庫選項](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

在Cloud Manager中建立的儲存庫也可用於添加或編輯管道時進行選擇。 請參閱文檔 [CI-CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 來瞭解更多資訊。

任何給定管道都有一個主儲存庫或分支。 與 [git子模組支援](#git-submodule-support)，在構建時可以包含許多次分支。

>[!NOTE]
>
>用戶必須具有角色 **部署管理器** 或 **業務所有者** 才能添加儲存庫。

## 刪除儲存庫 {#delete-repo}

刪除儲存庫將：

* 使刪除的儲存庫名稱不可用於將來可能建立的新儲存庫。
   * 錯誤消息 `Repository name should be unique within organization.` 會在這些情況下顯示。
* 使刪除的儲存庫在雲管理器中不可用，並且不可用於連結到管道。

按照這些操作刪除雲管理器中的儲存庫。

1. 從 **計畫概述** ，按一下 **儲存庫** 頁籤並導航至 **儲存庫** 的子菜單。

1. 選擇儲存庫，然後按一下省略號按鈕並選擇 **刪除** 刪除儲存庫。

   ![刪除儲存庫](/help/implementing/cloud-manager/assets/repos/delete-repo.png)

## Git子模組支援 {#git-submodule-support}

Git子模組可用於在生成時合併多個分支在Git儲存庫中的內容。

當Cloud Manager的生成進程執行時，在克隆了為管道配置的儲存庫並簽出了已配置的分支後，如果分支包含 `.gitmodules` 檔案，執行命令。

以下命令會將每個子模組檢出到相應的目錄中。

```
$ git submodule update --init
```

此技術是文檔中所述解決方案的潛在替代方法 [使用多個源Git儲存庫](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md) 對於那些願意使用git子模組且不想管理外部合併進程的組織。

例如，假設有三個儲存庫，每個儲存庫都包含一個名為 `main`。 在主儲存庫中，即在管道中配置的儲存庫 `main` 分支具有 `pom.xml` 檔案聲明其他兩個儲存庫中包含的項目。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
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

然後，您將為另外兩個儲存庫添加子模組。

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

這將導致 `.gitmodules` 檔案。

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

有關git子模組的詳細資訊，請參閱 [Git參考手冊。](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

### 限制和Recommendations {#limitations-recommendations}

使用git子模組時，請注意以下限制。

* Git URL必須與上一節中描述的語法完全一致。
* 只支援分支根上的子模組。
* 出於安全原因，請勿在Git URL中嵌入憑據。
* 除非有其他必要，強烈建議使用淺子模組。
   * 要執行此操作，請運行 `git config -f .gitmodules submodule.<submodule path>.shallow true` 每個子模組。
* Git子模組引用儲存到特定的Git提交。 因此，當對子模組儲存庫進行更改時，需要更新引用的提交。
   * 例如，使用 `git submodule update --remote`
