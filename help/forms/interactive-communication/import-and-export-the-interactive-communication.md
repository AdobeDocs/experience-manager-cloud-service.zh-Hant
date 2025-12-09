---
title: 匯入與匯出互動式通訊
description: 匯入和匯出互動式通訊可讓使用者順暢地遷移、重複使用和管理跨環境的通訊。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 9adc7a5669d8bf1e64cc93998cb2f91ffa9d3dd6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 18%

---


# 匯入與匯出互動式通訊

>[!NOTE]
>
> 互動式通訊功能在早期採用者程式中提供。 使用您的工作郵件地址寄送電子郵件至 `aem-forms-ea@adobe.com` 請求存取權限。

>[!IMPORTANT]
>
> **文件內容可能隨時變更**：此提示庫目前正在針對產品進行測試，可能會進行更新和修訂。隨著表單體驗建立工具在早期採用者方案期間持續發展，相關的提示、範例和最佳做法可能會有所變更。

互動式通訊(IC)的匯入和匯出功能可讓使用者順暢地遷移、重複使用和管理跨環境的通訊。 它可讓您從某個環境匯出互動式通訊(IC)及其關聯的片段和資料模型，並將其匯入另一個環境，以確保一致性並減少部署期間的重複工作。

## 主要優點

- 簡化跨環境的IC移轉。
- 保留片段、資料模型和相依性。
- 減少跨專案重新建立IC的工作量。

## 匯入與匯出互動式通訊

在一個環境中建立互動式通訊(IC)，並透過以下步驟匯出和匯入在另一個環境中重複使用它：

+++1.如何匯出互動式通訊

1.1.選取[建立的互動式通訊](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/interactive-communication/create-interactive-communication) (IC)。
1.2.按一下&#x200B;**下載**&#x200B;選項，將其匯出為ZIP檔。
1.3.下載的ZIP檔案包含IC及其選取的&#x200B;**範本**、**片段**&#x200B;和&#x200B;**資料模型**。

![尋找IC檔案](/help/forms/interactive-communication/assets/downloadic.png)
+++

+++2.如何匯入互動式通訊

2.1.前往目標環境。
2.2.瀏覽至&#x200B;**Forms > Forms和檔案>建立>檔案上傳**。
2.3.上傳ZIP檔案至&#x200B;**匯入** IC。

![尋找IC檔案](/help/forms/interactive-communication/assets/uploadfile.png)

2.4.上傳後，IC會與其相關的片段和資料模型一起出現。

![尋找IC檔案](/help/forms/interactive-communication/assets/importfragment.png)
+++

+++3.匯入和匯出片段

3.1.若要匯出，請從&#x200B;**Forms > Forms和檔案**&#x200B;中選取所需的片段，然後按一下&#x200B;**下載**，將其匯出為ZIP檔。

3.2.若要匯入，請前往目標環境，導覽至「Forms > Forms和檔案>建立> **檔案上傳**」，然後上傳匯出的ZIP檔案。

如此一來，就能在不同環境中輕鬆重複使用片段，確保設計的一致性，並減少重複工作。
+++
