---
title: 如何授與規則編輯器存取權給選取的使用者群組？
description: 使用適用性Forms的使用者類型各異，技能各異。 了解如何根據使用者的角色或功能，將規則編輯器的存取權限限制在使用者。
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 3%

---


# 將規則編輯器存取權授予給所選的使用者群組 {#grant-rule-editor-access-to-select-user-groups}

## 總覽 {#overview}

使用適用性Forms的使用者類型各異，技能各異。 雖然專家使用者可能擁有使用指令碼和複雜規則的適當知識，但可能有基本層級使用者，他們必須只使用適用性Forms的版面和基本屬性。

[!DNL Experience Manager Forms] 可讓您根據使用者的角色或功能，限制使用者的規則編輯器存取權。 在適用性Forms組態服務設定中，您可以指定 [使用者群組](forms-groups-privileges-tasks.md) 可檢視及存取規則編輯器的規則。

## 指定可存取規則編輯器的使用者群組 {#specify-user-groups-that-can-access-rule-editor}

1. 登入 [!DNL Experience Manager Forms] 管理員。
1. 在製作例項中，按一下 ![Adobe Experience Manager](assets/adobeexperiencemanager.png)Adobe Experience Manager >工具 ![錘](assets/hammer-icon.svg) > **[!UICONTROL 操作]** > **[!UICONTROL Web主控台]**. Web控制台在新窗口中開啟。

   ![1-2](assets/1-2.png)

1. 在 [!UICONTROL Web主控台] 視窗，找到並按一下 **[!UICONTROL 適用性表單設定服務]**. **[!UICONTROL 適用性表單設定服務]** 對話框。 請勿變更任何值，然後按一下 **[!UICONTROL 儲存]**.

   會建立檔案 `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` 在CRX-repository中。

1. 以管理員身分登入CRXDE。 開啟檔案 `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` 編輯。
1. 使用以下屬性指定可訪問規則編輯器的組的名稱（例如， RuleEditorsUserGroup），然後按一下 **[!UICONTROL 全部儲存]**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   若要啟用多個群組的存取權，請指定逗號分隔值的清單：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![建立使用者](assets/create_user_new.png)

   現在，當非指定使用者群組成員的使用者(此處    `RuleEditorsUserGroup`)點選欄位，編輯規則圖示( ![edit-rules1](assets/edit-rules1.png))無法在「元件」工具列中使用：

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   具有規則編輯器存取權的使用者可看見的元件工具列：

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   無法存取規則編輯器的使用者可看到的元件工具列

   有關向組添加用戶的說明，請參閱 [使用者管理與安全性](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).

