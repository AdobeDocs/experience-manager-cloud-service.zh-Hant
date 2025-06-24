---
title: Assets Prime
description: 進一步瞭解Assets Prime的主要方面，例如主要優點、使用者型別及其許可權。
feature: Asset Management
role: User, Admin
exl-id: 012f94c5-b1c3-4799-8eaf-af68d06c036f
source-git-commit: 47afd8f95eee2815f82c429e9800e1e533210a47
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 18%

---

# [!DNL Assets] as a Cloud Service Prime  {#assets-prime}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 與 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 與 Edge Delivery Services 整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>使用者介面可擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用 Dynamic Media Prime 與 Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

![AEM Assets Prime橫幅影像](/help/assets/assets/aem-assets-prime-package-banner.png)

Assets as a Cloud Service Prime包含輕量版DAM，可讓您執行各種關鍵功能，例如：

* **資產管理和資料庫服務**：這些工具可讓使用者能夠在集中存放庫中收錄、儲存、編目、控制、管理，及控管品牌的數位資產

* **搜尋、發現和共同作業**：此工具可讓使用者瀏覽、發現、共用，以及協作建立豐富客戶體驗所需的資產。

* **安全性和 Rights Management**：此工具可管理存取、授權、權限及安全性，以確保合規性、一致性與品牌完整性。

* **Creative Cloud 連線**：這些工具可讓行銷與創意團隊透過簡化的存取、評論、審查及註解來進行協作，以更新或完成數位資產。

* **Experience Cloud 連線**：這些工具可支援從其他 Experience Cloud 應用程式和服務，對數位資產進行原生存取。

* **沒有擴充性選項的分發入口網站體驗(Content Hub)**：工具可擴充對品牌已核准數位資產的存取權，以延伸利害關係人，以確保使用情況和品牌一致性。

* **整合**：與其他 Adobe 及非 Adobe 應用程式整合。

* **Dynamic Media (附加元件)**：此工具可用來轉換和傳遞影像、影片及其他新興內容，以大規模為任何裝置提供豐富的互動式多媒體體驗。

  >[!NOTE]
  >
  >Assets Prime也提供具有OpenAPI功能的Dynamic Media，讓您存取旋轉、裁切（僅限手動 — 無智慧型裁切）、翻轉、高度、寬度、品質、格式和自我調整視訊串流等基本影像修飾元。 請聯絡Adobe帳戶團隊以進一步瞭解。

1. [建立新程式](/help/journey-onboarding/create-program.md)。

然而，隨著您的DAM需求增長以及您需要更多功能，例如UI擴充性、API導向的自動化和自訂程式碼部署，您必須考慮升級至[Assets Ultimate](/help/assets/assets-ultimate-overview.md)。

本文提供啟用Assets as a Cloud Service Prime的端對端工作流程。

## 啟用Assets as a Cloud Service Prime{#enable-assets-prime}

使用Assets建立新程式時啟用Cloud Manager Prime。 執行以下步驟：

1. 以系統管理員身分登入Cloud Manager。 確保您在登入時選取正確的組織。

   >[!NOTE]
   >
   >確定您已新增至適當的Cloud Manager產品設定檔，以新增程式。 如需詳細資訊，請參閱[Cloud Manager中的角色型許可權](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)。

1. [建立新程式](/help/journey-onboarding/create-program.md)。

   建立新程式時，在&#x200B;**[!UICONTROL 解決方案和附加元件]**&#x200B;索引標籤中，選取&#x200B;**[!UICONTROL Assets Prime]**。 您也可以展開&#x200B;**[!UICONTROL Assets Prime]**，然後選取&#x200B;**[!UICONTROL Content Hub]**&#x200B;以啟用[Content Hub](/help/assets/product-overview.md)的資產發佈。

   ![AEM Assets Ultimate](assets/aem-assets-prime.png)


1. 按一下&#x200B;**[!UICONTROL 建立]**&#x200B;以建立程式。

1. 按一下程式卡，然後按一下&#x200B;**[!UICONTROL 新增環境]**。

1. 指定環境名稱、定義區域，然後按一下&#x200B;**[!UICONTROL 儲存]**&#x200B;以建立環境。

   ![將環境新增至Assets Prime](assets/aem-assets-prime-add-environment.png)

>[!NOTE]
>
>Assets Prime僅允許您建立生產環境。 成功建立生產環境後，「新增環境」選項就無法再使用。

Assets Prime現已為Experience Manager Assets as a Cloud Service啟用。

![AEM Assets Prime可供使用](assets/aem-assets-prime-setup-complete.png)

系統管理員會自動獲得AEM管理員的許可權，並會收到一封電子郵件，讓您導覽至Admin Console以管理產品設定檔。


