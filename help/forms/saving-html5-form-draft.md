---
title: 將HTML5表單儲存為草稿
description: 將HTML5表單儲存為草稿，並在稍後階段繼續填寫表單。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: HTML5 Forms,Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
hide: true
hidefromtoc: true
source-git-commit: 81a6c2b942df0e72a0b7d359f29c615a44640396
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 4%

---


# 將HTML5表單儲存為草稿 {#saving-an-html-form-as-a-draft}

<span class="preview"> HTML5 Forms功能屬於Early Access方案的一部分。 若要要求存取權，請將您的正式（工作）電子郵件ID傳送電子郵件至aem-forms-ea@adobe.com。
</span>

您可以將HTML5表單儲存為草稿，並在稍後階段繼續填寫表單。 Forms入口網站可讓任何使用者儲存和還原HTML5表單。 若要啟用「另存為草稿」功能，請將下列設定新增至設定檔節點：

## 允許另存為草稿功能的自訂設定檔 {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms可立即提供&#x200B;**另存為草稿**&#x200B;設定檔。 您可以使用另存為草稿設定檔來轉譯表單，以啟用HTML5表單的草稿功能。 您可以在&#x200B;**HTML Manager**&#x200B;中指定表單的Forms轉譯器設定檔。

若要對您現有的[自訂設定檔](/help/forms/custom-profile.md)啟用「另存為草稿」功能，請新增下列屬性至您的自訂設定檔節點：

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>字串</td>
   <td>true</td>
   <td><p>啟用另存為草稿功能</p> <p>此設定檔的。</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>字串</td>
   <td>true</td>
   <td><p>允許上傳附件</p> <p>使用此設定檔。</p> </td>
  </tr>
 </tbody>
</table>

## 草稿儲存和清單 {#drafts-storage-and-listing}

為表單啟用「另存為草稿」功能後；儲存表單時，該表單會列在「草稿和提交」元件中。 您可以擷取並開始填寫從「草稿和提交」元件中儲存的。

若要為「草稿和提交」元件啟用表單清單，請將下列屬性新增至設定檔節點：

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>字串</td>
   <td>true</td>
   <td>若要讓草稿和表單在提交後列在<br /> Forms Portal草稿和提交元件中</td>
  </tr>
 </tbody>
</table>

依預設，AEM Forms會將與表單草稿和提交相關聯的使用者資料儲存在發佈執行個體上的/content/forms/fp節點中。 您可以新增自訂儲存提供者，如需詳細資訊，請參閱[草稿與提交元件的自訂儲存](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/use-forms-portal/adding-custom-storage-provider-forms)。
