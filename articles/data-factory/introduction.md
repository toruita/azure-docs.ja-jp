---
title: "Azure Data Factory の概要 | Microsoft Docs"
description: "データの移動と変換を調整、自動化するクラウド データ統合サービスである Azure Data Factory について説明します。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/19/2017
ms.author: shlo
ms.translationtype: HT
ms.sourcegitcommit: c3a2462b4ce4e1410a670624bcbcec26fd51b811
ms.openlocfilehash: 09e514aee503b7cb045c81d8ddcb855ced9b072b
ms.contentlocale: ja-jp
ms.lasthandoff: 09/25/2017

---
# <a name="introduction-to-azure-data-factory"></a>Azure Data Factory の概要 
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [バージョン 1 - 一般公開](v1/data-factory-introduction.md)
> * [バージョン 2 - プレビュー](introduction.md)

ビッグ データの世界では、未整理の生データは、多くの場合、リレーショナル、非リレーショナル、その他のストレージ システム内に格納されます。 ただし、生データ自体には、アナリストや、データ サイエンティスト、管理職意思決定者に有用な分析を提供するのに必要となる正しいコンテキストや意味はありません。 必要なのは、データ制御と運用化の処理によって、膨大な量の生データを実用的なビジネス分析へと転換できるサービスです。 Azure Data Factory は、ETL (抽出 - 変換 - 読み込み)、ELT (抽出 - 読み込み - 変換)、データ統合という複雑なハイブリッド プロジェクト用に構築された、管理クラウド サービスです。

たとえば、クラウド内のゲームで生成される、数ペタバイト規模のゲーム ログを収集するゲーム会社があるとします。 アップセルやクロス セルの商機を見極め、魅力的な新機能を開発して、ビジネスの成長を後押しし、カスタマー エクスペリエンスを高めるために、その会社がこれらのログを分析して顧客の好みや内訳、利用行動などを正確に把握したいと考えているとしましょう。

これらのログを分析するには、顧客情報やゲーム情報、マーケティング キャンペーン情報など、オンプレミスのデータ ストアにある参照データを使用する必要があります。 この会社は、オンプレミスのデータ ストアにあるこれらのデータを、クラウドのデータ ストアにある追加のログ データと統合して活用しようと考えています。 状況を正確に把握するために、クラウドの Spark クラスターを使用して統合したデータを処理し (HDInsight)、最終的には、変換したデータを Azure SQL Data Warehouse などのクラウドのデータ ウェアハウスに公開して、これらのデータに基づくレポートを簡単に作成できるようにすることを希望しています。 このワークフローは、日単位のスケジュールに従って自動化、監視、管理されます。また、BLOB ストア コンテナーにファイルが配置されたときに実行されます。

Azure Data Factory は、このようなデータ シナリオを解決するプラットフォームです。 **そのクラウドベースのデータ統合サービスを通じて、データの移動と変換を制御して自動化するデータ主導型のワークフローをクラウドに作成**することができます。 Azure Data Factory を使えば、データ主導型のワークフロー (パイプライン) を作成し、スケジューリングできます。具体的には、各種データ ストアからデータを取り込む、そのデータを各種コンピューティング サービス (Azure HDInsight Hadoop、Spark、Azure Data Lake Analytics、Azure Machine Learning など) で処理/変換する、データ ストア (Azure SQL Data Warehouse など) に出力データを公開して、それを利用するビジネス インテリジェンス (BI) アプリケーションに提供するという一連の処理を行えるワークフローです。 Azure Data Factory を使うと、最終的に、生データを意味のあるデータ ストアとデータ レイクに整理し、より的確な意思決定に活用できます。

![Data Factory の上位ビュー](media/introduction/big-picture.png)

> [!NOTE]
> この記事は、現在プレビュー段階にある Data Factory のバージョン 2 に適用されます。 一般公開 (GA) されている Data Factory サービスのバージョン 1 を使用している場合は、[Data Factory バージョン 1 の概要](v1/data-factory-introduction.md)に関する記事をご覧ください。

## <a name="how-does-it-work"></a>それはどのように機能しますか?
通常、Azure Data Factory のパイプライン (データ主導型のワークフロー) では次の 4 つのステップが実行されます。

![データ主導型ワークフローの 4 つのステップ](media/introduction/four-steps-of-a-workflow.png)

### <a name="connect-and-collect"></a>接続と収集

企業は、さまざまな種類のデータをさまざまなソースに管理しています。ソースには、オンプレミスのソースやクラウド内のソース、構造化されたもの、構造化されていないもの、半構造化されたものなどがあり、そのデータの受信間隔も速度もまちまちです。 情報生成システム構築の最初のステップは、SaaS (サービスとしてのソフトウェア) サービス、データベース、ファイル共有、FTP Web サービスなど、必要なすべてのデータ ソースと処理の機能に接続し、必要に応じて、後続の処理を行う 1 か所にデータを移動することです。