Admin Console上的AEM as a Cloud Service執行個體包含下列產品設定檔：

* AEM 管理員

* AEM 使用者

* [AEM Assets 協作者使用者](#onboard-collaborator-users)

* [AEM Assets 進階使用者](#onboard-power-users)


![AEM Assets產品設定檔](assets/aem-assets-product-profiles.png)

您可以開始將使用者或使用者群組新增至AEM Assets Collaborator使用者和AEM Assets超級使用者產品設定檔。 如需詳細資訊，請參閱[加入AEM Assets Collaborator使用者](#onboard-collaborator-users)和[加入AEM Assets超級使用者](#onboard-power-users)。

如果您已啟用適用於Assets as a Cloud Service的Content Hub，則在Admin Console上的AEM Assets as a Cloud Service中會建立一個新執行個體，其尾碼為`delivery`：

![Content Hub的新執行個體](assets/new-instance-content-hub.png)

>[!NOTE]
>
>如果您在2024年8月14日之前布建Content Hub，則會建立以`contenthub`作為尾碼的新執行個體。

請注意，Content Hub的執行個體名稱中沒有`author`或`publish`。

按一下執行個體名稱以檢視`AEM Assets Limited Users` Content Hub產品設定檔。

![Content Hub產品設定檔](assets/content-hub-product-profile.png)

您可以開始將使用者或使用者群組新增至此產品設定檔，以便讓他們存取Content Hub。

>[!NOTE]
>
>如果您在2024年8月14日之前布建Content Hub，Content Hub產品設定檔會在`Limited Users`之後提及`contenthub`，而非`delivery`。

## 上線AEM Assets Collaborator使用者 {#onboard-collaborator-users}

AEM Assets Collaborator使用者可以透過貴組織在其他Assets產品和非Adobe應用程式中提供的Adobe整合來使用Experience Manager的資產，使用內建Adobe Express和Firefly來建立和編輯資產(利用專業設計的範本、品牌套件、Adobe Stock資產等)，以及使用AEM Assets Content Hub入口網站存取和利用貴組織核准的資產。

若要加入Collaborator使用者：

1. 按一下Experience Manager Assets產品清單中的AEM as a Cloud Service產品名稱，存取Admin Console產品設定檔。

1. 按一下AEM as a Cloud Service的生產製作例項：
   ![AEM as a Cloud Service的產品設定檔](assets/aem-cloud-service-instances.png)

1. 按一下Collaborators使用者產品設定檔，然後按一下&#x200B;**[!UICONTROL 新增使用者]**&#x200B;以將使用者新增至產品設定檔。
   ![使用者產品設定檔](assets/aem-assets-collaborator-user-permissions.png)

1. 按一下「**[!UICONTROL 儲存]**」以儲存變更。

您也可以存取及檢視指派給Collaborator使用者的服務，如下圖所示：

為Collaborator使用者提供![服務](assets/aem-assets-collaborator-users.png)

預設已啟用`Adobe Express`和`AEM Assets Collaborator Users`服務。 您可以視需求開啟或關閉切換按鈕，但Adobe建議使用針對產品設定檔啟用的預設服務。

## 入門AEM Assets超級使用者 {#onboard-power-users}

AEM Assets進階使用者可存取所有AEM Assets功能，包括管理資產、許可權、中繼資料以及有關數位資產的整體控管和自動化、透過您組織在其他Adobe和非Adobe應用程式中可用的Assets整合來使用Experience Manager中的資產、使用內建Adobe Express和Firefly利用專業設計的範本、品牌套件、Adobe Stock資產等建立和編輯資產，以及使用AEM Assets Content Hub入口網站存取和利用您組織中已核准的資產。

若要內建進階使用者：

1. 按一下Experience Manager Assets產品清單中的AEM as a Cloud Service產品名稱，存取Admin Console產品設定檔。

1. 按一下AEM as a Cloud Service的生產製作例項：
   ![AEM as a Cloud Service的產品設定檔](assets/aem-cloud-service-instances.png)

1. 按一下Power users產品設定檔，然後按一下&#x200B;**[!UICONTROL 新增使用者]**&#x200B;以將使用者新增至產品設定檔。
   ![使用者產品設定檔](assets/aem-assets-power-user-permissions.png)

1. 按一下「**[!UICONTROL 儲存]**」以儲存變更。

您也可以存取及檢視指派給超級使用者的服務，如下圖所示：

超級使用者的![服務](assets/aem-assets-power-users.png)

預設已啟用`Adobe Express`和`AEM Assets Power Users`服務。 您可以視需求開啟或關閉切換按鈕，但Adobe建議使用針對產品設定檔啟用的預設服務。
