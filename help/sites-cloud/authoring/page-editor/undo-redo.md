---
title: 還原和重做限制
description: 瞭解AEM頁面編輯器中還原和重做選項的限制。
exl-id: 87773f47-5116-4966-9ba4-5deedb7c4fa6
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 1%

---

# 還原和重做限制 {#undo-redo}

AEM會儲存您執行動作的歷史記錄，以及執行動作的順序，如此一來，您就可以依照執行動作的順序復原多個動作，並視需要重做這些動作，以重新套用一或多個動作。

如果選取了內容頁面上的元素（例如文字元件），則復原和重做命令會套用至選取的專案。

復原和重做命令的行為與其他軟體中的類似。 在您決定內容時，請使用命令來還原網頁的最近狀態。 例如，如果您將文欄位落移至頁面上的不同位置，您可以使用復原指令將段落移回。 如果之後您認為前一個位置較好，請使用重做指令「復原復原」。

例如，您可以：

* 只要您使用復原後尚未進行頁面編輯，就可以重做動作。
* 復原最多20個編輯動作（預設設定）。
* 也使用[鍵盤快速鍵](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)進行還原和重做。

您可以對下列型別的頁面變更使用還原和重做：

* 新增、編輯、移除和移動段落
* 就地編輯段落內容
* 在頁面中複製、剪下和貼上專案

>[!NOTE]
>
>* 需要特殊許可權才能復原和重做檔案與影像的變更。
>* 檔案和影像的變更記錄至少會持續10小時。 然而，在這段時間之後，變更的復原則無法保證。 您的管理員可以變更十小時的預設時間。
>* 您的系統管理員可以根據您執行個體的需求，設定「復原/重做」功能的各個方面。
