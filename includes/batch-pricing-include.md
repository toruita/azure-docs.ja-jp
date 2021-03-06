## <a name="pricing"></a>価格

Azure Batch は無料サービスです。Batch アカウント自体には課金されません。 課金の対象となるのは、基になる Azure コンピューティング リソースのうち Batch ソリューションが使用する部分と、ワークロードの実行時に他のサービスが使用するリソースです。 たとえば、プール内のコンピューティング ノード (VM) や、タスクの入力または出力として Azure Storage に格納するデータに対して課金されます。 同様に、Batch の[アプリケーション パッケージ](../articles/batch/batch-application-packages.md)機能を使用している場合は、アプリケーション パッケージを格納するために使用する Azure Storage リソースが課金の対象となります。 詳細については、「[Batch の価格](https://azure.microsoft.com/pricing/details/batch/)」を参照してください。

[優先順位の低い VM](../articles/batch/batch-low-pri-vms.md) では、Batch ワークロードのコストを大幅に引き下げることができます。 優先順位の低い VM の価格については、「[Batch の価格](https://azure.microsoft.com/pricing/details/batch/)」を参照してください。 