Data Factory を使用していない企業では、カスタムのデータ移動コンポーネントを構築するか、これらのデータ ソースと処理を統合するカスタム サービスを作成しなければなりません。 このような作業にはコストがかかり、システムの統合や保守が容易ではありません。エンタープライズ クラスの監視やアラートが欠け、完全に管理されたサービスが提供できるような制御機能を用意できないことも少なくありません。

Data Factory を使用すれば、データ パイプラインの[コピー アクティビティ](copy-activity-overview.md)で、オンプレミスとクラウドの両方のソース データ ストアからクラウド内の一元化されたデータ ストアにデータを移動し、詳しく分析することができます。 たとえば、Azure Data Lake Store でデータを収集し、後で Azure Data Lake Analytics コンピューティング サービスを使用してデータを変換することができます。 または、Azure BLOB ストレージでデータを収集し、後で Azure HDInsight Hadoop クラスターを使用してデータを変換することもできます。

### <a name="transform-and-enrich"></a>変換と強化
クラウド上の一元的なデータ ストアにデータが集まったら、HDInsight Hadoop、Spark、Data Lake Analytics、Machine Learning などのコンピューティング サービスを使って、その収集されたデータを処理または変換します。 保守しやすい管理されたスケジュールで確実に変換データを生成し、信頼性の高いデータを運用環境に提供する必要があります。

### <a name="publish"></a>[発行]
生データが変換されてビジネスに即応して利用できる形態になったので、このデータを、ビジネス ユーザーがビジネス インテリジェンス ツールから参照できる Azure Data Warehouse、Azure SQL DB、Azure CosmosDB、またはその他の分析エンジンに読み込みます。

### <a name="monitor"></a>監視
データ統合パイプラインを正常に構築してデプロイし、変換したデータからビジネス価値を生み出せるようになったなら、スケジュール化したアクティビティとパイプラインを監視して、成功率と失敗率を確認することができます。 Azure Data Factory には、Azure Monitor、API、PowerShell、OMS、Azure Portal の正常性パネルを利用してパイプラインを監視する、ビルトイン サポートが用意されています。

## <a name="whats-different-in-version-2"></a>バージョン 2 の変更点
Azure Data Factory バージョン 2 は、元の Azure Data Factory のデータ移動と変換サービスを基に構築されていますが、対応できるクラウドファースト データ統合シナリオの幅が広がりました。 Azure Data Factory V2 では、次の機能が提供されます。

- フローとスケールの制御
- Azure での SSIS パッケージのデプロイと実行

バージョン 1 のリリース以降、お客様はクラウド、オンプレミス、クラウド VM 内でデータ移動と処理の両方を実行する、複雑なハイブリッド データ統合シナリオを設計することを必要としていることがわかりました。 これらの要件を満たすには、セキュリティ保護された VNET 環境内でデータ転送と処理を行い、オンデマンドの処理能力を使用してスケールアウトする必要があります。

データ パイプラインがビジネス分析戦略の重要な要素になっているため、これらの重要なデータ活動には、データの増分読み込みやイベント トリガー型の実行をサポートする柔軟なスケジューリング機能が必要となっています。 最後の点として、このようなオーケストレーションが一層複雑になるにつれて、分岐処理、ループ処理、条件処理などの一般的なワークフロー パラダイムをサポートするサービスも一層必要になります。

バージョン 2 を使うと、既存の SQL Server Integration Services (SSIS) パッケージをクラウドに移行し、SSIS をリフトアンドシフトして、新しい “統合ランタイム” (IR) 機能を利用して ADF 内で管理される Azure のサービスとすることもできます。 バージョン 2 で SSIS IR をスピンアップすると、クラウド内で SSIS パッケージを実行、管理、監視、ビルドする機能が得られます。

### <a name="control-flow-and-scale"></a>フローとスケールの制御 
最新のデータ ウェアハウスの多様な統合フローとパターンをサポートするため、Data Factory では、時系列データと関連付けられていない新しい柔軟なデータ パイプライン モデルが利用できます。 このリリースでは、データ パイプラインの制御フロー内の条件や分岐をモデル化したり、これらのフロー内またはフロー間でパラメーターを明示的に渡したりすることができます。

データ統合に必要な任意のフロー スタイルをモデル化でき、それをオンデマンドで、またはスケジュール化してディスパッチできます。 これまで実現できなかったもので、今回実現できるようになった一般的なフローのいくつかを次に紹介します。   

