---
title: 資產選擇器集合
description: 使用資產選擇器集合。
role: Admin,User
exl-id: 1687e7d5-eb7e-4eb7-8747-e5dc6afacd5b
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 7%

---

# 資產選擇器集合 {#asset-selector-collections}

收藏集是Asset Selector中的一組資產、資料夾或其他收藏集。 使用收藏集在使用者之間共用資產。和檔案夾不同，收藏集可包含來自不同位置的資產。

Asset Selector中的Micro Front-end Collections可立即在唯讀模式下使用。 它會直接從您有權存取的[!DNL Experience Manager Assets]存放庫擷取資產和集合。

>[!NOTE]
>
>確保您有權存取[!DNL Experience Manager Assets] [imsOrg](/help/assets/asset-selector-properties.md)和集合。

Asset Selector中的Micro Front-end Collections可立即在唯讀模式下使用。 它會直接從您有權存取的Experience Manager Assets存放庫擷取資產和集合，並從您的Experience Manager Assets存放庫繼承公開和私人資料夾的屬性。 深入瞭解[在Assets檢視](/help/assets/manage-collections-assets-view.md#create-collection)中建立公開或私用集合。

您可以在「資產選擇器」中，以邊欄檢視和模型檢視來檢視集合。

邊欄檢視中的![集合](assets/collections-rail-modal-view.png)

<!--
Additionally, you can [customize](/help/assets/asset-selector-customization.md) the `featureSet` property to enable or disable collections in Asset Selector. See [enable or disable Collections tab](#enable-disable-collections-tab).-->

此外，您也可以自訂「系列」標籤下資產的選擇。 若要這麼做，您可以使用`handleSelection`自訂它。 請參閱[使用物件結構描述](/help/assets/asset-selector-customization.md#handling-selection)處理Assets的選取專案。

## 檢視集合 {#view-collections}

資產選取器可讓您在![清單檢視](assets/do-not-localize/list-view.png)清單檢視或![格線檢視](assets/do-not-localize/grid-view.png)格線檢視中檢視集合。 檢視資產選擇器[&#128279;](overview-asset-selector.md#types-of-view)中的檢視型別。

## 將資產拖放至收藏集 {#collection-drag-and-drop}

您可以直接從Author環境中的[!DNL Assets as a Cloud Service]檢視將資產拖放至Collections。 若要這麼做，請將資產從Assets標籤拖曳至Asset Selector應用程式的「集合」工作區域，以建置豐富的應用程式。

>[!NOTE]
>
>* 只有在邊欄檢視中才能拖放資產。
>* 您只能拖放檔案（資產），不能拖放資料夾。

另一方面，您也可以直接[啟用或停用集合](asset-selector-customization.md#enable-disable-drag-and-drop)中的拖放資產。

## 停用在集合中選擇資產 {#disable-selection-collection}

「停用選取」可用來隱藏或停用資產或資料夾無法選取的功能。 它會隱藏卡片或資產中的「選取」核取方塊，使其無法選取。 請參閱[停用選取專案](/help/assets/asset-selector-customization.md#disable-selection)。

## 啟用或停用集合索引標籤 {#enable-disable-collections-tab}

資產選擇器可讓您根據需求和可用性來自訂元件。 若要啟用或停用Asset Selector中的「集合」索引標籤，您可以透過下列方式使用`featureSet`屬性：

* **啟用集合標籤：**&#x200B;若要啟用集合標籤，您必須提供`collections`做為陣列的值。 預設會為所有使用者立即啟用「集合」索引標籤。 例如 `featureSet:["collections"]`
* **停用集合標籤：**&#x200B;若要停用集合標籤，您必須提供空陣列作為其值。 例如 `featureSet:[ ]`

>[!MORELIKETHIS]
>
>* [資產選擇器自訂](/help/assets/asset-selector-customization.md)
>* [整合資產選擇器與各種應用程式](/help/assets/integrate-asset-selector.md)
>* [資產選擇器屬性](/help/assets/asset-selector-properties.md)
