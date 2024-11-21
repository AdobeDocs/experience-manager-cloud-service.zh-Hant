---
Title: How to configure submit action to Marketo Engage for forms?
Description: Learn how to configure the submit action of Adaptive Form to send data to Marketo Engage.
Keywords: Submit data to Marketo engage, Configure submit action as Submit to Marketo Engage
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
source-git-commit: 681c194f997ab66f93beedad4eea273614e6797d
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 2%

---


# 設定提交動作以Marketo Engage現有表單

<span class="preview">此功能可在早期採用者方案下使用。 您可以從您的官方電子郵件ID寫信到aem-forms-ea@adobe.com ，以加入率先採用者計畫並請求存取該功能。</span>

![工作流程](/help/forms/assets/workflow-marketo-3.png)

最適化Forms編輯器提供&#x200B;**提交至Marketo Engage**&#x200B;提交動作，以將最適化Forms資料傳送至Adobe Marketo Engage進行處理。 您可以設定現有的最適化表單，在提交時提交資料至[Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home)。

提供多種現成可用的提交動作，用於處理表單提交。 您可以在[最適化表單提交動作](/help/forms/configure-submit-actions-core-components.md)文章中進一步瞭解這些選項。

## 設定提交動作以Marketo Engage表單時的考量

* 確認最適化表單已設定為Marketo Engage資料來源，以便在表單提交時提交資料給Marketo Engage。 不過，您可以將提交動作變更為替代動作，例如&#x200B;**提交至OneDrive**&#x200B;或&#x200B;**提交至SharePoint**，即使表單是以Marketo Engage資料結構描述設定亦然。

## 設定提交動作以Marketo Engage現有表單的先決條件

設定提交動作以Marketo Engage的先決條件：

* 設定最適化表單](/help/forms/use-marketo-engage-data-source-in-form.md)的[Marketo Engage資料來源，並將表單元素與Marketo Engage欄位繫結。

## 如何設定提交動作以Marketo Engage現有表單？

您可以設定最適化表單的提交動作，將資料提交至Adobe Marketo Engage。 若要將提交動作設定為Marketo Engage，請執行下列步驟：

1. 開啟最適化表單進行編輯。
1. 開啟內容樹狀結構並選取&#x200B;**[!UICONTROL 參考線容器]**。
1. 按一下最適化表單容器屬性![最適化表單容器屬性](/help/forms/assets/configure-icon.svg)圖示。 用於設定提交動作的調適型表單容器對話方塊開啟。
1. 開啟&#x200B;**[!UICONTROL 提交]**&#x200B;標籤，並選取提交動作作為&#x200B;**提交至Marketo Engage**。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

![Marketo提交動作](/help/forms/assets/marketo-engage-submit-action.png){width=50%， height=50%}


將最適化表單的提交動作設定為&#x200B;**提交至Marketo Engage**&#x200B;後，您可以將資料傳送至Adobe Marketo Engage進行處理。 資料可用來分析和最佳化行銷活動、自動化後續電子郵件，以及根據表單提交觸發工作流程。

## 常見問題集(FAQ)

**問：您可以變更表單的提交動作，以設定為與Marketo Engage結構描述連線嗎？**
**A：**&#x200B;依預設，當表單設定為與Marketo Engage結構描述連線時，會選取&#x200B;**送出至Marketo**&#x200B;動作。 不過，您可以視需要變更表單的提交動作。

## 下一步

您也可以將最適化表單與[Munchkin資料庫](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin)連線，以追蹤造訪次數、點按次數和表單提交次數。

## 相關的文章

{{af-submit-action}}

## 另請參閱

{{marketo-engage-see-also}}
