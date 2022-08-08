---
title: 配置資產上載限制
description: '配置Adobe Experience Manager資產以限制用戶可以基於MIME類型上傳的資產類型。 它有助於防止意外上載不希望有的格式和惡意檔案。 '
source-git-commit: 3be29e4f76b53b4be7815e50ec42c627fec84b68
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---

# 配置資產上載限制 {#configure-asset-upload-restrictions}

您可以配置Adobe Experience Manager資產，以限制用戶可以基於MIME類型上傳的資產類型。

>[!IMPORTANT]
>
>預設情況下，Experience Manager Assets允許用戶上載所有MIME類型的資產。 但是，您可以配置設定，以僅限於用戶上載特定MIME類型的檔案。

## 必備條件 {#prerequisites-asset-upload-restrictions}

您必須具有管理員權限才能配置資產上載限制。

## 對資產上載應用限制 {#apply-restrictions-asset-uploadsssssss}

配置 [!DNL Experience Manager] 要限制用戶上載特定MIME類型的檔案，請執行以下操作：

1. 導航到 **[!UICONTROL 工具>資產>資產配置]**。

1. 按一下 **[!UICONTROL 上載限制]**。

1. 按一下 **[!UICONTROL 添加]** 定義允許的MIME類型。

1. 在文本框中指定MIME類型。 您可以按一下 **[!UICONTROL 添加]** 再次指定更多允許的MIME類型。 也可以按一下 ![刪除表徵圖](assets/delete-icon.svg) 從清單中刪除任何MIME類型。

1. 按一下「**[!UICONTROL 儲存]**」。

**示例1:允許將所有映像和PDF檔案上載到Experience Manager Assets**

要允許將所有格式的影像和PDF檔案上載到Experience Manager Assets，請執行以下設定：

![資產上載限制](assets/asset-upload-restrictions.png)

`image/*` 因為MIME類型允許以所有格式上載影像。 `application/pdf` 因為MIME類型允許將PDF檔案上載到Experience Manager Assets。

**示例2:允許將特定影像格式上載到Experience Manager Assets**

要將特定影像格式添加到允許的MIME類型並限制上載所有其他資產格式，請執行以下設定：

![資產限制](assets/asset-restrictions.png)

根據影像中描述的設定，可以將。JPG、.PNG和。GIF格式的影像上載到Experience Manager Assets。




