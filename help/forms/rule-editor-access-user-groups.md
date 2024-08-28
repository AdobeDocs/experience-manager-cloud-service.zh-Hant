---
title: 如何提供aem最適化表單規則編輯器的存取權以選取使用者群組？
description: 有各種型別的使用者具備最適化Forms所需的各種技能。 瞭解如何根據使用者的角色或功能限制使用者的規則編輯器存取權。
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
hide: true
hidefromtoc: true
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%

---


# 將規則編輯器存取權授予給所選的使用者群組 {#grant-rule-editor-access-to-select-user-groups}

## 概觀 {#overview}

有各種型別的使用者具備最適化Forms所需的各種技能。 雖然專家使用者可能擁有使用指令碼和複雜規則的正確知識，但可能有基礎級別的使用者，他們只能使用最適化Forms的版面和基本屬性。

[!DNL Experience Manager Forms]可讓您根據使用者的角色或功能限制使用者的規則編輯器存取權。 在最適化Forms組態服務設定中，您可以指定可檢視及存取規則編輯器的[使用者群組](forms-groups-privileges-tasks.md)。

## 指定可存取規則編輯器的使用者群組 {#specify-user-groups-that-can-access-rule-editor}

1. 以系統管理員身分登入[!DNL Experience Manager Forms]。
1. 在作者執行個體中，按一下![Adobe Experience Manager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Tools ![hammer](assets/hammer-icon.svg) > **[!UICONTROL 作業]** > **[!UICONTROL Web主控台]**。 Web主控台會在新視窗中開啟。

   ![1-2](assets/1-2.png)

1. 在[!UICONTROL 網頁主控台]視窗中，找到並按一下&#x200B;**[!UICONTROL 最適化表單設定服務]**。 **[!UICONTROL 最適化表單設定服務]**&#x200B;對話方塊就會顯示。 不要變更任何值，然後按一下[儲存]。****

   它會在CRX-repository中建立檔案`/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config`。

1. 以管理員身分登入CRXDE。 開啟檔案`/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config`進行編輯。
1. 使用以下屬性來指定可存取規則編輯器的群組名稱（例如RuleEditorsUserGroup），然後按一下&#x200B;**[!UICONTROL 「儲存全部」]**。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   若要啟用多個群組的存取權，請指定逗號分隔值清單：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![建立使用者](assets/create_user_new.png)

   現在，當使用者不是指定使用者群組的一部分時(此處    `RuleEditorsUserGroup`)點選欄位，「元件」工具列中無法使用「編輯規則」圖示(![edit-rules1](assets/edit-rules1.png))：

   ![componentstolbarwithre](assets/componentstoolbarwithre.png)

   具有規則編輯器存取許可權的使用者看得見的元件工具列：

   ![componentstolbarwithoutre](assets/componentstoolbarwithoutre.png)

   沒有規則編輯器存取許可權的使用者看得見的元件工具列

   如需將使用者新增至群組的說明，請參閱[使用者管理與安全性](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html)。

