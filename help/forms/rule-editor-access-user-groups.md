---
title: 如何授予規則編輯器對選擇用戶組的訪問權限？
description: 有不同類型的用戶擁有不同的技能，可與適應性Forms合作。 瞭解如何根據用戶的角色或功能限制規則編輯器對用戶的訪問。
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 3%

---


# 將規則編輯器存取權授予給所選的使用者群組 {#grant-rule-editor-access-to-select-user-groups}

## 概覽 {#overview}

有不同類型的用戶擁有不同的技能，可與適應性Forms合作。 雖然專家用戶可能擁有使用指令碼和複雜規則的正確知識，但可能有基本級用戶，他們只能使用自適應Forms的佈局和基本屬性。

[!DNL Experience Manager Forms] 允許您根據用戶的角色或功能限制規則編輯器對用戶的訪問。 在自適應Forms配置服務設定中，可以指定 [用戶組](forms-groups-privileges-tasks.md) 可以查看和訪問規則編輯器。

## 指定可以訪問規則編輯器的用戶組 {#specify-user-groups-that-can-access-rule-editor}

1. 登錄到 [!DNL Experience Manager Forms] 作為管理員。
1. 在作者實例中，按一下 ![Adobe Experience Manager](assets/adobeexperiencemanager.png)Adobe Experience Manager>工具 ![錘](assets/hammer-icon.svg) > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。 Web控制台將在新窗口中開啟。

   ![1-2](assets/1-2.png)

1. 在 [!UICONTROL Web控制台] 窗口，查找並按一下 **[!UICONTROL 自適應表單配置服務]**。 **[!UICONTROL 自適應表單配置服務]** 對話框。 不更改任何值，然後按一下 **[!UICONTROL 保存]**。

   它建立一個檔案 `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` 在CRX儲存庫中。

1. 以管理員身份登錄到CRXDE。 開啟檔案 `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` 的子菜單。
1. 使用以下屬性指定可以訪問規則編輯器的組的名稱（例如，RuleEditorsUserGroup），然後按一下 **[!UICONTROL 全部保存]**。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   要啟用對多個組的訪問，請指定逗號分隔值的清單：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![建立使用者](assets/create_user_new.png)

   現在，當用戶不是指定用戶組的一部分時(此處    `RuleEditorsUserGroup`)點擊欄位，編輯規則表徵圖( ![編輯規則1](assets/edit-rules1.png))在「元件」工具欄中不可用：

   ![元件儲存器](assets/componentstoolbarwithre.png)

   具有規則編輯器訪問權限的用戶可見的元件工具欄：

   ![構件](assets/componentstoolbarwithoutre.png)

   對沒有規則編輯器訪問權限的用戶可見的元件工具欄

   有關向組添加用戶的說明，請參見 [用戶管理和安全](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html)。

