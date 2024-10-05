---
title: 設定管道變數
description: 瞭解如何在Cloud Manager中使用管道變數來管理組建的特定設定變數。
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 20%

---

# 設定管道變數 {#configuring-pipeline-variables}

您的建置流程可能會依據特定的設定變數而定，這些變數不適合放入Git存放庫中，或者您可能需要在使用同一分支的管道執行之間切換這些變數。 Cloud Manager可讓您將這些資料當成管道變數來管理。

## 管道變數 {#pipeline-variables}

您可以使用Cloud Manager以數種不同的方式設定管道變數。

* [透過Cloud Manager UI](#ui)
* [使用Cloud Manager CLI](#cli)
* [使用Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

變數可能以純文字或加密待用的方式儲存。在任何一種情況下，都可在組建環境中以環境變數的形式取得，然後可以從 `pom.xml` 檔案或其他建置指令碼中加以參照。

### 管道變數命名慣例 {#naming-conventions}

變量名必須遵守以下約定。

* 變數名稱只能包含字母數字構成的字元和底線 (`_`)。
* 按照慣例，上述名稱應全部大寫。
* 每個管道限制為 200 個變數。
* 每個名稱不得超過100個字元。
* 每個`string`變數值都必須少於 2048 個字元。
* 每個`secretString`型別變數值都必須少於或等於500個字元。

## 透過Cloud Manager UI {#ui}

管道變數可透過Cloud Manager UI設定和管理。 您必須有許可權編輯管道，才能新增、編輯和刪除管道變數。

如果管道正在執行，則會封鎖變數管理。

### 新增管道變數 {#add-ui}

1. 當[管理您的管道時，](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)點選或按一下您要建立管道變數的管道的省略符號按鈕，並從內容選單中選取&#x200B;**檢視/編輯變數**。

   ![檢視/編輯管道變數](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. **變陣列態**&#x200B;視窗隨即開啟。 在表格的第一列輸入變數詳細資料，然後點選或按一下&#x200B;**新增**。

   * **設定名稱**&#x200B;是變數的唯一識別碼，它必須標頭[管線變數命名慣例](#naming-conventions)。
   * **值**&#x200B;是變數儲存的值。
   * **套用的步驟**&#x200B;是管道中套用變數的步驟。 此為必要欄位。
      * **組建**
      * **功能測試**
      * **UI測試**
   * **Type**&#x200B;定義變數是純文字或加密為機密。

   ![新增變數](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. 隨即會新增至表格。 視需要新增其他變數，然後點選或按一下「儲存」****&#x200B;以儲存您新增至管道的變數。

### 編輯管道變數 {#edit-ui}

1. 當[管理您的管道時，](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)點選或按一下您要建立管道變數的管道的省略符號按鈕，並從內容選單中選取&#x200B;**檢視/編輯變數**。

   ![檢視/編輯管道變數](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. **變陣列態**&#x200B;視窗隨即開啟。 點選或按一下您要編輯之變數的省略符號按鈕，然後選取&#x200B;**編輯**。

   ![編輯變數](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. 視需要更新變數的值，然後點選或按一下「套用」**** （列末端的核取記號）以套用變更，或點選「捨棄」**** （返回箭頭）以還原變更。

   * 只能編輯變數的值。

   ![編輯變數](/help/implementing/cloud-manager/assets/pipeline-variables-edit-save.png)

1. 點選或按一下「**儲存**」，將您對變數所做的變更儲存至管道。

如果您想要刪除變數，請在&#x200B;**變數設定**&#x200B;視窗的管道變數省略符號選單中選取&#x200B;**刪除**，而非&#x200B;**編輯**。

## 使用Cloud Manager CLI {#cli}

此 CLI 命令設定一個變量。

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

此 CLI 命令設定一個變量。

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

在 Maven `pom.xml` 檔案中使用時，使用類似下列的語法將這些變數對應到 Maven 屬性通常會有幫助。

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```
