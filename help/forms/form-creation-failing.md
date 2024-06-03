---
title: 如何疑難排解表單建立失敗？
description: 疑難排解AEM Formsas a Cloud Service環境中表單建立的失敗。
feature: Adaptive Forms, Troubleshooting
role: User
source-git-commit: 23491130b44147753c5b98f316be5a9e5937afea
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# 發佈表單時出現問題{#form-creation-fails}

使用者更新至AEM Formsas a Cloud Service版本後 `2024.5.16461`：

**部分使用者** 建立表單時可能會遇到問題，其程度為當使用者建立表單時，建立對話方塊中會彈出以下錯誤訊息：

`A server error occurred. Try again after sometime.`

## 原因 {#cause-form-creation-fails}

發生此問題是因為作者發佈表單時沒有 **首次發佈範本** 已用在其中。 這會導致額外的 `jcr:uuid` 和其他受保護及系統產生的屬性重新命名為 `<template-path>/initial/jcr:content` 節點，導致後續表單建立失敗。

## 因應措施 {#resolution-form-creation-fails}

若要解決此問題，請執行以下步驟：

1. 確認您在表單中使用的範本沒有 `jcr:uuid` 和其他系統在路徑中產生的受保護屬性 `<template-path>/initial/jcr:content node`.
1. 使用範本主控台明確地發佈範本。
1. 現在，發佈範本時，請嘗試使用範本建立新表單。
1. 如果您在未來的版本中使用了範本更新，請再次發佈範本（如步驟2所述）以防止表單建立失敗問題。


<!--

# Issue {#form-creation-fails}

After updating to AEM Forms as a Cloud Service version `2024.5.16461.20240524T172309Z`, When a user publishes a form using an unpublished template, it fails to create a form and shows an error:

`Property is protected: jcr:uuid = 09e0d6be-f619-4405-b021-27eb1c5326d3`

## Solution {#troubleshoot-form-creation-fails}

To resolve the issue, perform the following workaround steps:

1. Publish the template explicitly using the template console.
    
    >[!NOTE]
    > Prior to this step ensure that the (unpublished) template does not have `jcr:uuid` and other system generated properties under the initial content's `jcr:content node`. To sort out it, first, sanitize the template to publish it explicitly.

    >[!NOTE]
    > This action doesn't replicate the initial content node.
1. Now, when your template is published, try creating new forms using the template.
1. If the template is changed in the future, publish it again as mentioned in the step 1.

-->










