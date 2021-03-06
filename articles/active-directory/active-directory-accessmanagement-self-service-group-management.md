---
title: "アプリケーション アクセス管理のセルフ サービス化に必要な Azure Active Directory の設定 | Microsoft Docs"
description: "Azure Active Directory にセキュリティ グループまたは Office 365 グループを作成して管理したり、セキュリティ グループまたは Office 365 グループのメンバーシップを要求したりすることができます。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 904d5c70-c34a-46c4-a9a7-d1efecf4821c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/07/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
ms.translationtype: HT
ms.sourcegitcommit: 12c20264b14a477643a4bbc1469a8d1c0941c6e6
ms.openlocfilehash: 7a7370eb076ba8602a58a260a14bb863c55bc803
ms.contentlocale: ja-jp
ms.lasthandoff: 09/07/2017

---
# <a name="set-up-azure-active-directory-for-self-service-group-management"></a>セルフサービス グループ管理に必要な Azure Active Directory の設定
Azure Active Directory (Azure AD) では、管理下のユーザーが自分でセキュリティ グループまたは Office 365 グループを作成して管理することができます。 ユーザーはセキュリティ グループまたは Office 365 グループのメンバーシップを要求することもできます。要求されたメンバーシップは、グループの所有者が承認または拒否できます。 グループの業務上の趣旨を理解している人物に日常的なメンバーシップ管理を委任することができます。 セルフサービスによるグループ管理機能を使用できるのはセキュリティ グループと Office 365 グループだけであり、メールを有効にしたセキュリティ グループまたは配布リストでは使用できません。

セルフサービス型のグループ管理には現在、グループ管理の委任とセルフサービス化という基本的な 2 つの使い方が考えられます。

* **グループ管理の委任** 管理者が、社内で利用している SaaS アプリケーションへのアクセスを管理しているとします。 それらのアクセス権を管理する負担が大きくなってきたことから、この管理者はビジネス オーナーに依頼して新しいグループを作成してもらいます。 管理者はアプリケーションへのアクセス権を新しいグループに割り当て、既にアプリケーションにアクセスしているすべてのユーザーをそのグループに追加します。 これ以降はビジネス オーナーがユーザーをさらに追加できます。追加されたユーザーはアプリケーションへと自動的にプロビジョニングされます。 ビジネス オーナーは、管理者によるユーザーのアクセス管理が行われるまで待つ必要がありません。 管理者が同じ権限を別のビジネス グループのマネージャーに付与した場合、その人物も自分のユーザーのアクセス管理ができるようになります。 ビジネス オーナーもマネージャーも、互いのユーザーを表示または管理することはできません。 管理者は依然として、そのアプリケーションへのアクセス権を持ったすべてのユーザーを表示でき、必要に応じてアクセス権をブロックすることができます。
* **グループ管理のセルフサービス化** たとえば、2 人のユーザーが別々に SharePoint Online サイトを設定しているとします。 この 2 人のユーザーは、自分のサイトへのアクセス権を互いのチームに付与しようとしています。 これを実現するには、Azure AD に 1 つのグループを作成し、SharePoint Online で両者がそのグループを選択して、それぞれのサイトへのアクセス権を付与します。 アクセス権を必要とする人がいれば、その人物がアクセス パネルからアクセス権を要求します。承認が下りればその人物は自動的に、両方の SharePoint Online サイトにアクセスできるようになります。 後日、2 人のうち一方が、サイトにアクセスしているすべてのユーザーに、特定の SaaS アプリケーションへのアクセス権も付与することに決めたとします。 SaaS アプリケーションの管理者は、アプリケーションによる SharePoint Online サイトへのアクセス権を追加することができます。 それ以後は、要求が承認されると、2 つの SharePoint Online サイトへのアクセス権に加え、この SaaS アプリケーションへのアクセス権も付与されるようになります。

## <a name="make-a-group-available-for-user-self-service"></a>グループをユーザーのセルフ サービスに使用できるようにする
1. ディレクトリのグローバル管理者のアカウントで [Azure AD 管理センター](https://aad.portal.azure.com)にサインインします。
2. **[ユーザーとグループ]** を選択し、**[グループ設定]** を選択します。
3. **[セルフサービスによるグループ管理が有効になりました]** を **[はい]** に設定します。
4. **[ユーザーはセキュリティ グループを作成できます]** または **[ユーザーは Office 365 グループを作成できます]** を **[はい]** に設定します。
  * これらの設定を有効にすると、自分のディレクトリ内のすべてのユーザーが、新しいセキュリティ グループを作成したりそれらのグループにメンバーを追加したりできるようになります。 これらの新しいグループは、他のすべてのユーザーのアクセス パネルにも表示されるようになります。 グループのポリシー設定で許可されている場合、他のユーザーはこれらのグループへの参加要求を作成できます。 
  * これらの設定が無効になっていると、ユーザーはグループを作成できず、所有している既存のグループを変更することもできません。 ただし、それらのグループのメンバーシップの管理と、他のユーザーからのグループへの参加要求の承認は、引き続き行うことができます。

ユーザーによるセルフサービスのグループ管理は、**[セキュリティ グループを管理できるユーザー]** と **[Office 365 グループを管理できるユーザー]** を使用することで、さらに細かくアクセス制御を行うこともできます。 **[ユーザーはグループを作成できます]** を有効にすると、自分のテナント内のすべてのユーザーが、新しいグループを作成したりそれらのグループにメンバーを追加したりできるようになります。 それらを **[一部]** に設定すると、グループの管理機能を一部のユーザー グループに限定できます。 このスイッチを **[一部]** に設定した場合、ユーザーが新しいグループを作成してそのグループにメンバーを追加できるようにするには、そのユーザーを SSGMSecurityGroupsUsers グループに追加する必要があります。 **[セキュリティ グループのためのセルフサービスを使用できるユーザー]** と **[Office 365 グループを管理できるユーザー]** を **[すべて]** に設定すると、自分のテナント内のすべてのユーザーが新しいグループを作成できます。

**[セキュリティ グループを管理できるグループ]** または **[Office 365 グループを管理できるグループ]** を使用して、特定のグループを 1 つ指定し、そのメンバーにセルフサービス機能の利用を許可することもできます。

## <a name="next-steps"></a>次のステップ
次の記事は、Azure Active Directory に関する追加情報を示します。

* [Azure Active Directory のグループによるリソースへのアクセス管理](active-directory-manage-groups.md)
* [グループの設定を構成するための Azure Active Directory コマンドレット](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)
* [Azure Active Directory とは](active-directory-whatis.md)
* [オンプレミス ID と Azure Active Directory の統合](active-directory-aadconnect.md)

