# System telemetry and API Management

## Background

Now that the Best For You Organics (BFYOC) API is complete, they want to start tracking telemetry from their API calls to be able to monitor the solution. After all, if you can't measure it, you can't improve it!

BFYOC would also like to begin exposing their APIs. They want to ensure the the APIs use consistent URL. They also want them exposed as different suites of APIs. They would like to have a different suite of APIs  exposed to the mobile application, internal business users running reports and external partners. They also want to ensure that their mobile users receive priority access to those APIs by throttling requests from both internal business users and external partners.

## Telemetry

The first part of this challenge is to work as a team to enable telemetry for the production Ratings API functions. BFYOC has requested a table derived from telemetry that displays the following information about your Ratings functions:

* The number of times each function was run in the past hour

* The average duration of each function in that hour

* There should be one row for each of the three Ratings functions your team created earlier

> **Hint**: Application Insights may take a few minutes before showing telemetry from your functions

## API Exposure

### Uniform URL

Next your team is to create a uniformly addressed version of the entire API. This includes the `GetUser`, `GetProduct` and `GetProducts` APIs that already existed, and all the production functions your team created: `CreateRating`, `GetRating`, and `GetRatings`. Your team should expose all of these operations under the same base URL, as they currently are under different base URLs.

### Product suites

Your team will now need to create 3 suites of APIs. One for each of the use cases: Mobile Application, Internal business users and External Partners. The team will need to configure the products so that only the required operations are exposed to the different product suites. Those requirements are as follows:

#### Mobile Applications

The Mobile Application requires access to all of the APIs. Each of them is required for different areas of the application's UX. So the operations that need to be configured for this product suite are as follows:

* GetUser
* GetProduct
* GetProducts
* CreateRating
* GetRating
* GetRatings

#### Internal business users

The Internal business users use the APIs for reporting purposes. They need access to the product and rating information but shouldn't be using the user operation or be able to create ratings. So the operations that should be exposed to this product suite are as follows:

* GetProduct
* GetProducts
* GetRating
* GetRatings

#### External Partners

The External Partners use case is to be able to see products that BYFOC has to offer, so should only have the product operations exposed to them. So this product suite should only have the following operations exposed to them:

* GetProduct
* GetProducts

### Throttling

Finally, we need to ensure that our Mobile Application users are given priority over use of these APIs. We need to create some throttling on the operations exposed to the Internal business users and the External Partners.

Your team will need to create policies that ensure that the Internal business users do not make more than 30 calls within a 10 second time period on the operations that are exposed through this product suite.

The External Partners should also be throttled, but shouldn't be throttled as greatly. The operations exposed to our partners should be limited to 60 calls per 15 seconds.

The mobile applications users shouldn't have any throttling configured on the operations exposed to them.

## Success Criteria

* Demonstrate to your coach the implementation of how to check the total number of times and the average duration of each function for the past hour based on telemetry. The results should be displayed as a table, in the same result set, and have one row for each of the three production Ratings API functions you created in the previous challenge.

    > No need to store the results in a data store, on screen display of the results is sufficient

* Demonstrate to your coach the implementation of exposing a uniform API under the same base URL for all functions

* Demonstrate to your coach the configuration of the 3 different product suites and the operations exposed to each of them.

* Demonstrate to your coach the implementation of the rate limiting requirements. The results should have different policies configured on the Internal business users product suite then on the External Partners product suite. There should be no throttling configured on the Mobile Applications product suite.

## References

