---
title: 使用多個儲存庫
description: 了解如何使用Cloud Manager時管理多個Git存放庫。
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# 使用多個儲存庫 {#working-with-multiple-source-git-repos}

了解如何使用Cloud Manager時管理多個Git存放庫。

## 同步客戶管理的Git存放庫 {#syncing-customer-managed-git-repositories}

與其直接使用Cloud Manager的Git存放庫， [客戶可以使用自己的git存放庫](integrating-with-git.md) 或多個專屬的git存放庫。 在這些情況下，應設定自動同步程式，以確保Cloud Manager的Git存放庫一律保持最新。

根據客戶的Git存放庫托管位置，可使用GitHub動作或Jenkins等持續整合解決方案來設定自動化。 自動化就緒後，每次推送至客戶擁有的Git存放庫時，都能自動轉送至Cloud Manager的Git存放庫。

雖然單一客戶擁有的Git存放庫可直接執行此類自動化作業，但若要為多個存放庫進行此設定，需先進行初始設定。 來自多個Git存放庫的內容必須對應至單一Cloud Manager Git存放庫內的不同目錄。  Cloud Manager的Git存放庫需布建根Maven `pom.xml`，列出模組區段中的不同子專案。

以下是範例 `pom.xml` 檔案供兩個客戶擁有的git存放庫使用。

* 第一個項目將放入名為 `project-a`.
* 第二個項目被放入名為 `project-b`.

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

這樣的根 `pom.xml` 會推送至Cloud Manager的git存放庫中的分支。 然後，需要設定這兩個專案，以自動將變更轉送至Cloud Manager的Git存放庫。

可能的解決方案如下。

1. 推送至專案A中的分支可觸發GitHub動作。
1. 此動作會結帳專案A和Cloud Manager Git存放庫，並將專案A的所有內容複製到目錄 `project-a` 位於Cloud Manager的Git存放庫。
1. 然後動作會提交變更。

例如，專案A中主分支的變更會自動推送至Cloud Manager的Git存放庫中主分支。 當然，分支之間可能會有對應，例如推送至名為的分支 `dev` 在專案A中，會推送至名為 `development` 位於Cloud Manager的Git存放庫。 專案B需執行類似步驟。

根據分支策略和工作流程，同步可針對不同分支進行設定。 如果使用的Git存放庫未提供與GitHub動作類似的概念，也可透過Jenkins（或類似）進行整合。 在這種情況下，網路鈎子會觸發Jenkins工作來完成工作。

請依照下列步驟，新增新的、第三個來源或存放庫。

1. 將新的GitHub動作新增至新的存放庫，將變更從該存放庫推送至Cloud Manager的Git存放庫。
1. 請至少執行一次該動作，以確保專案程式碼位於Cloud Manager的Git存放庫中。
1. 在根Maven中將引用添加到新目錄 `pom.xml` 在Cloud Manager git存放庫中。

## 範例GitHub動作 {#sample-github-action}

此為推送至主分支，然後推送至Cloud Manager之Git存放庫的子目錄時，所觸發的GitHub動作範例。 GitHub動作需要提供兩個秘密， `MAIN_USER` 和 `MAIN_PASSWORD`，即可連線並推送至Cloud Manager的git存放庫。

```java
name: SYNC
env:
  # Username/email used to commit to Cloud Manager's Git repository
  USER_NAME: <NAME>
  USER_EMAIL: <EMAIL>
  # Directory within the Cloud Manager Git repository
  PROJECT_DIR: project-a
  # Cloud Manager's Git repository
  MAIN_REPOSITORY: https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
  # The branch in Cloud Manager's Git repository to push to
  MAIN_BRANCH : <BRANCH_NAME>
 
# Only run on a push to this branch
on:
  push:
     branches: [ main ]
 
jobs:
  build:
    runs-on: ubuntu-latest
 
    steps:
      # Checkout this project into a sub folder
      - uses: actions/checkout@v2
        with:
          path: sub
      # Cleanup sub project
      - name: Clean project
        run: |
          git -C sub log --format="%an : %s" -n 1 > commit.txt
          rm -rf sub/.git
          rm -rf sub/.github
      # Set global git configuration
      - name: Set git config
        run: |
          git config --global credential.helper cache
          git config --global user.email ${USER_EMAIL}
          git config --global user.name ${USER_NAME}
      # Checkout the main project
      - name: Checkout main project
        run:
          git clone -b ${MAIN_BRANCH} ${MAIN_REPOSITORY}.git main 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf main/${PROJECT_DIR} 
          mv sub main/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C main add -f ${PROJECT_DIR}
          git -C main commit -F ../commit.txt
          git -C main push
```

使用GitHub動作非常有彈性。 您可以執行Git存放庫分支之間的任何對應，以及將個別Git專案對應至主專案的目錄配置。

>[!NOTE]
>
>範例指令碼使用 `git add` 更新儲存庫。 這會假設已包含移除。 視Git的預設設定而定，這可能需要取代為 `git add --all`.

## 範例Jenkins Job {#sample-jenkins-job}

此示例指令碼可用於Jenkins作業或類似作業，並具有以下流程：

1. Git存放庫中的變更會觸發此事件。
1. Jenkins工作會檢查該項目或分支的最新狀態。
1. 然後，該作業觸發此指令碼。
1. 此指令碼接著會勾選Cloud Manager的Git存放庫，並將專案代碼提交至子目錄。

詹金斯的工作需要有兩個秘密， `MAIN_USER` 和 `MAIN_PASSWORD`，即可連線並推送至Cloud Manager的git存放庫。

```java
# Username/email used to commit to Cloud Manager's Git repository
export USER_NAME=<NAME>
export USER_EMAIL=<EMAIL>
# Directory within the Cloud Manager Git repository
export PROJECT_DIR=project-a
# Cloud Manager's Git repository
export MAIN_REPOSITORY=https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
# The branch in Cloud Manager's Git repository to push to
export MAIN_BRANCH=<BRANCH_NAME>
 
# clean up and init
rm -rf target
mkdir target
 
# mv project to sub folder
mkdir target/sub
for f in .* *
do
    if [ "$f" != "." -a "$f" != ".." -a "$f" != "target" ]
    then
        mv "$f" target/sub
    fi
done
cd target
 
# capture log and remove git info
cd sub
git log --format="%an : %s" -n 1 > ../commit.txt
rm -rf .git
rm -rf .github
cd ..
 
# checkout main repository
git clone -b $MAIN_BRANCH $MAIN_REPOSITORY main
cd main
 
# configure main repository
git config credential.helper cache
git config user.email $USER_EMAIL
git config user.name $USER_NAME
 
# update project in main
rm -rf $PROJECT_DIR
mv ../sub $PROJECT_DIR
 
# commit changes to main
git add -f $PROJECT_DIR
git commit -F ../commit.txt
git push
```

使用詹金斯的工作是非常靈活的。 您可以執行Git存放庫分支之間的任何對應，以及將個別Git專案對應至主專案的目錄配置。

>[!NOTE]
>
>範例指令碼使用 `git add` 更新儲存庫。 這會假設已包含移除。 視Git的預設設定而定，這可能需要取代為 `git add --all`.
