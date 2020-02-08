---
title: 將浮水印新增至您的數位資產
description: 瞭解如何使用浮水印功能將數位水印新增至資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 浮水印 {#watermarking}

Adobe Experience Manager(AEM)Assets中的浮水印功能可讓您在資產中新增數位水印，協助使用者驗證資產的真實性和版權所有權。 AEM Assets支援將文字用作PNG和JPEG檔案上的浮水印。

若要能夠套用浮水印至資產，請在「DAM更新資產」工作流程中新增「浮水印」步驟。

1. 點選／按一下AEM標誌，然後前往「工 **[!UICONTROL 具]** >工 **[!UICONTROL 作流程]** > **[!UICONTROL 模型]**」。
1. 從「工作流模型」頁面中，選擇「 **[!UICONTROL DAM更新資產」工作流]** ，然後按一下「 **[!UICONTROL 編輯」]**。

1. 從「側面板」中，將「 **[!UICONTROL 新增浮水印]** 」步驟拖曳至「DAM更新資產」工作流程。

<!--  ![Darg add watermark step in the DAM update asset workflow](assets/add_watermark_step_aem_assets.png) -->

>[!NOTE]
>
>將「新增浮水印」步驟置於「處理縮圖」步驟之前的任意位置。

1. 開啟「 **[!UICONTROL 新增浮水印]** 」步驟以顯示其屬性。
1. 在「參 **[!UICONTROL 數]** 」標籤中，在各種欄位中指定有效值，包括文字、字型類型、大小、顏色、位置、方向等。 若要確認變更，請點選／按一下「完成」圖示。

<!--   ![Provide the arguments in the add watermark step in Assets](assets/arguments_add_watermark_aem_assets.png) -->

1. 使用浮水印 **[!UICONTROL 步驟儲存DAM更新資產]** (Dam Update Asset)工作流程。
1. 從「資產」使用者介面上傳範例資產。 浮水印會在您在上述步驟中設定的位置顯示字型大小、顏色等。