- 制御フロー:
    - パイプライン内のシーケンスでのアクティビティの連鎖
    - パイプライン内のアクティビティの分岐
    - parameters
        - パイプライン レベルでパラメーターを定義でき、オンデマンドで、あるいはトリガーからパイプラインを呼び出す際に引数を渡すことができます
        - アクティビティは、パイプラインに渡される引数を使用できます。
    - カスタム状態の受け渡し
        - 状態などのアクティビティ出力は、パイプライン内の後続のアクティビティで使用できます。
    - ループ コンテナー
        - For-each 
- トリガー ベースのフロー
    - パイプラインは、オンデマンドで、または実時間に合わせてトリガーできます。
- 差分フロー
    - 差分コピー用にパラメーターを使用したり最大値を定義したりして、オンプレミスやクラウドのリレーショナル ストアからディメンションまたは参照テーブルを移動し、データをレイクに読み込みます。 

詳細については、「[チュートリアル: 制御フロー](tutorial-control-flow.md)」をご覧ください。

### <a name="deploy-ssis-packages-to-azure"></a>SSIS パッケージを Azure にデプロイする 
SSIS ワークロードを移動する場合は、データ ファクトリ バージョン 2 を作成し、Azure-SSIS 統合ランタイム (IR) をプロビジョニングできます。 Azure-SSIS IR は、クラウドでの SSIS パッケージ実行専用の、Azure VM (ノード) の完全に管理されたクラスターです。 詳しい手順については、「チュートリアル: [SSIS パッケージを Azure にデプロイする](tutorial-deploy-ssis-packages-azure.md)」を参照してください。 
 

## <a name="rich-cross-platform-sdks"></a>豊富なクロス プラットフォーム SDK
プログラマティック インターフェイスを必要とする詳しい知識のあるユーザー向けに、バージョン 2 では、使い慣れた IDE を使用してパイプラインを作成、管理、監視するために使用できる豊富な SDK のセットが用意されています。

- .NET SDK
- PowerShell
- Python SDK

REST API を使用してデータ ファクトリを作成することもできます。 

## <a name="load-the-data-into-a-lake"></a>データをレイクに読み込む
Data Factory には、30 以上のコネクタが用意されており、ハイブリッドの異種環境から、Azure にデータを読み込むことができます。  内部テストでの最新のパフォーマンス結果とチューニングに関する推奨事項については、「[パフォーマンスとチューニングのガイド](copy-activity-performance.md)」をご覧ください。 最近ではさらに、プライベート ネットワーク環境にインストールされるセルフホステッドの統合ランタイムで高可用性とスケーラビリティが利用できるようになりました。これにより、可用性とスケーラビリティの向上という、階層 1 の大規模エンタープライズのお客様の要件に対応します。

## <a name="top-level-concepts-in-version-2"></a>バージョン 2 のトップレベルの概念
1 つの Azure サブスクリプションで 1 つ以上の Azure Data Factory インスタンス (データ ファクトリ) を利用できます。 Azure Data Factory は、4 つの主要コンポーネントで構成されたプラットフォームです。このプラットフォームを基盤とし、データ移動とデータ変換のステップを含んだデータ主導型のワークフローを作成することができます。

### <a name="pipeline"></a>パイプライン
データ ファクトリには、1 つまたは複数のパイプラインを設定できます。 パイプラインは、1 つの作業単位を実行するための複数のアクティビティから成る論理的なグループです。 パイプライン内のアクティビティがまとまって 1 つのタスクを実行します。 たとえば、パイプラインに Azure BLOB からデータを取り込むアクティビティのグループを含め、HDInsight クラスターで Hive クエリを実行してデータをパーティション分割することができます。 パイプラインのメリットは、アクティビティを個別にではなく、セットとして管理できることです。 パイプライン内のアクティビティは、連鎖して順次処理することも、独立して並行処理することもできます。

### <a name="activity"></a>アクティビティ
アクティビティは、パイプライン内の処理ステップを表します。 たとえば、コピー アクティビティを使用して、データ ストア間でデータをコピーできます。 同様に、Azure HDInsight クラスターに対して Hive クエリを実行する Hive アクティビティを使用して、データを変換または分析できます。 Data Factory では、データ移動アクティビティ、データ変換アクティビティ、制御アクティビティの 3 種類のアクティビティがサポートされています。

### <a name="datasets"></a>データセット
データセットは、データ ストア内のデータ構造を表しています。アクティビティ内でデータを入力または出力として使用したい場合は、そのデータをポイントまたは参照するだけで済みます。 

### <a name="linked-services"></a>リンクされたサービス
リンクされたサービスは、接続文字列によく似ており、Data Factory が外部リソースに接続するために必要な接続情報を定義します。 リンクされたサービスはデータ ソースへの接続を定義するもので、データセットはデータの構造を表すもの、と捉えることができます。 たとえば、Azure Storage アカウントに接続するための接続文字列は、Azure Storage のリンクされたサービスで指定します。 また、データを格納する BLOB コンテナーやフォルダーは、Azure BLOB データセットで指定します。

