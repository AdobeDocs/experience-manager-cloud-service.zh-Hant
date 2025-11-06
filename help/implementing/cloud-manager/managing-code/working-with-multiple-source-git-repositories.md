---
title: 使用多個存放庫
description: 瞭解在使用Cloud Manager時如何管理多個Git存放庫。
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 35%

---

# 使用多個存放庫 {#working-with-multiple-source-git-repos}

瞭解在使用Cloud Manager時如何管理多個Git存放庫。

## 同步私人Git存放庫 {#syncing-customer-managed-git-repositories}

[客戶可以使用自己的私人Git存放庫](integrating-with-git.md)或多個自己的Git存放庫，而不是直接使用Cloud Manager的Git存放庫。 在這些情況下，請設定自動同步程式，以確保Cloud Manager中的Git存放庫隨時保持最新。

根據託管客戶Git存放庫的位置，可以使用GitHub操作或Jenkins等持續整合解決方案來設定自動化。 建立自動化後，可將每次到客戶自己的Git存放庫的推送自動轉寄到Cloud Manager的Git存放庫。

雖然對單一客戶擁有的Git存放庫而言，這類自動化很簡單，但若為多個存放庫設定，則需要初始設定。 來自多個Git存放庫的內容必須對應至單一Cloud Manager Git存放庫中不同的目錄。 Cloud Manager的Git存放庫必須以根Maven `pom.xml`布建，並在模組區段中提供不同子專案的清單。

以下是兩個客戶自有Git存放庫的範例`pom.xml`檔案。

* 第一個專案會放入名為 `project-a` 的目錄中。
* 第二個專案會放入名為 `project-b` 的目錄中。

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

這類根 `pom.xml` 會被推送到 Cloud Manager Git 存放庫中的某個分支。然後，必須設定這兩個專案以自動將變更轉寄到Cloud Manager的Git存放庫。

以下是可能的解決方案。

1. 推送至專案A中的分支以觸發GitHub動作。
1. 該操作會簽出專案 A 和 Cloud Manager Git 存放庫，然後將專案A的所有內容複製到Cloud Manager的Git存放庫中的`project-a`目錄。
1. 然後，該操作會認可-推送變更。

例如，會將專案A中主要分支上的變更自動推送到Cloud Manager的Git存放庫中的主要分支。 分支之間可能存在對應，例如，會將對專案A中名為`dev`分支的推送推到Cloud Manager的Git存放庫中名為`development`的分支。 專案 B 需要類似的步驟。

根據分支原則和工作流程，可以為不同的分支設定同步。如果所使用的 Git 存放庫未提供類似 GitHub 操作的概念，則也有可能經由 Jenkins (或類似方法) 進行整合。在這種情況下，webhook會觸發進行這項工作的Jenkins作業。

依照下列步驟進行，即可新增第三個來源或存放庫。

1. 新增GitHub動作至新存放庫，這會將變更從該存放庫推送至Cloud Manager的Git存放庫。
1. 至少執行一次該動作，確認方案程式碼存在於 Cloud Manager 的 Git 存放庫中。
1. 在Cloud Manager Git存放庫中，在根Maven `pom.xml`中新增新目錄的參考。



## GitHub 操作範例 {#sample-github-action}

以下是由推送至主要分支所觸發的範例GitHub動作。 接著推送至Cloud Manager Git存放庫的子目錄。 GitHub動作必須提供兩個秘密`MAIN_USER`和`MAIN_PASSWORD`，才能連線並推送至Cloud Manager的Git存放庫。

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
          git clone -b ${MAIN_BRANCH} ${MAIN_REPOSITORY} ${MAIN_BRANCH} 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf ${MAIN_BRANCH}/${PROJECT_DIR} 
          mv sub ${MAIN_BRANCH}/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C ${MAIN_BRANCH} add -f ${PROJECT_DIR}
          git -C ${MAIN_BRANCH} commit -F ../commit.txt
          git -C ${MAIN_BRANCH} push
```

使用 GitHub 操作非常靈活。能夠執行 Git 存放庫分支間的任何對應，以及單獨 Git 專案至主要專案目錄版面的任何對應。

>[!NOTE]
>
>範例指令碼使用 `git add` 來更新存放庫。指令碼會假設包含移除。 根據Git的預設設定，必須以`git add --all`取代。

## Jenkins 作業範例 {#sample-jenkins-job}

以下是指令碼範例，可用於Jenkins作業或類似操作，流程如下：

1. 會由Git存放庫中的變更觸發。
1. Jenkins 作業會檢查該專案或分支的最新狀態。
1. 該作業會觸發此指令碼。
1. 此指令碼會陸續簽出 Cloud Manager 的 Git 存放庫並將專案程式碼提交到子目錄。

Jenkins作業必須提供兩個秘密`MAIN_USER`和`MAIN_PASSWORD`，才能連線並推送至Cloud Manager的Git存放庫。

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

使用 Jenkins 作業非常靈活。能夠執行 Git 存放庫分支間的任何對應，以及單獨 Git 專案至主要專案目錄版面的任何對應。

>[!NOTE]
>
>範例指令碼使用 `git add` 來更新存放庫。指令碼會假設包含移除。 根據Git的預設設定，必須以`git add --all`取代。
