---
title: Cloud Manager中的管道變數
description: 瞭解如何在Cloud Manager中使用管道變數來管理組建的特定設定變數。
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fb180685152a00d520530d21a44337381febba7f
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 14%

---

# Cloud Manager中的管道變數 {#configuring-pipeline-variables}

您的建置流程可能會依賴不應儲存在Git存放庫中的特定設定變數。 或者，您可能需要在同一分支上的管道執行之間調整它們。 Cloud Manager可讓您以管道變數的形式管理這些設定。

## 關於管道變數 {#pipeline-variables}

您可以使用Cloud Manager以數種不同的方式設定管道變數。

* [使用Cloud Manager使用者介面](#ui)
* [使用Cloud Manager CLI](#cli)
* [使用Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

變數可能以純文字或加密待用的方式儲存。在任何一種情況下，都能在建置環境中以環境變數的形式使用變數，然後可以從 `pom.xml` 檔案或其他建置指令碼中進行參照。

## 透過Cloud Manager新增管道變數 {#ui}

管道變數可透過Cloud Manager使用者介面進行設定和管理。 它們有助於簡化管道管理，尤其是在跨不同步驟需要不同配置時。

您必須有權編輯管道以新增、編輯和刪除管道變數。

如果管道正在執行，則會封鎖變數管理。

**若要透過Cloud Manager新增管道變數：**

1. 當[管理您的管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)時，按一下您要為其建立管道變數的管道的![省略符號 — 更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 從下拉式功能表，按一下&#x200B;**檢視/編輯變數**。

   ![檢視/編輯管道變數](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. 在&#x200B;**變陣列態**&#x200B;對話方塊中，在表格的第一列輸入詳細資料。

   | 欄位 | 說明 |
   | --- | --- |
   | 名稱 | 設定變數的唯一名稱。 它可識別管道中使用的特定變數。 它必須遵循以下命名慣例：<ul><li>變數只能包含英數字元和底線(`_`)。</li><li>按照慣例，上述名稱應全部大寫。</li><li>每個管道限制為 200 個變數。</li><li>每個名稱不得超過100個字元。</li><li>每個`string`變數值都必須少於 2048 個字元。</li><li>每個`secretString`型別變數值都必須少於或等於500個字元。</li></ul> |
   | 值 | 變數儲存的值。 |
   | 套用的步驟 | 必要。要套用變數的管道中的步驟：<ul><li>**建置** — 在建置程式期間套用變數。</li><li>**功能測試** — 變數用於功能測試步驟。</li><li>**UI測試** — 變數用於UI測試階段。</li><li>**部署** — 在部署步驟期間使用變數。 例如，將此變數用於Edge Delivery Services管道。</li></ul> |
   | 類型 | 如果變數是純文字或加密為秘密，請選取。 |

   ![新增變數](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. 按一下&#x200B;**新增**。

   視需要新增其他變數。

1. 按一下&#x200B;**儲存**。

## 編輯管道變數 {#edit-ui}

1. 當[管理您的管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)時，按一下您要編輯其管道變數的管道的![省略符號 — 更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在下拉式功能表中，按一下&#x200B;**檢視/編輯變數**。

   ![檢視/編輯管道變數](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. 在&#x200B;**變陣列態**&#x200B;對話方塊中，按一下您要變更之變數的![省略符號 — 其他圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在下拉式功能表中，按一下&#x200B;**編輯**。

   ![編輯變數](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. 視需要更新變數的值。

   只能變更變數的值。

1. 執行下列任一項作業：

   * 按一下![套用 — 勾選圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)以套用變更。
   * 按一下![復原圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Undo_18_N.svg)以還原變更。

1. 按一下&#x200B;**儲存**。


## 刪除管道變數 {#delete-ui}

1. 當[管理您的管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)時，按一下要刪除管道變數之管道的![省略符號 — 更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在下拉式功能表中，按一下&#x200B;**檢視/編輯變數**。

   ![檢視/編輯管道變數](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. 在&#x200B;**變陣列態**&#x200B;對話方塊中，按一下您要移除之變數的![省略符號 — 其他圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然後按一下&#x200B;**刪除**。

## 使用Cloud Manager CLI設定管道變數 {#cli}

CLI （指令行介面）中的這個指令會設定變數。

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

此 CLI 命令設定一個變量。

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

在Maven `pom.xml`檔案中使用時，使用類似下列範例的語法將這些變數連結至Maven屬性通常會有幫助：

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