Data Factory ではリンクされたサービスは 2 つの目的に使用されます。

- オンプレミスの SQL Server、Oracle データベース、ファイル共有、Azure Blob Storage アカウント、その他の **データ ストア** を表すため。 サポートされるデータ ストアの一覧については、「[コピー アクティビティ](copy-activity-overview.md)」を参照してください。
- アクティビティの実行をホストできる **コンピューティング リソース** を表すため。 たとえば、HDInsightHive アクティビティは HDInsight Hadoop クラスターで実行されます。 変換アクティビティとサポートされているコンピューティング環境の一覧については、「[データの変換](transform-data.md)」を参照してください。

### <a name="triggers"></a>トリガー
トリガーは、パイプラインの実行をいつ開始する必要があるかを決定する処理単位を表します。 さまざまな種類のイベントに合わせて、さまざまな種類のトリガーがあります。プレビュー用には、実時間のスケジューラ トリガーがサポートされています。 


### <a name="pipeline-runs"></a>パイプライン実行
パイプライン実行は、パイプラインを実行するインスタンスです。 パイプライン実行は、通常、パイプラインで定義されたパラメーターに引数を渡してインスタンス化されます。 引数は、手動で渡すか、トリガー定義内で渡すことができます。

### <a name="parameters"></a>parameters
パラメーターは、読み取り専用の構成のキーと値のペアです。  パラメーターはパイプラインで定義され、定義済みパラメーターの引数は、実行時に、トリガーが作成した実行コンテキストか、手動で実行されるパイプラインから渡されます。 パイプライン内のアクティビティは、パラメーターの値を使用します。
データセットとは、厳密に型指定されたパラメーターと、再利用または参照可能なエンティティのことです。 アクティビティは、データセットを参照でき、データセットの定義で定義されたプロパティを使用できます。

リンクされたサービスも厳密に型指定されたパラメーターであり、これにはデータ ストアかコンピューティング環境のいずれかへの接続情報が入ります。 これは再利用可能または参照可能なエンティティでもあります。

### <a name="control-flow"></a>制御フロー
パイプライン アクティビティのオーケストレーションです。これには、シーケンスに従うアクティビティの連鎖、分岐、パイプライン レベルで定義できるパラメーター、オンデマンドかトリガーからパイプラインが呼び出される際に渡される引数が含まれます。 さらに、カスタム状態の受け渡しや、ループ コンテナー、つまり For-each 反復子も含まれます。


Data Factory の概念について詳しくは、次の記事をご覧ください。

- [データセットとリンクされたサービス](concepts-datasets-linked-services.md)
- [パイプラインとアクティビティ](concepts-pipelines-activities.md)
- [統合ランタイム](concepts-integration-runtime.md)

## <a name="supported-regions"></a>サポートされているリージョン:

現時点では、米国東部と米国東部 2 のリージョンでデータ ファクトリを作成できます。 ただし、データ ファクトリは、他の Azure リージョン内のデータ ストアやコンピューティング サービスにアクセスし、データ ストア間でデータを移動したり、コンピューティング サービスを使用してデータを処理したりできます。

Azure Data Factory 自体は、データを保存しません。 Azure Data Factory を使用すると、データ主導型のワークフローを作成し、サポートされているデータ ストア間でのデータ移動と、他のリージョンまたはオンプレミスの環境にあるコンピューティング サービスを使用したデータ処理を調整できます。 また、プログラムと UI の両方のメカニズムを使用して、ワークフローを監視および管理することもできます。

Data Factory を利用できるリージョンが米国東部と米国東部 2 のリージョンのみであっても、Data Factory 内でデータ移動を実行するサービスは、いくつかのリージョンでグローバルに利用できます。 データ ストアがファイアウォールの内側にある場合は、オンプレミスの環境にインストールされている Data Management Gateway がデータを移動します。

たとえば、Azure HDInsight クラスターや Azure Machine Learning などのコンピューティング環境が西ヨーロッパ リージョン以外で稼働しているものと想定します。 北ヨーロッパに Azure Data Factory インスタンスを作成して利用すると、西ヨーロッパのコンピューティング環境でジョブのスケジュール設定にそのインスタンスを使用することができます。 Data Factory がコンピューティング環境でジョブをトリガーするまでに数ミリ秒かかりますが、コンピューティング環境でのジョブの実行時間は変わりません。

## <a name="next-steps"></a>次のステップ
次のクイック スタートの手順 ([PowerShell](quickstart-create-data-factory-powershell.md)、[.NET](quickstart-create-data-factory-dot-net.md)、[Python](quickstart-create-data-factory-python.md)、[REST API](quickstart-create-data-factory-rest-api.md)、Azure Portal) に従って、データ ファクトリを作成する方法をご確認ください。 