* [Monitor Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-monitoring)
* [Azure Monitor Log Queries](https://docs.microsoft.com/azure/azure-monitor/log-query/log-query-overview)
* [Azure API Management Overview](https://docs.microsoft.com/azure/api-management/api-management-key-concepts)
* [Azure API Management Tiers](https://docs.microsoft.com/azure/api-management/api-management-features)
* [Azure API Management Policies](https://docs.microsoft.com/azure/api-management/set-edit-policies)
* [Azure API Management Access Restriction Policies](https://docs.microsoft.com/azure/api-management/api-management-access-restriction-policies)

## Progress Diagram

![System telemetry and API Management progress diagram](https://serverlessoh.azureedge.net/public/system-telemetry-and-api-management-progress-diagram.jpg)

# システム テレメトリと API 管理

## 背景

API が完成したので、BFYOC は次に、API を呼び出してテレメトリの追跡を開始し、ソリューションを監視できるようにすることを検討しています。測定できなければ改善することができないからです。

BFYOC は、API の公開に着手するにあたって、一貫性のある URL を使用する API にしたいと考えています。また、モバイル アプリケーション向けの API、レポートを実行する社内業務ユーザー向けの API、外部パートナー向けの API というように、用途別に異なる API スイートを公開することを要望しています。さらに、社内業務ユーザーと外部パートナーの双方からの API リクエストをスロットリングすることにより、モバイル ユーザーが優先的にアクセスできるようにしたいと考えています。

## テレメトリ

この課題ではまず、運用環境に展開しているレーティング API の関数のテレメトリを収集できるようにします。BFYOC は、テレメトリを基に、各レーティング関数についての情報を次のような表に出力するよう要望しています。

* 過去 1 時間に各関数が実行された回数を表示

* その 1 時間における各関数の平均実行時間を表示

* チームがこれまでに作成した 3 つのレーティング関数 1 つにつき 1 行で表示

> **ヒント**: Application Insights は、関数からテレメトリを取得するまでに数分かかる場合があります。

## API の公開

### 統一 URL

すべての API に対して統一的なアドレスを作成します。これは、既存の API (`GetUser`、`GetProduct`、`GetProducts`)、チームが作成した運用環境のすべての関数 (`CreateRating`、`GetRating`、`GetRatings`) が対象となります。現在これらは異なるベース URL の下に存在しているため、統一されたベース URL で公開します。

### API スイート

モバイル アプリケーション、社内業務ユーザー、外部パートナーというユース ケースごとに 1 つずつ、計 3 つの API スイートを作成します。それぞれのスイートは、必要な操作のみを公開するように構成する必要があります。要件は次のとおりです。

#### モバイル アプリケーション

モバイル アプリケーションではすべての API にアクセスする必要があります。どれもアプリケーションの UX のさまざまな領域に欠かせません。したがって、このスイート用に構成する操作は次のとおりです。

* GetUser
* GetProduct
* GetProducts
* CreateRating
* GetRating
* GetRatings

#### 社内業務ユーザー

社内業務ユーザーは、レポートを作成する目的で API を使用するため、商品とレーティングの情報にアクセスできなくてはいけません。ただし、ユーザー情報の取得やレーティングの作成は不要です。したがって、このスイートで公開すべき操作は次のとおりです。

* GetProduct
* GetProducts
* GetRating
* GetRatings

#### 外部パートナー

外部パートナーの場合は、BYFOC が販売している商品を確認する必要があるため、商品情報にアクセスできる必要があります。したがって、このスイートでは次の操作のみを公開します。

* GetProduct
* GetProducts

### スロットリング

最後に、社内業務ユーザーと外部パートナーに公開する操作に対してスロットリングを行うことで、モバイル アプリケーションのユーザーが優先的に API を使用できるようにします。

社内業務ユーザーが API スイートで公開されている操作を 10 秒間に 30 回を超えて呼び出せないようにするポリシーを作成します。

外部パートナーの操作もスロットリングする必要がありますが、それほど厳しくせずに、外部パートナーに公開する操作の呼び出しは 15 秒あたり 60 回までとします。

モバイル アプリケーションのユーザーに公開する操作はスロットリングの構成を行いません。

## 成功条件

* テレメトリに基づいて各関数の過去 1 時間の実行回数と平均実行時間を確認する機能を実装したことをコーチに示す。結果は 1 つの表にまとめ、前の課題で作成した 3 つのレーティング API 関数 1 つにつき 1 行で表示する。

    > 結果をデータ ストアに保存する必要はありません。画面に表示するだけで十分です。

* すべての関数が同じベース URL で統一されている API を公開したことをコーチに示す。

* 3 つの異なる API スイートの構成と、それぞれで公開している操作をコーチに見せる。

* レート制限の要件をコーチに示す。社内業務ユーザー向けスイートと外部パートナー向けスイートは異なるポリシーで構成する。モバイル アプリケーション向けスイートにはスロットリングを構成しない。

## 参考資料

* [Azure Functions を監視する](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-monitoring)
* [Azure Monitor のログ クエリ](https://docs.microsoft.com/ja-jp/azure/azure-monitor/log-query/log-query-overview)
* [Azure API Management について](https://docs.microsoft.com/ja-jp/azure/api-management/api-management-key-concepts)
* [Azure API Management のレベル](https://docs.microsoft.com/ja-jp/azure/api-management/api-management-features)
* [Azure API Management のポリシー設定](https://docs.microsoft.com/ja-jp/azure/api-management/set-edit-policies)
* [Azure API Management のアクセス制限ポリシー](https://docs.microsoft.com/ja-jp/azure/api-management/api-management-access-restriction-policies)

## 進捗図

![進捗図: システム テレメトリと API 管理](https://serverlessoh.azureedge.net/public/system-telemetry-and-api-management-progress-diagram.jpg)
