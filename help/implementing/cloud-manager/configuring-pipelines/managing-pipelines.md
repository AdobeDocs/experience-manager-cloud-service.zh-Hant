---
title: 管理管道
description: 了解如何管理現有管道，包括將其編輯、執行和刪除。
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 47%

---


# 管理管道 {#managing-pipelines}

了解如何管理現有管道，包括將其編輯、執行和刪除。

## 管道卡 {#pipeline-card}

此&#x200B;**管道**&#x200B;卡位於 Cloud Manager 中的&#x200B;**方案總覽**&#x200B;頁面上，可讓您總覽您所有的管道及其目前狀態。

![Cloud Manager 中的管道卡](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

按一下每個管道旁邊的省略符號按鈕，您就可以執行下列操作。

* [執行管道](#running-pipelines)
* [編輯管道](#editing-pipelines)
* [刪除管道](#deleting-pipelines)
* [檢視詳細資訊](#view-details)

在管道清單底部有一般選項。

* **新增** - 至[可新增生產管道](configuring-production-pipelines.md)或是[新增非生產管道](configuring-non-production-pipelines.md)
* **全部顯示** - 將使用者帶到管道畫面，在更詳細的表格中檢視所有管道。
* **存取存放庫資訊** - 顯示要存取 Cloud Manager Git 存放庫所必需的資訊
* **了解更多** - 瀏覽至 CI/CD 管道文件資源。

## 管線視窗 {#pipelines}

此 **管道** 視窗顯示所選計畫的所有管道的完整清單。 這很有用，因為它提供的資訊比 [管道卡。](#pipeline-card)

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 從 **計畫總覽** 頁面，點選或按一下 **管道** 標籤以切換至 **管道** 視窗。

1. 在這裡，您可以看到計畫的所有管道清單，並像在中一樣開始和停止管道執行 **管道卡**.

如果管道正在執行，將游標暫留在其 **狀態** 欄會顯示執行的詳細資訊。

![管道執行詳細資料](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

點選或按一下 **檢視詳細資料** 將帶您前往 [管道執行的詳細資訊。](#view-details)

## 活動視窗 {#activity}

此 **活動** 視窗顯示所選方案的所有管道執行的完整清單。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 從 **計畫總覽** 頁面，點選或按一下 **活動** 標籤以切換至 **活動** 視窗。

1. 您可以在此處檢視計畫的所有管道執行清單，包括當前和歷史執行。

如果管道正在執行，將游標暫留在其 **狀態** 欄會顯示執行的詳細資訊。

![管道執行詳細資料](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

點選或按一下 **檢視詳細資料** 將帶您前往 [管道執行的詳細資訊。](#view-details)

## 執行管道 {#running-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 導覽至 **管道** 卡來自 **計畫總覽** 頁面，並按一下您執行的管道旁的省略符號按鈕選擇 **執行** 功能表中。

1. 此管道執行開始，並由&#x200B;**狀態**&#x200B;欄顯示。

您可以查看執行的詳細資訊，只要再按一下省略符號按鈕，並選取&#x200B;**[檢視詳細資訊。](#view-details)**

依管道的類型而定，您也許可以取消執行，只要再按一下省略符號按鈕，並選取&#x200B;**取消**。

## 編輯管道 {#editing-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 導覽至 **管道** 卡來自 **計畫總覽** 頁面，按一下要編輯的管道旁的省略符號按鈕，然後選取 **編輯** 功能表中。

1. **編輯生產管道**&#x200B;或是&#x200B;**編輯非生產管道**&#x200B;對話框會隨即顯示，讓您可以對您在建立管道時輸入的詳細資訊進行編輯。

   * 如需有關管道可用的所有欄位和設定選項的詳細資訊，請參閱以下頁面。
      * [設定生產管道](configuring-production-pipelines.md)
      * [設定非生產管道](configuring-non-production-pipelines.md)

1. 按一下 **更新** 一旦您完成編輯管道。

>[!NOTE]
>
>您無法編輯執行中的管道。

## 刪除管道 {#deleting-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 導覽至 **管道** 卡來自 **計畫總覽** 頁面，並按一下您執行的管道旁的省略符號按鈕選擇 **刪除** 功能表中。

>[!NOTE]
>
>您無法刪除執行中的管道。

## 檢視管道詳細資訊 {#view-details}

您可以檢視管道的詳細資訊，以檢視其上次執行的狀態和記錄。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 導覽至 **管道** 卡來自 **計畫總覽** 頁面，並按一下您執行的管道旁的省略符號按鈕選擇 **檢視詳細資料** 功能表中。

1. 系統將會帶您前往執行中管道的詳細資訊頁面。

![管道詳情](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

從這裡您可以查看管道各個步驟的狀態，並擷取組建紀錄以進行診斷。檢視檔案 [部署程式碼](/help/implementing/cloud-manager/deploy-code.md) 以取得程式碼部署和測試執行的詳細資訊。

管道執行中的所有步驟都會顯示，其中尚未開始的步驟以灰色顯示。 完成的步驟會顯示其持續時間。

管道步驟完成後，會顯示摘要。

![步驟摘要](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

點選或按一下 **檢視詳細資料** 顯示連結 **持續時間** 區段。 這包括根據該計畫歷史趨勢的管道平均持續時間。

![持續時間](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

>[!NOTE]
>
>您只能查看正在執行或已執行至少一次的管道的詳細資訊。

## 取消管道 {#cancel}

如果管道處於驗證或建立影像階段，您可以安全地取消管道執行。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 在計畫總覽頁面，在頁面上按一下您要取消的管道的省略符號按鈕 **管道** 卡片。

   ![取消管道](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. 點選或按一下 **取消**.

或者，您可以從配管詳細資訊頁面取消配管。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 導覽至 **管道** 標籤從 **計畫總覽** 頁面，然後點選或按一下您要取消的管道。

1. 系統將會帶您前往執行中管道的詳細資訊頁面。

   ![取消管道詳細資料](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. 點選或按一下 **取消**.
