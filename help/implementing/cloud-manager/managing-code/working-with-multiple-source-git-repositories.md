---
title: 使用多個儲存庫
description: 瞭解如何在使用Cloud Manager時管理多個Git儲存庫。
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# 使用多個儲存庫 {#working-with-multiple-source-git-repos}

瞭解如何在使用Cloud Manager時管理多個Git儲存庫。

## 同步客戶管理的Git儲存庫 {#syncing-customer-managed-git-repositories}

與其直接使用Cloud Manager的Git儲存庫， [客戶可以使用自己的git儲存庫](integrating-with-git.md) 或多個自己的git儲存庫。 在這些情況下，應設定自動同步過程以確保Cloud Manager的Git儲存庫始終保持最新。

根據客戶的Git儲存庫的托管位置，可以使用GitHub操作或Jenkins等連續整合解決方案來設定自動化。 隨著自動化的實施，每次推送到客戶擁有的git儲存庫時，都可自動轉發到Cloud Manager的git儲存庫。

雖然單個客戶擁有的Git儲存庫的這種自動化是直接進行的，但為多個儲存庫配置此自動化需要初始設定。 需要將來自多個Git儲存庫的內容映射到單個Cloud Manager Git儲存庫中的不同目錄。  需要為Cloud Manager的Git儲存庫設定根Maven `pom.xml`，列出模組部分中的不同子項目。

以下是示例 `pom.xml` 兩個客戶擁有的git儲存庫的檔案。

* 第一個項目將放入名為 `project-a`。
* 第二個項目被放入名為 `project-b`。

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

這樣的根 `pom.xml` 已推送到Cloud Manager的git儲存庫中的分支。 然後，需要設定這兩個項目，以自動將更改轉發到Cloud Manager的Git儲存庫。

一個可能的解決辦法是：

1. GitHub操作可以通過推入項目A中的分支來觸發。
1. 該操作將簽出項目A和Cloud Manager git儲存庫，並將項目A的所有內容複製到目錄 `project-a` 在Cloud Manager的Git儲存庫中。
1. 然後，操作將提交 — 推送更改。

例如，項目A中主分支的更改將自動推送到Cloud Manager的Git儲存庫中的主分支。 當然，分支之間可能有一個映射，就像向一個名為 `dev` 將項目A中的分支推送到名為 `development` 在Cloud Manager的Git儲存庫中。 項目B需要類似的步驟。

根據分支策略和工作流，可以為不同分支配置同步。 如果使用的Git儲存庫不提供與GitHub操作類似的概念，則也可以通過Jenkins（或類似）進行整合。 在這種情況下，網鈎會觸發Jenkins的作業來完成工作。

按照以下步驟添加新的、第三個源或儲存庫。

1. 將新GitHub操作添加到新儲存庫，將更改從該儲存庫推送到Cloud Manager的Git儲存庫。
1. 至少執行一次該操作，以確保項目代碼位於Cloud Manager的Git儲存庫中。
1. 在根Maven中添加對新目錄的引用 `pom.xml` 在Cloud Manager git儲存庫中。

## 示例GitHub操作 {#sample-github-action}

這是一個GitHub操作示例，該操作通過推送到主分支，然後推入到Cloud Manager的git儲存庫的子目錄觸發。 GitHub操作需要提供兩個秘密， `MAIN_USER` 和 `MAIN_PASSWORD`，以便能夠連接並推送到Cloud Manager的git儲存庫。

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

使用GitHub操作非常靈活。 可以執行Git儲存庫分支之間的任何映射以及將單獨的Git項目映射到主項目的目錄佈局中的任何映射。

>[!NOTE]
>
>示例指令碼使用 `git add` 更新儲存庫。 這假定包括刪除。 根據Git的預設配置，可能需要用 `git add --all`。

## 示例Jenkins作業 {#sample-jenkins-job}

這是一個示例指令碼，可用於Jenkins作業或類似作業，並具有以下流：

1. 它由Git儲存庫中的更改觸發。
1. 詹金斯的工作檢查了那個項目或分支的最新狀態。
1. 然後，作業觸發此指令碼。
1. 此指令碼隨後會簽出Cloud Manager的Git儲存庫，並將項目代碼提交到子目錄。

詹金斯的工作需要有兩個秘密， `MAIN_USER` 和 `MAIN_PASSWORD`，以便能夠連接並推送到Cloud Manager的git儲存庫。

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

用詹金斯的工作很靈活。 可以執行Git儲存庫分支之間的任何映射以及將單獨的Git項目映射到主項目的目錄佈局中的任何映射。

>[!NOTE]
>
>示例指令碼使用 `git add` 更新儲存庫。 這假定包括刪除。 根據Git的預設配置，可能需要用 `git add --all`。
