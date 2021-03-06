---
title: "Windows 上での Azure CLI の使用 | Microsoft Docs"
description: "Windows 上での Azure CLI の使用"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.translationtype: HT
ms.sourcegitcommit: 8f9234fe1f33625685b66e1d0e0024469f54f95c
ms.openlocfilehash: 0ac4aa10db43fb84119ab97cf78b2d5592cfd277
ms.contentlocale: ja-jp
ms.lasthandoff: 09/20/2017

---

# <a name="using-the-azure-cli-on-windows"></a>Windows 上での Azure CLI の使用

Azure コマンド ライン インターフェイス (CLI) は、Azure リソースの作成と管理のためのコマンドラインとスクリプト環境を提供します。 Azure CLI は、macOS、Linux、および Windows オペレーティング システムで使用できます。 これらのオペレーティング システムにわたって CLI コマンドは同じですが、オペレーティング システム固有のスクリプト構文は異なることがあります。

このドキュメントでは、Windows 上で Azure CLI をインストールおよび実行する方法、およびそれぞれの構文上の考慮事項について詳細に説明します。 詳細な Azure CLI のドキュメントについては、[Azure CLI のドキュメント]( https://docs.microsoft.com/en-us/cli/azure/overview)を参照してください。

## <a name="windows-subsystem-for-linux"></a>Windows Subsystem for Linux

Windows Subsystem for Linux (WSL) は、Windows 10 Anniversary 以降のエディション上で Ubuntu Linux 環境を提供します。 有効な場合、WSL は Azure CLI スクリプトの作成および実行に使用できるネイティブ Bash エクスペリエンスを提供します。 WSL がネイティブ Bash エクスペリエンスを提供するため、Azure CLI スクリプトを macOS、Linux、Windows の間で変更なしに共有できます。

WSL 内で Azure CLI を使用するには、次の手順を実行します。

|タスク | このサンプルについての指示 |
|---|---|
| WSL を有効にする | [WSL ドキュメントをインストールする](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| Azure CLI のインストール |[WSL/Ubuntu 14.04 上での CLI のインストール](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a>PowerShell

Azure CLI は、Windows でネイティブに実行できます。 この構成では、Windows オペレーティング システム上に Azure CLI パッケージがインストールされ、PowerShell からコマンドを実行できます。 この構成では、任意のサポートされているバージョンの Windows 上で Azure CLI コマンドおよびスクリプトを実行できますが、プラットフォーム固有のスクリプト構文が必要です。 このため、スクリプトを macOS、Linux、Windows の間で変更なしに共有できるとは限りません。

Windows 上で Azure CLI を使用するには、[Windows 上での CLI のインストール](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows)に関する記事の手順を使用してパッケージをインストールします。

## <a name="docker-image"></a>Docker イメージ

Docker for Windows を使用する場合は、Azure CLI を含む Docker イメージで起動できます。 このイメージは、Linux に基づいており、ネイティブ Bash エクスペリエンスが含まれています。  Docker for Windows と Azure CLI イメージを使用している場合は、macOS、Linux、Windows の間で共有されるスクリプト。 

Docker for Windows 上で Azure CLI を使用するには、Docker for Windows が実行されていることを確認し、次のコマンドを実行します。

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

完了すると、Azure CLI ツールが事前に読み込まれた Bash セッションが開始されます。

## <a name="next-steps"></a>次のステップ

[Azure 仮想マシン用の CLI サンプル](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Azure Web Apps 用の CLI サンプル](../../app-service/app-service-cli-samples.md)

[Azure SQL 用の CLI サンプル](../../sql-database/sql-database-cli-samples.md)

