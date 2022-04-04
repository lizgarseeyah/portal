# Process distributor order batch files

## Background

Best For You Organics Company (BFYOC) receives orders from distributors
via flat files, similar to that of many businesses. These files come in
batches of three, however each file can come in at different times. BFYOC
would like your team to create an implementation that can process the files
as a batch, storing the data contained as a single JSON object in a database.

## Challenge

The purchase order information from some of the distributors arrive in
batches. Each batch is made up of exactly three different files, each with
different information about orders, as described below:

* Type 1: order header details.
For example: `20180518151300-OrderHeaderDetails.csv`

* Type 2: order line items. For example:
`20180518151300-OrderLineItems.csv`

* Type 3: product information for the batch.
For example: `20180518151300-ProductInformation.csv`

For these example file names the batch that binds them together is the file
name prefix `20180518151300`.

Before continuing to the challenge, create a Storage Account of kind
`StorageV2 (general purpose v2)` in your Azure Subscription, and then create
a new Blob container in it.

You will be required to post your team table number, the storage account
connection string, and the blob container name. The distributor systems will
start sending batches of flat files with order details into your blob storage
container every 1 minute. The date based prefix of the file names will indicate
what files belong to the same batch.

Make an HTTP POST call to the `/team/registerStorageAccount`
endpoint of the [Serverless OpenHack API System](https://petstore.swagger.io/?url=https://serverlessohmanagementapi.trafficmanager.net/api/definition) to register your team's storage account.

**Take note of the teamTableNumber used in this registration. It will be required in later challenges.**

**Make sure to note that the API is case-sensitive, so all parameters and parameter values must match case.  Review the swagger documentation to make sure you have the BODY composed correctly [here](https://petstore.swagger.io/?url=https://serverlessohmanagementapi.trafficmanager.net/api/definition#/Register%20Storage%20Account/register)**

Your challenge is to work as a team to create a solution that:

* Waits until all the files for the same batch arrive before processing them.

* Once all three files for a batch have been received, make an HTTP POST call to the `/order/combineOrderContent`
endpoint of the [Serverless OpenHack API System](https://petstore.swagger.io/?url=https://serverlessohmanagementapi.trafficmanager.net/api/definition), which will combine the content and return a single JSON document per order.

**Make sure to note that the API is case-sensitive, so all parameters and parameter values must match case.  Review the swagger documentation to make sure you have the BODY composed correctly [here](https://petstore.swagger.io/?url=https://serverlessohmanagementapi.trafficmanager.net/api/definition#/Register%20Storage%20Account/combineOrderContent)**

* Insert the JSON document of each order into your database as a separate
entry/record.

**Note: The Serverless Open Hack will periodically check team registrations
and delete those with invalid storage accounts and services used in later
challenges. To ensure your team's registration isn't deleted, be sure not to
delete the Azure services used here and subsequent challenges.**

>HINT: Make sure to register EventGrid as a resource provider on your Azure Subscription before trying to respond to storage events.  Failure to register Event Grid will result in an inability to create subscriptions that respond to Azure storage events

## Success Criteria

* Demonstrate to your coach how you implemented the workflow to read, combine,
and insert the data from the batches of flat files into one JSON document per
order into a database. All the details from the flat files need to be in the
JSON documents generated.

## References

* [Register Event Grid](https://docs.microsoft.com/en-us/azure/event-grid/custom-event-quickstart-portal)  

* [An introduction to Azure Event Grid](https://docs.microsoft.com/azure/event-grid/overview)

* [Event Grid: Reacting to Blob Storage events](https://docs.microsoft.com/azure/storage/blobs/storage-blob-event-overview)

* [Durable Functions overview](https://docs.microsoft.com/azure/azure-functions/durable-functions-overview)

* [Send, receive, and batch process messages in Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-batch-process-send-receive-messages)

## Progress Diagram

![Process distributor order batch files progress diagram](https://serverlessoh.azureedge.net/public/order-batch-files-progress-diagram.jpg)

# 流通業者の注文バッチ ファイルを処理する

## 背景

BFYOC は、他の多くの企業と同様に、流通業者からの注文をフラット ファイルで受け取ります。3 種類のファイルで 1 つの注文情報となりますが、それぞれ異なるタイミングで送られてくる場合があります。BFYOC は、これらのファイルを一括で処理し、そのデータを 1 つの JSON オブジェクトとしてデータベースに保存したいと考えています。

## 課題

一部の流通業者からの注文情報は、複数のファイルで届きます。ファイルは 3 種類あり、それぞれ以下のように異なる情報を保持しています。

* タイプ 1: 注文ヘッダーの詳細
例: `20180518151300-OrderHeaderDetails.csv`

* タイプ 2: 注文明細行の品目
例:
`20180518151300-OrderLineItems.csv`

* タイプ 3: 注文バッチの商品情報
例: `20180518151300-ProductInformation.csv`

上の例の場合、各ファイルの名前の `20180518151300` というプレフィックスを基に 1 つの注文バッチにまとめることができます。

課題を進める前に、Azure サブスクリプションに `StorageV2 (汎用 v2)` などのストレージ アカウントを作成し、その中に BLOB コンテナーを新規作成します。

チームのテーブル番号、ストレージ アカウントの接続文字列、BLOB コンテナー名を流通業者のシステムに送信します。システムに登録されたら、注文情報を含むフラット ファイルが 1 分おきに BLOB コンテナーに送られてきます。日時に基づくプレフィックスが同じであれば、同じ注文バッチに属するファイルということになります。

[Serverless OpenHack API システム (英語)](https://petstore.swagger.io/?url=https://serverlessohmanagementapi.trafficmanager.net/api/definition) のエンドポイント `/team/registerStorageAccount` に対して HTTP POST 呼び出しを実行し、チームのストレージ アカウントを登録します。

**この登録処理で使用する teamTableNumber をメモしておいてください。後の課題で必要になります。**

この課題では、次のようなソリューションを作成します。

* 同一注文バッチのファイルすべてを受信するまで処理を待機する。

* 注文バッチの 3 ファイルすべてを受信したら、[Serverless OpenHack API システム (英語)](https://petstore.swagger.io/?url=https://serverlessohmanagementapi.trafficmanager.net/api/definition) のエンドポイント `/order/combineOrderContent` に対して HTTP POST 呼び出しを実行する。これにより、ファイルが結合され、注文ごとに 1 つの JSON ドキュメントが返されます。

* 各注文の JSON ドキュメントを個別のエントリ/レコードとしてデータベースに追加する。

**注: この Serverless OpenHack では、チームによる登録が定期的にチェックされ、ストレージ アカウントと後の課題で使用するサービスが無効なものは削除されます。自分のチームが登録したものが削除されないように、この課題以降で使用する Azure サービスは削除しないでください。**

## 成功条件

* ワークフローの実装をコーチに示す。ワークフローでは、フラット ファイルの注文バッチ データを読み込み、注文ごとに 1 つの JSON ドキュメントに結合し、データベースに格納する。生成される JSON ドキュメントには、フラット ファイルから取得した詳細情報すべてが含まれている必要がある。

## 参考資料

* [Azure Event Grid とは](https://docs.microsoft.com/ja-jp/azure/event-grid/overview)

* [Event Grid: Blob Storage イベントへの対応](https://docs.microsoft.com/ja-jp/azure/storage/blobs/storage-blob-event-overview)

* [Durable Functions とは](https://docs.microsoft.com/ja-jp/azure/azure-functions/durable/durable-functions-overview)

* [Azure Logic Apps でのメッセージの送信、受信、バッチ処理](https://docs.microsoft.com/ja-jp/azure/logic-apps/logic-apps-batch-process-send-receive-messages)

## 進捗図

![進捗図: 流通業者の注文バッチ ファイル処理](https://serverlessoh.azureedge.net/public/order-batch-files-progress-diagram.jpg)
