---
title: 具有不同資料選項的互動式通訊編輯器中的PDF預覽
description: 使用不同資料選項在互動式通訊編輯器中預覽PDF，以三種不同的方式預覽互動式通訊。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 371838c77beafa8c67259a865b25325632bea0b0
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 15%

---


# 互動式通訊編輯器中的 PDF 預覽

>[!NOTE]
>
> 互動式通訊功能在早期採用者程式中提供。 使用您的工作郵件地址寄送電子郵件至 `aem-forms-ea@adobe.com` 請求存取權限。

>[!IMPORTANT]
>
> **文件內容可能隨時變更**：此提示庫目前正在針對產品進行測試，可能會進行更新和修訂。隨著表單體驗建立工具在早期採用者方案期間持續發展，相關的提示、範例和最佳做法可能會有所變更。

PDF預覽功能可讓使用者以三種不同的方式預覽互動式通訊：沒有資料、使用本機JSON型資料或來自已設定資料模型的範例資料。

## 主要優點

- 使用範例資料預覽互動式通訊，以視覺化方式呈現與通訊合併時的即時資料。

- 上傳本機JSON資料檔案以產生資料導向預覽，無需後端設定。

- 使用連線表單資料模型(FDM)來模擬設計期間與範例資料的即時資料整合。

- 輕鬆地在資料選項（無資料、本機資料、FDM）之間切換，以驗證配置、結構和個人化。

## 具有不同資料選項的互動式通訊編輯器中的PDF預覽

不使用資料、本機資料或來自已設定資料模型的範例資料來預覽互動式通訊，以進行彈性的測試和驗證。

+++1.無資料預覽。

1.1.在IC編輯器中開啟互動式通訊。

1.2.使用[PDF預覽]選項，並選取[無資料]選項&#x200B;**來檢視沒有資料的通訊。**

![尋找IC檔案](/help/forms/interactive-communication/assets/nodata.png)

+++

+++2.使用本機JSON資料預覽

2.1.準備結構化JSON檔案。 如需參考，您可以從用於通訊的JSON結構描述[(FDM)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/work-with-form-data-model)複製範例資料。

2.2.在IC編輯器中，移至&#x200B;**PDF預覽** >使用本機資料。

2.3.選取並上傳您的JSON檔案，使用提供的資料呈現PDF預覽。

![尋找IC檔案](/help/forms/interactive-communication/assets/localdata.png)

+++

+++3.使用資料模型預覽 

3.1.選取&#x200B;**使用資料模型**，以使用已設定之IC表單資料模型(FDM)的範例資料。

3.2.預覽會自動填入模型欄位中的資料。 請確保範例資料在首次使用時儲存在FDM中，否則預覽可能會顯示為無資料。

![尋找IC檔案](/help/forms/interactive-communication/assets/datamodel.png)

+++

