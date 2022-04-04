# Pub/Sub and Network Integration

## Background

Executives at Best For You Organics Company (BFYOC) have taken notice of the success of the recently implemented solution to enable Point of Sale (POS) terminals to send sales data to the cloud, and they want to leverage this new data even more. They have started a pilot program to update BFYOC POS terminals to randomly capture a PDF version of the sales receipt in addition to the detailed transaction data.  They would like to save all the transaction data to their private storage in the cloud for data archival and future analysis.  Additionally, executives are concerned about the potential for fraudulent transactions, and would like to add additional rigor for transactions which exceed $100.

After learning of the executive's high-level requirements, the cloud architecture team has decided to implement a publisher/subscriber (pub/sub) messaging technique to capture POS sales data which has a receipt.  They feel they can use a message filtering pattern to identify sales data which has a total transaction cost greater than $100.  Additionally, because BFYOC is highly protective of customer and sales data, they want to ensure all the data is safely stored within an Azure storage account which is accessible only from services within, or integrated with, BFYOC's virtual network in Azure. The files stored in blob storage are able to be used by other systems within BFYOC's virtual network, such as data analysis and fraud detection processes.

BFYOC has an existing virtual network containing at least two subnets.  They also have an Azure storage account configured to use Azure Virtual Network service endpoints to restrict access from any source except the two subnets within the virtual network.  An Azure Virtual Machine is available to be used as a jumpbox for viewing data from services within the virtual network.

