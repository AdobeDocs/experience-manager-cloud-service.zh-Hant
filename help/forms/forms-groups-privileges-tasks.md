---
title: AEM Formsas a Cloud Service提供哪些立即可用的使用者群組？
description: 現成可用的使用者群組清單以及指派給每個群組的許可權
exl-id: bd66ce92-14d9-47fe-b5d3-022e3e468d25
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 21%

---

# 群組與權限 {#aem-forms-on-osgi-groups-and-privileges}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/forms-groups-privileges-tasks.html) |
| AEM as a Cloud Service  | 本文章 |

您可以 [建立群組](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) 並指派原則和 [使用者](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) 至群組。 這些原則可控制屬於群組之使用者的許可權。

設定後 [!DNL AEM Forms] as a Cloud Service，下表列出的群組如下 [!DNL forms-users] 和表單 — 超級使用者，可自動用於指派：

<table>
 <tbody>
  <tr>
   <td>群組</td> 
   <td>權限</td> 
  </tr>
  <tr>
   <td>[!DNL forms-users] <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>建立、預覽、發佈及提交最適化Forms</li> 
    <!-- <li>Create, preview, and publish interactive communications and document fragments</li> -->
     <li>將資產上傳至AEM執行個體</li> 
     <li>建立主題</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>[!DNL forms-power-user]</td> 
   <td>
    <ul> 
     <li>Create, preview, publish, and submit Adaptive Forms</li> 
     <li>Create, preview, and publish interactive communications and document fragments</li> 
     <li>Create scripts for Adaptive Forms using code editor</li> 
     <li>Upload assets including scripts</li> 
     <li>Create themes</li> 
     <li>Import packages containing XDP</li> 
    </ul> </td> 
  </tr>
 <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>Review submissions</li> 
     <li>Approve or reject submissions</li> 
    </ul> </td> 
  </tr> -->
  <tr>
   <td>[!DNL template-authors] <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>建立及預覽最適化Forms <!-- or interactive communications --> 範本</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>[!DNL fdm-authors]</p> </td> 
   <td>
    <ul> 
     <li>建立和修改表單資料模型</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Access Correspondence Management letters or interactive communications using Agent UI</li> 
    </ul> </td> 
  </tr> --> 
  <!-- <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> -->
    <!-- <li>Create an inbox application</li>  -->
    <!-- <li>Create a workflow model</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL workflow-users]</td> 
   <td>
    <ul> 
     <li>Use AEM inbox applications<br /> -->
     <!-- 
     <strong>Note: </strong>You must have cm-agent-users and [!DNL workflow-users] group assignments to access Interactive Communications Agent UI in AEM inbox.</li>  -->
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL fd-administrators]</td> 
   <td>
    <ul> 
     <!-- <li>Configure PDF Generator</li> --> 
     <!-- <li>Configure Watched folder</li> -->
     <li>管理工作流程應用程式</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

## 另請參閱

* [Cloud Service 環境上線](/help/forms/setup-forms-cloud-service.md)
* [設定本機開發環境](/help/forms/setup-local-development-environment.md)
* [從 AEM 6.5 Forms 移轉到 Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [建立獨立的最適化表單](/help/forms/creating-adaptive-form-core-components.md)
* [將最適化表單新增至AEM Sites頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)



