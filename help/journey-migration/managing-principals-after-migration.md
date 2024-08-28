---
title: 移轉後管理主體
description: 瞭解如何在IMS和AEM中設定使用者和群組
source-git-commit: 5b0dfb847a1769665899d6dd693a7946832fe7d1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# 移轉後管理主體 {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="移轉後管理主體"
>abstract="瞭解如何在IMS和AEM中設定使用者和群組"

本檔案說明客戶應該採取的高層級步驟，以便在IMS和AEM中設定使用者和群組，以便使用其AEM as a Cloud Service環境。

## 管理主參與者 {#managing-principals}

對於AEM as a Cloud Service，使用者和群組管理時主要必須使用Admin Console。  考慮移轉時，某些工作可在內容移轉發生之前執行。  基本上是這些主要任務群組中的

* 在IMS中建立使用者和群組
* 將使用者指派給IMS中的群組
* 指派IMS群組至AEM群組（如有必要）

前兩個可能會在內容移轉之前或之後執行。  這些步驟只會影響IMS中的使用者和群組，可能包括與外部IDP （例如Active Directory或LDAP）的整合。  在[使用Admin Console](/help/journey-migration/managing-principals.md)在IMS中管理主參與者(Principals)中說明這些步驟。

內容移轉至AEM as a Cloud Service環境後，第三個步驟即可執行。

### 正在移轉群組

在移轉的擷取階段中，如果群組需要符合已移轉內容的ACL或CUG原則，則會移轉群組。  如需詳細資訊，請參閱[群組移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)。

已移轉的群組(不是由Assets集合建立所建立的 — 請參閱下方的集合)會設定為IMS群組。  這表示在IMS中建立的相同名稱的任何群組(例如，透過Admin Console)都會連結至AEM中的群組，而屬於IMS群組成員的使用者也會成為AEM中的群組成員。  為了進行此連結，必須先在IMS中建立群組。  使用Admin Console在您的AEM執行個體中個別或大量建立群組，如[使用Admin Console管理IMS中的主體](/help/journey-migration/managing-principals.md)中所述。

使用AEM安全性UI指派IMS群組至本機AEM群組。  請參閱[建立和設定群組](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-groups#edit-a-group)。  雖然本檔案適用於AEM 6.5，但亦適用於將群組新增至AEM as a Cloud Service中的其他群組。

### IMS使用者

由於使用者並未移轉，因此必須在IMS中建立這些使用者，才能在AEM中使用。  有數種方法可以達成此目的，但重要的是，必須將建立的使用者指派給正確的IMS群組，以便使用者能有與先前AEM系統中相同的內容存取權。  可用於此作業的其中一項工具是Admin Console中的大量上傳功能；使用大量上傳程式可上傳使用者及其必須所屬的群組。  在執行此操作之前，必須先在IMS中建立群組，如上所述。

若要知道每個使用者應該屬於哪些群組，您可以使用使用者報告（請參閱[群組移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)）。  此報告會列出每個使用者應成為其成員的群組，此清單可包含在Admin Console大量上傳功能的輸入檔案中。

### 集合

建立Assets集合時，也會自動建立一些群組以管理對該集合的存取權。  如果在已移轉的集合中提及這些群組，則會移轉這些群組，但未將其設定為直接連結至IMS群組；在AEM中，這些群組仍為「本機群組」，且無法透過IMS管理。

由於這些群組不在IMS中，因此無法使用大量上傳工具將使用者建立為其直接成員。  也在AEM中的IMS使用者可以個別新增到這些群組，但大量執行此動作需要額外的步驟。  以下是可行方法之一：
* 在Admin Console/IMS中建立一個或多個新群組以存取集合，並為AEM設定它們。
* 以群組成員身分登入，以便在AEM中建立群組。
* 對於已移轉的集合，請使用Assets集合UI，將新群組新增為編輯器/擁有者/檢視者。
* 新增（或大量上傳）使用者至Admin Console中的新群組。
* 當使用者首次登入時，他們的IMS使用者將在AEM中建立，並且他們應該有權存取新群組，從而存取原始收集群組。

注意：若要大量指派使用者，必須使用上述步驟在IMS中建立使用者；已存在於IMS中的使用者無法透過大量上傳再次建立。


