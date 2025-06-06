---
title: 如何在AEM Forms中設定「外出」設定？
description: 在休假或休假時委派任務以無縫執行工作流程。
exl-id: c7e436f1-8e1c-4334-b3dc-ab9800695301
feature: Adaptive Forms, Workflow
role: Admin, User
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 1%

---


# 設定「外出」設定 {#configure-out-of-office-settings}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/configure-out-of-office-settings.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

如果您計畫不在辦公室，則可以指定指定指定給您該期間之料號的變更。

您可以選擇指定休假設定的開始日期和時間，以及結束日期和時間，使其生效。 如果您位在與伺服器不同的時區，則使用使用者端的時區。

您可以設定所有專案皆傳送至的預設接收者。 您也可以指定特定程式中的專案例外，以傳送給其他使用者或保留在收件匣中，直到您返回。 如果指定的人員也在外面，則專案會傳送給指定的使用者。 如果無法將專案指派給不在辦公室的使用者，則該專案會保留在您的收件匣中。

您可以根據工作流程模型來區隔專案委派。 例如，您可以將與「工作流程A」相關的專案指定給使用者A，並將與「工作流程B」相關的專案指定給使用者B。


>[!NOTE]
>
>* 當您啟用「不在辦公室」設定時，在啟用此設定之前，收件匣中所有可用的專案都會保留在您的收件匣中。 僅委派在啟用設定後收到的專案。
>* 當您關閉「外出」設定時，委派的專案不會自動指派回您。 您可以使用索賠功能來指定料號給您。
>* 當使用者A將專案委派給使用者B，而使用者B進一步委派給使用者C，則專案僅被指派給使用者C，而不是使用者B。
>* 當工作分派中有回圈時，任務會保留為原始使用者。 例如，當使用者A將專案委派給使用者B使用者B將專案委派給使用者C、使用者C將專案委派給使用者D，而使用者D將專案委派給使用者B時，系統會建立一個回圈。 在此情況下，專案仍會保留在原始使用者中。 使用者A是上述範例中的原始使用者。

## 啟用您帳戶的「外出」設定 {#enable-out-of-office}

執行以下步驟來啟用您帳戶的郵件答錄機設定，並將您的收件匣專案委派給其他使用者：

1. 登入您的AEM執行個體。 選取![收件匣](assets/bell.svg)圖示，然後選取&#x200B;**[!UICONTROL 全部檢視]**。 您的收件匣專案清單隨即顯示。
1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;按鈕旁的![檢視選擇器](assets/viewlist.svg)或![檢視選擇器](assets/calendar.svg)圖示，並選取&#x200B;**[!UICONTROL 設定]**。 設定對話方塊隨即顯示。
1. 開啟[設定]對話方塊上的[外出] **&#x200B;**&#x200B;索引標籤。
1. 選取&#x200B;**[!UICONTROL 啟用/停用]**&#x200B;按鈕以啟用「外出」設定。
1. 指定設定的&#x200B;**[!UICONTROL 開始時間]**&#x200B;和&#x200B;**[!UICONTROL 結束時間]**。 專案只會在指定的期間內委派。 將&#x200B;**[!UICONTROL 結束時間]**&#x200B;欄位保留空白以委派專案無限期。
1. 選取&#x200B;**[!UICONTROL 在此期間]**&#x200B;轉寄我的專案核取方塊。 如果您未選取選項也未指定受託人，則您的專案不會轉寄給任何使用者。 雖然您已離開並啟用此設定，但專案仍會保留在您的收件匣中。
1. 選取&#x200B;**[!UICONTROL 新增被指定者]**。 在&#x200B;**[!UICONTROL 受指派人]**&#x200B;欄位中指定要委派專案的使用者。 指定要委派給指定使用者的&#x200B;**[!UICONTROL 工作流程模型]**。 您可以選取多個工作流程模型。

   此外，若要將所有專案（不論工作流程模型為何）指派給特定使用者，請從「工作流程模型」下拉式清單中選取&#x200B;**[!UICONTROL 所有工作流程]**。<br>

   若要針對除了少數工作流程模型以外的所有工作流程模型，將專案指派給特定使用者，請從[工作流程模型]下拉式清單中選取&#x200B;**[!UICONTROL 所有工作流程]**，選取&#x200B;**[!UICONTROL +新增例外]**，並指定要省略的工作流程模型。
   <br>

   重複該步驟以新增更多受指派人。<br>

   >[!NOTE]
   >
   >受指派人的順序很重要。 當專案被指派給已啟用休假設定的使用者時，專案會根據指定的受指派人清單以新增受指派人的順序進行評估。 當專案符合條件時，即會指派給受指派人，且不會勾選下一個受指派人。


1. 選取&#x200B;**[!UICONTROL 儲存]**。此設定會在指定的開始日期和時間生效。 如果您在離開辦公室時登入，則在變更您的設定之前，不會將您視為在辦公室中。

現在，系統會自動將休假期間指派給您的專案指派給指定的受指派人。
![外出](assets/out-of-office.png)

>[!NOTE]
>
>(僅適用於以Forms為中心的工作流程專案)使用工作流程中&#x200B;**[!UICONTROL 指派任務]**&#x200B;步驟的「休假中」設定&#x200B;**選項，啟用**&#x200B;允許受指派人進行委派。 只有已啟用上述選項的專案才會委派給其他使用者。
>(僅適用於以Forms為中心的工作流程專案)啟用工作流程中&#x200B;**[!UICONTROL 指派任務]**&#x200B;步驟的「休假中」設定&#x200B;**選項，讓**&#x200B;允許受指派人進行委派。 只有已啟用前述選項的專案才會委派給其他使用者。

## 限制 {#limitations}

* 不支援指派專案給群組。
* 目前不支援為專案工作啟用「不在辦公室」功能。
