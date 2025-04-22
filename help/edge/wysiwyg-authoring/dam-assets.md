---
title: 使用Edge Delivery Services透過DAM Assets發佈頁面
description: 瞭解確保您將頁面的DAM資產無縫發佈到Edge Delivery Services所需的設定。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 160f0474-a72d-4183-a2b2-2f8ba177605d
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 2%

---

# 使用Edge Delivery Services透過DAM Assets發佈頁面 {#dam-assets}

瞭解確保您將頁面的DAM資產無縫發佈到Edge Delivery Services所需的設定。

## 通用編輯器、DAM Assets和Edge Delivery {#overview}

針對通用編輯器編輯內容時，您當然可以從DAM中選取資產。 當您發佈內容至Edge Delivery Services時，也會發佈相關的DAM內容。

為確保這種順暢的行為，AEM和Edge Delivery Services必須能夠正確存取DAM才能發佈。 其中包括：

* [確定資產資料夾可以存取](#accessible)。
* [確定資產資料夾已指派適當的設定（視需要）](#configuration)。

## 確保Assets資料夾可供存取 {#accessible}

從AEM發佈頁面至Edge Delivery Services時，會使用[技術帳戶](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。 當您首次發佈使用通用編輯器建立的頁面時，Cloud Manager會自動在AEM中建立名稱為`<hash>@techacct.adobe.com`格式的使用者帳戶。

![技術帳戶](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

此技術帳戶必須具有所有DAM資料夾的存取許可權，才能發佈其內容。 您可以執行下列兩個動作中的一個:

* 請勿使用私人DAM資料夾。
* 授予技術帳戶使用者對DAM資料夾的存取權。

## 確保為Assets資料夾指派正確的設定 {#configuration}

通常可確保您的技術帳戶擁有您在DAM中資產的存取權，這足以將您的資產與頁面發佈到Edge Delivery Services。

但在其他兩種情況下需要額外設定：

* 如果您想要將具有非影像資產（例如PDF或視訊）的頁面發佈到Edge Delivery Services。
* 如果您想要將影像資產發佈至Edge Delivery Services，而不受頁面影響。

若要支援這兩個使用案例，必須將[設定](/help/implementing/developing/introduction/configurations.md)指派給DAM資料夾。

1. 登入您的AEM製作環境。
1. 在「**網站**」下，選取您要發佈資產的網站或是與資產關聯的網站。
1. 在工具列中點選或按一下&#x200B;**屬性**。
1. 在屬性視窗的&#x200B;**進階**&#x200B;索引標籤上，記下&#x200B;**雲端設定**&#x200B;欄位中的設定。
   * 當您以`/conf/<site-name>`格式建立您的網站時，會自動建立此專案。
1. 在屬性視窗中，點選或按一下「**取消**」，並導覽至&#x200B;**Assets** -> **檔案**，然後選取您的DAM資料夾。
1. 在工具列中點選或按一下&#x200B;**屬性**。
1. 在屬性視窗的&#x200B;**雲端服務**&#x200B;標籤的&#x200B;**雲端設定**&#x200B;欄位中，選取與您先前指出的相同設定。
1. 點選或按一下「**儲存並關閉**」。
