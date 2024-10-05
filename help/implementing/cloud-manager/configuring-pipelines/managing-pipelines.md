---
title: 管理管道
description: 了解如何管理現有管道，包括將其編輯、執行和刪除。
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 69%

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

## 管道視窗 {#pipelines}

**管道**&#x200B;視窗顯示所選方案所有管道的完整清單。這很有用，因為它提供的資訊比[管道卡](#pipeline-card)提供的資訊更完整。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從&#x200B;**方案總覽**&#x200B;頁面，選取&#x200B;**管道**&#x200B;索引標籤以切換至&#x200B;**管道**&#x200B;視窗。

1. 在這裡，您可以看到方案所有管道的清單，並啟動和停止管道執行，就像在&#x200B;**管道卡**&#x200B;中一樣。

如果管道正在執行，按一下&#x200B;**狀態**&#x200B;欄中的資訊圖示會顯示有關執行的詳細資訊。

![管道執行詳細資訊](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

按一下&#x200B;**檢視詳細資訊**，即可前往[管道執行詳細資訊](#view-details)。

您也可以按一下管道的省略符號按鈕，以採取適用於管道狀態的其他動作，例如[編輯](#editing-pipelines)它或[取消執行](#cancel)。

![管道動作](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-actions.png)

## 活動視窗 {#activity}

**活動**&#x200B;視窗會顯示所選方案以及其他重要方案事件的所有管道執行的完整清單。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從&#x200B;**方案總覽**&#x200B;頁面，選取&#x200B;**活動**&#x200B;索引標籤以切換至&#x200B;**活動**&#x200B;視窗。

1. 在這裡，您可以看到方案所有管道執行的清單，包括目前和歷史執行。

如果管道正在執行，按一下&#x200B;**狀態**&#x200B;資料行中的資訊圖示將會顯示執行的詳細資訊。

![管道執行詳細資訊](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

點選或按一下代表管道執行的資料列，系統就會將您導向管道執行的[詳細資料](#view-details)。

您也可以按一下省略符號按鈕，以針對管道執行採取進一步的動作，例如檢視其詳細資料或下載記錄，這會帶您前往[管道詳細資料頁面](#view-details)。

![管道執行動作](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-execution-actions.png)

## 執行管道 {#running-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 瀏覽至&#x200B;**管道**&#x200B;卡 (位於&#x200B;**方案總覽**&#x200B;頁面)，並按一下您執行的管道旁的省略符號按鈕，從選單中選取&#x200B;**執行**。

1. 此管道執行開始，並由&#x200B;**狀態**&#x200B;欄顯示。

您可以查看執行的詳細資訊，只要再按一下省略符號按鈕，並選取「**[檢視詳細資訊](#view-details)**」。

依管道的類型而定，您也許可以取消執行，只要再按一下省略符號按鈕，並選取「**取消**」。

## 編輯管道 {#editing-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 瀏覽至&#x200B;**管道**&#x200B;卡 (位於&#x200B;**程式概觀**&#x200B;頁面)，並按一下您要編輯的管道旁的省略符號按鈕，然後從選單中選取&#x200B;**編輯**。

1. **編輯生產管道**&#x200B;或是&#x200B;**編輯非生產管道**&#x200B;對話框會隨即顯示，讓您可以對您在建立管道時輸入的詳細資訊進行編輯。

   * 如需有關管道可用的欄位和設定選項的詳細資訊，請參閱以下頁面。
      * [設定生產管道](configuring-production-pipelines.md)
      * [設定非生產管道](configuring-non-production-pipelines.md)

1. 按一下&#x200B;**更新**，在您完成編輯管道之後。

>[!NOTE]
>
>您無法編輯執行中的管道。

>[!NOTE]
>
>私人存放庫不支援 Web 層和設定管道。請參閱[在Cloud Manager中新增私人存放庫](/help/implementing/cloud-manager/managing-code/private-repositories.md)，以取得詳細資訊和完整的限制清單。

## 刪除管道 {#deleting-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 瀏覽至&#x200B;**管道**&#x200B;卡 (位於&#x200B;**方案總覽**&#x200B;頁面)，並按一下您執行的管道旁的省略符號按鈕，從選單中選取&#x200B;**刪除**。

>[!NOTE]
>
>您無法刪除執行中的管道。

## 檢視管道詳細資訊 {#view-details}

您可以檢視管道的詳細資訊，以檢視其上次執行的狀態和記錄。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 瀏覽至&#x200B;**管道**&#x200B;卡 (位於&#x200B;**方案總覽**&#x200B;頁面)，並按一下您執行的管道旁的省略符號按鈕，從選單中選取&#x200B;**檢視詳情**。

1. 系統將會帶您前往執行中管道的詳細資訊頁面。

![管道詳情](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

從這裡您可以查看管道各個步驟的狀態，並擷取組建紀錄以進行診斷。如需程式碼部署和測試執行的詳細資訊，請參閱檔案[部署您的程式碼](/help/implementing/cloud-manager/deploy-code.md)。

管道執行中的所有步驟都會顯示，尚未開始的步驟會顯示為灰色。已完成的步驟會顯示其持續時間。

管道步驟完成後，將顯示摘要。

![步驟摘要](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

選取&#x200B;**檢視詳細資料**&#x200B;連結以顯示&#x200B;**持續時間**&#x200B;區段。 這包括基於該方案歷史趨勢的管道平均持續時間。

![持續時間](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

如果您的管道包含引發問題的&#x200B;**代碼掃描**&#x200B;步驟，您可以點選或按一下「**下載詳細資訊**」按鈕，以查看未通過的[程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)清單。

![程式碼品質問題](assets/managing-pipelines-code-quality-issues.png)

CSV 檔案中有「**專案檔案位置**」欄，會指出違規程式碼的位置。此欄是專案相對路徑，而「**檔案位置**」欄是 Maven 產生。

![專案程式碼掃描問題詳細資訊](assets/managing-pipelines-code-quality-details.png)

>[!NOTE]
>
>您只能查看正在執行或已執行至少一次的管道的詳細資訊。

## 取消管道 {#cancel}

如果管道處於驗證或建立影像階段，您可以安全地取消管道執行。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從方案總覽頁面，在&#x200B;**管道**&#x200B;卡上按一下您要取消的管道的省略符號按鈕。

   ![正在取消管道](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. 選取&#x200B;**取消**。

或者，您可以從配管詳細資訊頁面取消配管。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從&#x200B;**方案總覽**&#x200B;頁面瀏覽至&#x200B;**管道**&#x200B;索引標籤，並選取您要取消的管道。

1. 系統將會帶您前往執行中管道的詳細資訊頁面。

   ![取消管道詳細資料](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. 選取&#x200B;**取消**。
