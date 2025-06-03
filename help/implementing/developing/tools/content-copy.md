---
title: 內容複製工具
description: 內容複製工具可讓使用者根據需求，從AEM as a Cloud Service上的生產環境複製可變內容，以便用於測試目的的較低環境。
exl-id: 5883e4bc-9861-498e-bd35-32ff03d901cc
feature: Developing
role: Admin, Architect, Developer
source-git-commit: cf2f64dec2ff39ea237dd092b3049bf9b8cd40e7
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 35%

---

# 內容複製工具 {#content-copy}

內容複製工具可讓使用者根據需求，從AEM as a Cloud Service上的生產環境複製可變內容，以便用於測試目的的較低環境。

## 簡介 {#introduction}

目前的真實資料對於測試、驗證和使用者接受度很有價值。內容複製工具可讓您將內容從生產AEM as a Cloud Service環境複製到測試、開發或[快速開發環境(RDE)](/help/implementing/developing/introduction/rapid-development-environments.md)環境，以進行此類測試。

要複製的內容由內容集定義。內容集包含JCR路徑清單，這些路徑包含要從來源製作服務環境複製到相同Cloud Manager程式中目標製作服務環境的可變內容。 內容集中允許使用以下路徑。

```text
/content
/conf/**/settings/wcm
/conf/**/settings/dam/cfm/models
/conf/**/settings/graphql/persistentQueries
/etc/clientlibs/fd/themes
```

複製內容時，來源環境是真實的來源。

* 如果路徑相同，在目的地環境中修改了內容，則來源中的內容會覆寫內容。
* 如果路徑不同，來源中的內容會與目標中的內容合併。

## 權限 {#permissions}

要使用內容複製工具，在來源和目標環境中都需要某些許可權。

