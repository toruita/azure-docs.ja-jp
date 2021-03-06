---
title: "Service Fabric CLI スクリプト サンプル - クラスター上のアプリケーションを更新する"
description: "Service Fabric CLI スクリプト サンプル - アプリケーションを新しいバージョンで更新する この例では、デプロイされているアプリケーションも新しいビットでアップグレードされます。"
services: service-fabric
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 09/19/2017
ms.author: adegeo
ms.custom: 
ms.translationtype: HT
ms.sourcegitcommit: c3a2462b4ce4e1410a670624bcbcec26fd51b811
ms.openlocfilehash: f91ea8c2f8c6e9a6ce38cf72be2c61d9e5218b23
ms.contentlocale: ja-jp
ms.lasthandoff: 09/25/2017

---

# <a name="add-an-application-certificate-to-a-service-fabric-cluster"></a>アプリケーション証明書の Service Fabric クラスターへの追加

このサンプル スクリプトは、既存のアプリケーションの新しいバージョンをアップロードしてから、デプロイされているアプリケーションを新しいビットでアップグレードします。

[!INCLUDE [links to azure cli and service fabric cli](../../../includes/service-fabric-sfctl.md)]

## <a name="sample-script"></a>サンプル スクリプト

[!code-sh[main](../../../cli_scripts/service-fabric/upgrade-application/upgrade-application.sh "Upload and update an application on a Service Fabric cluster")]

## <a name="next-steps"></a>次のステップ

詳細については、[Service Fabric CLI ドキュメント](../service-fabric-cli.md)をご覧ください。

その他の Azure Service Fabric 用 Service Fabric CLI サンプルは、[Service Fabric CLI のサンプル](../samples-cli.md)のページにあります。

