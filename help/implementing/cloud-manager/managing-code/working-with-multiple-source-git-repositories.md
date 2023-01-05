---
title: 使用多個存放庫
description: 了解如何在使用 Cloud Manager 時管理多個 Git 存放庫。
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: 5ea5c3f03642ae2f7471165d4d0ee33c2cc31b6b
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 100%

---

# 使用多個存放庫 {#working-with-multiple-source-git-repos}

了解如何在使用 Cloud Manager 時管理多個 Git 存放庫。

## 同步客戶管理的 Git 存放庫 {#syncing-customer-managed-git-repositories}

[客戶可以使用自己的 Git 存放庫](integrating-with-git.md)或多個自己的 Git 存放庫，而不是直接使用 Cloud Manager 的 Git 存放庫。在這種情況下應設定自動同步流程，以確保 Cloud Manager 的 Git 存放庫隨時保持最新。

根據託管客戶 Git 存放庫的位置，可以使用 GitHub 操作或 Jenkins 等持續整合解決方案來設定自動化。建立自動化後，可將每次到客戶自己的存放庫的推送自動轉寄到 Cloud Manager 的 Git 存放庫。

雖然對單一客戶擁有的 Git 存放庫而言，這類自動化很簡單，但若為多個存放庫設定，則需要初始設定。需要將來自多個 Git 存放庫的內容對應到單一 Cloud Manager 的 Git 存放庫中不同的目錄。需要在 Cloud Manager 的 Git 存放庫佈建根 Maven `pom.xml`，在模組區段中提供不同子專案的清單。

以下是兩個客戶自有 Git 存放庫的範例 `pom.xml` 檔案。

* 第一個專案將放入名為 `project-a` 的目錄中。
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

這類根 `pom.xml` 會被推送到 Cloud Manager 的 Git 存放庫中的某個分支。然後需要設定這兩個專案以自動將變更轉寄到 Cloud Manager 的 Git 存放庫。

以下是可能的解決方案。

1. 可以透過推送到專案 A 中的分支來觸發 GitHub 動作。
1. 該動作將檢查專案 A 和 Cloud Manager Git 存放庫，並將專案 A 中的所有內容複製到 Cloud Manager 的 Git 存放庫中的目錄 `project-a`。
1. 然後該操作將認可-推送變更。

例如，會將專案 A 中主要分支上的變更自動推送到 Cloud Manager 的 Git 存放庫中的主要分支。當然，分支之間可能會進行對應，例如，會將對專案 A 中名為 `dev` 分支的推送推到 Cloud Manager 的 Git 存放庫中名為 `development` 的分支。專案 B 需要類似的步驟。

根據分支原則和工作流程，可以為不同的分支設定同步。如果使用的 Git 存放庫不提供類似 GitHub 操作的概念，則也有可能透過 Jenkins (或類似方法) 進行整合。在這種情況下，webhook 會觸發進行這項工作的 Jenkins 作業。

請依照下列步驟，新增第三個來源或存放庫。

1. 將新的 GitHub 操作新增到新存放庫，會因此從該存放庫將變更推送到 Cloud Manager 的 Git 存放庫。
1. 至少執行一次該操作，以確保專案計劃碼在 Cloud Manager 的 Git 存放庫中。
1. 在 Cloud Manager Git 存放庫的根 Maven `pom.xml` 中新增對新目錄的參考資料。

## GitHub 操作範例 {#sample-github-action}

這是一個 GitHub 操作的範例，透過推送至主要分支然後推入 Cloud Manager 的 Git 存放庫的子目錄中來觸發。需要對該 GitHub 操作提供兩個秘密：`MAIN_USER` 以及 `MAIN_PASSWORD`，才能連線並推送至 Cloud Manager 的 Git 存放庫。

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

使用 GitHub 操作非常靈活。Git 存放庫的分支之間可執行的任何對應，以及單獨的 Git 專案到主要專案的目錄版面中的任何對應。

>[!NOTE]
>
>範例指令碼使用 `git add` 來更新存放庫。這假設包括刪除。根據 Git 的預設設定，這可能需要取代為 `git add --all`。

## Jenkins 作業範例 {#sample-jenkins-job}

這是指令碼範例，可用於 Jenkins 作業或類似操作，流程如下所示：

1. 會由 Git 存放庫中的變更觸發。
1. Jenkins 作業會檢查該專案或分支的最新狀態。
1. 該作業會觸發此指令碼。
1. 該指令碼會依次檢查 Cloud Manager 的 Git 存放庫並將專案計劃碼認可到子目錄。

需要對該 Jenkins 作業提供兩個秘密：`MAIN_USER` 以及 `MAIN_PASSWORD`，才能連線並推送至 Cloud Manager 的 Git 存放庫。

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

使用 Jenkins 作業非常靈活。Git 存放庫的分支之間可執行的任何對應，以及單獨的 Git 專案到主要專案的目錄版面中的任何對應。

>[!NOTE]
>
>範例指令碼使用 `git add` 來更新存放庫。這假設包括刪除。根據 Git 的預設設定，這可能需要取代為 `git add --all`。
