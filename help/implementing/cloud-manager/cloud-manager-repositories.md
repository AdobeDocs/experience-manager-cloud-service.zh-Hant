---
title: Cloud Manager儲存庫
description: Cloud Manager儲存庫
exl-id: Cloud Manager Repositories
source-git-commit: 1f2109731b8efd1c05941b7a7db23e6497257cbf
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Cloud Manager儲存庫 {#cloud-manager-repos}

在Cloud Manager中建立和可用的儲存庫可透過「儲存庫」頁面來檢視和管理。

>[!NOTE]
>任何給定公司或[Adobe的Identity Management System](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/ims.html)中的所有程式都有300個儲存庫的限制。

## 添加和管理儲存庫 {#add-manage-repos}

請依照下列步驟，在Cloud Manager中檢視及管理存放庫：

1. 從&#x200B;**程式概述**&#x200B;頁，按一下&#x200B;**儲存庫**&#x200B;頁簽並導航到&#x200B;**儲存庫**&#x200B;頁。

1. 按一下&#x200B;**添加儲存庫**&#x200B;以啟動嚮導。

   >[!NOTE]
   >必須登錄部署管理員或業務所有者角色中的用戶才能添加儲存庫。

   ![](assets/repos/create-repo2.png)


1. 按要求輸入名稱和說明，然後按一下&#x200B;**Save**。

   ![](assets/repos/repo-1.png)

1. 選擇&#x200B;**保存**。 新建立的存放庫會顯示在表格中，如下所示。 在Cloud Manager中建立的儲存庫也可供您在新增或編輯管道步驟期間選取。 請參閱[設定CI-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en)以深入了解。

   >[!NOTE]
   >任何指定管道都有單個&#x200B;*primary*&#x200B;存放庫或分支。 透過[Git子模組支援](#git-submodule-support)，不過建置時可包含許多次要分支。

   ![](assets/repos/create-repo3.png)

1. 您可以選擇儲存庫，然後按一下表格最右側的菜單選項，以&#x200B;**複製儲存庫URL**、**查看和更新**&#x200B;或&#x200B;**刪除**&#x200B;儲存庫，如下圖所示。

   ![](assets/repos/create-repo3.png)


## Git子模組支援 {#git-submodule-support}

Git子模組可用來在建置時合併Git存放庫間多個分支的內容。 執行Cloud Manager的建置程式時，在為管道配置的存放庫複製並簽出已配置的分支後，如果根目錄中的分支包含`.gitmodules`檔案，則會執行命令。

```
$ git submodule update --init
```

這會將每個子模組簽入相應目錄。 對於熟悉使用Git子模組且不想管理外部合併程式的組織，此技術是https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/working-with-multiple-source-git-repositories.html的替代方法。

例如，假設有三個存放庫，每個存放庫都包含名為main的單一分支。 在「主要」存放庫（即管道中設定的存放庫）中，主分支有一個pom.xml檔案，聲明其他兩個存放庫中包含的專案：

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

然後，您將為其他兩個存放庫新增子模組：

```
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

這會產生如下所示的`.gitmodules`檔案：

```
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

有關Git子模組的詳細資訊，請參閱[Git參考手冊](https://git-scm.com/book/en/v2/Git-Tools-Submodules)。

使用Git子模組時，請記住以下事項：

* Git URL必須完全使用上述語法。 基於安全考量，請勿在這些URL中內嵌憑證。
* 僅支援分支根的子模組。
* Git子模組參考會儲存至特定的Git提交。 因此，在對子模組存放庫進行變更時，需要更新所參考的提交，例如使用`git submodule update --remote` 。