| 內容副本功能 | AEM管理員群組 | 部署管理員角色 |
|---|---|---|
| 建立和修改[內容集](#create-content-set) | 不需要 | 必填 |
| 開始獲取消[內容副本程序](#copy-content) | 必填 | 必填 |

如需許可權及其設定方式的詳細資訊，請參閱[AEM as a Cloud Service團隊和產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md)。

## 建立內容集 {#create-content-set}

在複製任何內容之前，必須定義一個內容集。定義內容集後，即可重複使用內容集來複製內容。 請依照下列步驟操作，以建立內容集。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 使用側邊導覽面板，從&#x200B;**總覽**&#x200B;頁面導覽至&#x200B;**內容集**&#x200B;索引標籤。

1. 在熒幕的右上方，按一下&#x200B;**新增內容集**。

   ![內容集](assets/content-sets.png)

1. 在精靈的&#x200B;**詳細資料**&#x200B;索引標籤上，提供內容集的名稱和說明，並選取&#x200B;**繼續**。

   ![內容詳細資料](assets/add-content-set-details.png)

1. 在精靈上的&#x200B;**內容路徑**&#x200B;索引標籤，指定要包含在內容集中的可變內容路徑。

   1. 在&#x200B;**新增包含路徑**&#x200B;中輸入路徑欄位。
   1. 按一下「**新增路徑**」，將路徑新增至內容集。
   1. 必要時，再按一下「**新增路徑**」。
      * 最多允許50個路徑。

   ![新增路徑至內容集](assets/add-content-set-paths.png)

1. 如果您必須調整或限制內容集，則可以排除子路徑。

   1. 在包含的路徑清單中，按一下您想要限制的路徑旁的&#x200B;**新增排除子路徑**。
   1. 在選取的路徑下輸入要排除的子路徑。
   1. 選取&#x200B;**排除路徑**。
   1. 再次選取&#x200B;**新增排除子路徑**&#x200B;以視需要新增要排除的其他路徑。
      * 排除的路徑必須相對於包含的路徑。
      * 排除的路徑數量沒有限制。

   ![排除路徑](assets/add-content-set-paths-excluded.png)

1. 您可以視需要編輯指定的路徑。

   1. 按一下已排除子路徑旁邊的X，以便刪除它們。
   1. 按一下路徑旁的省略符號按鈕，即可顯示&#x200B;**編輯**&#x200B;和&#x200B;**刪除**&#x200B;選項。

   ![編輯路徑清單](assets/add-content-set-excluded-paths.png)

1. 選取&#x200B;**建立**&#x200B;以建立內容集。

內容集現在可用於在環境之間複製內容。

## 正在編輯內容集 {#edit-content-set}

請依照下列步驟，建立新的內容。不要按一下&#x200B;**新增內容集**，請從主控台選取現有內容集，然後從省略符號選單中選取&#x200B;**編輯**。

![編輯內容集](assets/edit-content-set.png)

編輯內容集時，您可以展開已設定的路徑以顯示排除的子路徑。

## 正在複製內容 {#copy-content}

建立內容集後，您就可以用它來複製內容。 請依照下列步驟操作，以便複製內容。

>[!NOTE]
> 當[內容轉移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md)作業正在環境中執行時，請勿在該環境中使用內容複製。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 從&#x200B;**概觀**&#x200B;頁面瀏覽到&#x200B;**環境**&#x200B;畫面。

1. 從&#x200B;**環境**&#x200B;畫面瀏覽&#x200B;**內容集**&#x200B;頁面。

1. 從控制台選擇一個內容集，然後從省略號選單選擇&#x200B;**複製內容**。

   ![內容複製](assets/copy-content.png)

   >[!NOTE]
   >
   >在以下情況下可能無法選擇環境：
   >
   >* 使用者沒有適當的權限。
   >* 環境中有正在執行的管道或正在進行的複製內容作業。
   >* 環境正在休眠或啟動。

1. 在&#x200B;**複製內容**&#x200B;對話框中，指定內容副本作業的來源和目的地。

   ![正在複製內容](assets/copying-content.png)

   * 內容只能從較高的環境複製到較低的環境，或在開發/RDE環境之間複製，其中環境的階層如下所示（從最高到最低）：
      * 生產
      * 中繼
      * 開發/RDE

1. 如有必要，您也可以選擇在復製程式中&#x200B;**包含存取控制清單**。

1. 選取&#x200B;**複製**。

複製程序開始。複製過程的狀態反映在所選內容集的控制台中。

## 內容複製活動 {#copy-activity}

您可以在&#x200B;**複製內容活動**&#x200B;中監控複製過程的狀態頁面。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 從&#x200B;**概觀**&#x200B;頁面瀏覽到&#x200B;**環境**&#x200B;畫面。

1. 從&#x200B;**環境**&#x200B;畫面瀏覽&#x200B;**複製內容活動**&#x200B;頁面。

![內容複製活動](assets/copy-content-activity.png)

### 內容複製狀態 {#statuses}

開始複製內容後，該過程可能具有以下狀態之一。

| 狀態 | 說明 |
|---|---|
| 進行中 | 內容複製作業正在進行中 |
| 已失敗 | 內容複製作業失敗 |
| 完成 | 內容複製作業成功完成 |
| 已取消 | 使用者在啟動內容複製操作後將其取消 |

### 取消復製程式 {#canceling}

如果您在啟動內容復製作業後必須中止該作業，則可選擇取消該作業。

若要這麼做，請在&#x200B;**複製內容活動**&#x200B;頁面上，從您先前啟動的復製程式省略符號選單中選取&#x200B;**取消**&#x200B;動作。

![取消內容復本](assets/content-copy-cancel.png)

>[!NOTE]
>
>取消內容複製操作時，可能會導致目標環境中的內容出現部分副本。 此情況可能會使目的地環境處於無法使用的狀態。
>
>如果您的環境因取消而處於這類狀態，請聯絡Adobe客戶服務以尋求協助。

### 存取記錄檔 {#accessing-logs}

您可以檢查來源和目的地環境的記錄，以瞭解任何已完成的內容復製程式。

若要這麼做，請在&#x200B;**複製內容活動**&#x200B;頁面上，從您要檢閱記錄檔的復製程式省略符號選單中選取&#x200B;**記錄檔**&#x200B;動作，然後選取哪個環境。

![正在存取複製內容程式的記錄檔](assets/copy-content-logs.png)

記錄檔會下載到您的本機電腦。 如果下載未開始，請檢查您的快顯封鎖程式設定。

## 限制 {#limitations}

內容複製工具具有以下限制。

* 內容無法從較低層級的環境複製到較高層級的環境。
* 內容只能從製作服務複製到製作服務。
* 跨程序內容複製是不可能的。
* 在同一環境中運行並發內容複製作業是不可能的。
* 每個內容集最多可以指定50個路徑。 排除的路徑沒有數量限制。
* 請勿使用內容複製工具作為複製或映象工具，因為它無法追蹤來源上已移動或刪除的內容。
* 內容複製工具沒有版本設定功能，且自上次內容復製作業以來，無法自動在內容集中的來源環境中偵測修改的內容或建立的內容。
   * 如果您只想使用內容變更來更新目的地環境，則自上次內容復製作業以來，您必須建立內容集。 然後，指定自上次內容復製作業以來進行變更的來源例項上的路徑。
* 版本資訊不包含在內容副本中。
* [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)可以根據通用唯一識別碼(UUID)指定參考欄位。 此類UUID是存放庫專屬的，因此在複製內容片段時，內容複製工具會在目標環境中重新計算這些UUID。