![Virtual Network with subnets and blob storage service endpoints](https://serverlessoh.azureedge.net/public/pubsub-and-vnet-integration-virtual-network-diagram.png)

## Challenge

Your first challenge is to modify the Azure Function used in the previous challenge to send the specified receipt information to a pub/sub messaging system, but only if there is a receipt.  Using the POS data sent via the Event Hub from the previous challenge, you can create a new JSON document with a structure similar to the example below that will be sent to your pub/sub messaging system.

```JSON
{
    "totalItems": 8,
    "totalCost": 123.40,
    "salesNumber": "0c423398-3c7c-0682-7519-4701c445ed7a",
    "salesDate": "09/11/2019 06:04:43",
    "storeLocation": "00d8ea6f-935c-2cca-9bbc-f56b5a091621",
    "receiptUrl": "https://serverlessohsales.blob.core.windows.net/TheReceipt.pdf"
}
```

Next, you will need to create a process(es) which is able to filter based on the total cost in each message, and accomplish the following tasks:

1. If the total cost is greater than or equal to $100:

    * retrieve the PDF file of the receipt using the ```receiptUrl``` value
    * base64 encode the PDF
    * create a JSON object which includes the receipt data, along with the base64 encoded version of the receipt
    * save the JSON object with a unique name to the "receipts-high-value" container within the provided Azure Storage account (accessible only from the virtual network)

    The format for the saved data should be as follows:

    ```JSON
    {
        "Store": "00d8ea6f-935c-2cca-9bbc-f56b5a091621",
        "SalesNumber": "0c423398-3c7c-0682-7519-4701c445ed7a",
        "TotalCost": 123.40,
        "Items": 8,
        "SalesDate": "09/11/2019 06:04:43",
        "ReceiptImage":"V2VsY29tZSB0byBTZXJ2ZXJsZXNzIE9wZW5IYWNrIQ=="
    }
    ```

2. If the total cost is less than $100:

    * create a JSON object which includes the receipt data
    * save the JSON object with a unique name to the "receipts" container within the provided Azure Storage account (accessible only from the provided virtual network)

    The format for the saved data should be as follows:

    ```JSON
    {
        "Store": "00d8ea6f-935c-2cca-9bbc-f56b5a091621",
        "SalesNumber": "0c423398-3c7c-0682-7519-4701c445ed7a",
        "TotalCost": 6.58,
        "Items": 1,
        "SalesDate": "09/02/2019 10:36:17"
    }
    ```

When determining how to perform the filtering of messages, it is important to remember that BFYOC has built a distributed system which may, over time, require additional processing streams.  The cloud architecture team wants to ensure the solution avoids filtering "in code" by leveraging features of the selected messaging system.

>HINT: All receipts should be sent to the messaging system, regardless of overall total cost.

## Success Criteria

* Demonstrate the Azure Function which publishes data to a pub/sub messaging service.
* Demonstrate the ability to filter messages to the appropriate process based on the total cost of purchased items.
* Demonstrate the ability to retrieve messages from the pub/sub service and save JSON files with a unique name to the proper blob storage container in the provided Azure Storage account (which uses service endpoints).

## References

* [Claim-Check Pattern](https://docs.microsoft.com/azure/architecture/patterns/claim-check)
* [Azure Virtual Network Service Endpoints](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview)
* [Azure Functions Premium plan (network connectivity)](https://docs.microsoft.com/azure/azure-functions/functions-premium-plan#private-network-connectivity)
* [Azure Functions binding expression patterns](https://docs.microsoft.com/azure/azure-functions/functions-bindings-expressions-patterns#create-guids)
* [Azure Functions triggers and bindings concepts](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings)
* [Azure Functions Recipes - Triggers and bindings](https://docs.microsoft.com/sandbox/functions-recipes/triggers-bindings)
* [Azure Service Bus Queues, Topics and Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-queues-topics-subscriptions)
* [Azure Service Bus bindings for Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-bindings-service-bus)
* [Azure Service Bus Topics and Filters](https://docs.microsoft.com/azure/service-bus-messaging/topic-filters)
* [Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-resource-manager-namespace-topic-with-rule)
* [Azure CLI (Service Bus)](https://docs.microsoft.com/cli/azure/servicebus/topic/subscription/rule?view=azure-cli-latest
)
* [Azure Service Bus Samples (GitHub)](https://github.com/Azure/azure-service-bus/tree/master/samples)
* [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer)

## Progress Diagram

![Pub/Sub and VNet Integration Progress Diagram](https://serverlessoh.azureedge.net/public/pubsub-and-vnet-integration-progress-diagram.jpg)

# Pub/Sub とネットワークの統合

## 背景

BFYOC の幹部は、POS 端末から販売データをクラウドに送るソリューションの実装がうまくいったことを受け、新しいデータのさらなる活用を進めたいと考えました。そこで、POS 端末を更新して、詳細なトランザクション データに加えてレシートの PDF を無作為に取得できるようにするパイロット プログラムを開始しました。すべてのトランザクション データをクラウド上のプライベート ストレージに格納し、データの保管と詳細な分析を可能にすることが目的です。幹部は不正な取引が行われていないかを懸念しており、金額が 100 ドル以上のトランザクションについては厳格にチェックしたいと考えています。

幹部から出されたおおまかな要件を踏まえて、クラウド アーキテクチャ チームは、パブリッシュ/サブスクライブ (pub/sub) 方式のメッセージング手法を実装して、レシートを含む POS の販売データを取得することにしました。メッセージ フィルタリング パターンを適用すれば、トランザクションの合計金額が 100 ドル以上の販売データを識別できると見込んでいます。また、顧客データや販売データの保護を重視し、1 つの Azure ストレージ アカウント内にすべてのデータを格納することで、Azure に配置している BFYOC の仮想ネットワーク内のサービス、またはそのネットワークと連携しているサービス以外からはアクセスできないようにして、安全性を確保したいと考えています。ファイルを Blob Storage に格納すれば、データ分析や不正検出プロセスなど、BFYOC の仮想ネットワーク内の他のシステムから使用できます。

BFYOC の既存の仮想ネットワークには、少なくとも 2 つのサブネットがあります。Azure ストレージ アカウントは、Azure Virtual Network サービス エンドポイントを使用して、仮想ネットワーク内の 2 つのサブネット以外のすべてのソースからのアクセスを制限するように構成されています。仮想ネットワーク内のサービスからデータを表示するための踏み台として、Azure Virtual Machines を使用できます。

![サブネットと Blob Storage サービス エンドポイントを持つ仮想ネットワーク](https://serverlessoh.azureedge.net/public/pubsub-and-vnet-integration-virtual-network-diagram.png)

## 課題

まず、レシートが存在する場合のみ、指定のレシート情報を pub/sub メッセージング システムに送信するよう、前の課題で使用した Azure Functions 関数を変更します。前の課題で作成したイベント ハブ経由で送信されてくる POS データを基に、次のような構造の JSON ドキュメントを新規作成して pub/sub メッセージング システムに送信します。

```JSON
{
    "totalItems": 8,
    "totalCost": 123.40,
    "salesNumber": "0c423398-3c7c-0682-7519-4701c445ed7a",
    "salesDate": "09/11/2019 06:04:43",
    "storeLocation": "00d8ea6f-935c-2cca-9bbc-f56b5a091621",
    "receiptUrl": "https://serverlessohsales.blob.core.windows.net/TheReceipt.pdf"
}
```

次に、それぞれのメッセージの合計金額でフィルタリングを行うために、次のタスクを実行するプロセスを作成します。

1. 合計金額が 100 ドル以上の場合

    * レシートの PDF ファイルを ```receiptUrl``` 値から取得する。
    * PDF を base64 でエンコードする。
    * レシート データと base64 でエンコードしたレシートを含む JSON オブジェクトを作成する。
    * JSON オブジェクトを一意の名前で、指定された Azure ストレージ アカウント内の「receipts-high-value」コンテナーに保存する (仮想ネットワークからのみアクセス可能)。

    保存するデータは次のような形式とします。

    ```JSON
    {
        "Store": "00d8ea6f-935c-2cca-9bbc-f56b5a091621",
        "SalesNumber": "0c423398-3c7c-0682-7519-4701c445ed7a",
        "TotalCost": 123.40,
        "Items": 8,
        "SalesDate": "09/11/2019 06:04:43",
        "ReceiptImage":"V2VsY29tZSB0byBTZXJ2ZXJsZXNzIE9wZW5IYWNrIQ=="
    }
    ```

2. 合計金額が 100 ドル未満の場合

    * レシート データを含む JSON オブジェクトを作成する。
    * JSON オブジェクトを一意の名前で、指定された Azure ストレージ アカウント内の「receipts」コンテナーに保存する (仮想ネットワークからのみアクセス可能)。

    保存するデータは次のような形式とします。

    ```JSON
    {
        "Store": "00d8ea6f-935c-2cca-9bbc-f56b5a091621",
        "SalesNumber": "0c423398-3c7c-0682-7519-4701c445ed7a",
        "TotalCost": 6.58,
        "Items": 1,
        "SalesDate": "09/02/2019 10:36:17"
    }
    ```

メッセージのフィルタリング方法を決める際には、時間が経つにつれて管理に追加の処理ストリームが必要になる可能性がある点に留意してください。フィルタリングを「コードで」実行するソリューションは避け、選択したメッセージング システムの機能を活用するようにします。

## 成功条件

* pub/sub メッセージング サービスにデータを発行する Azure Functions 関数の実装をコーチに示す。
* 購入商品の合計金額に基づいて適切なプロセスが実行されるようメッセージをフィルタリングする機能をコーチに示す。
* pub/sub メッセージング サービスからのメッセージを取得して、JSON ファイルを一意の名前で、指定された Azure Storage アカウントの適切な Blob Storage コンテナーに (サービス エンドポイントから) 保存する機能をコーチに示す。

## 参考資料

* [要求チェック パターン](https://docs.microsoft.com/ja-jp/azure/architecture/patterns/claim-check)
* [Azure Virtual Network サービス エンドポイント](https://docs.microsoft.com/ja-jp/azure/virtual-network/virtual-network-service-endpoints-overview)
* [Azure Functions Premium プラン (ネットワーク接続)](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-premium-plan#private-network-connectivity)
* [Azure Functions のバインド式のパターン](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-bindings-expressions-patterns#create-guids)
* [Azure Functions でのトリガーとバインドの概念](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-triggers-bindings)
* [Azure Functions ガイド: トリガーとバインド (英語)](https://docs.microsoft.com/sandbox/functions-recipes/triggers-bindings)
* [Azure Service Bus のキュー、トピック、サブスクリプション](https://docs.microsoft.com/ja-jp/azure/service-bus-messaging/service-bus-queues-topics-subscriptions)
* [Azure Functions における Azure Service Bus のバインド](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-bindings-service-bus)
* [Azure Service Bus のトピックとフィルター](https://docs.microsoft.com/ja-jp/azure/service-bus-messaging/topic-filters)
* [トピック、サブスクリプション、ルールを含む Service Bus 名前空間を Azure Resource Manager テンプレートで作成する](https://docs.microsoft.com/ja-jp/azure/service-bus-messaging/service-bus-resource-manager-namespace-topic-with-rule)
* [Azure CLI : Service Bus のルール (英語)](https://docs.microsoft.com/ja-jp/cli/azure/servicebus/topic/subscription/rule?view=azure-cli-latest
)
* [Azure Service Bus のサンプル (GitHub、英語)](https://github.com/Azure/azure-service-bus/tree/master/samples)
* [Service Bus Explorer (英語)](https://github.com/paolosalvatori/ServiceBusExplorer)

## 進捗図

![進捗図: pub/sub および VNet の統合](https://serverlessoh.azureedge.net/public/pubsub-and-vnet-integration-progress-diagram.jpg)
