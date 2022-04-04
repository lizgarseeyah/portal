# Alerting and notification

## Background

Best For You Organics Company's management would like to be alerted when
there's a high number of bad reviews for a specific ice cream. They are
hoping they can take advantage of the system you created earlier to react
to business related information that is raised from custom telemetry in
your code.

## Challenge

Your first challenge is to update the `CreateRating` function and put the
`userNotes` field through a sentiment analysis service. You should then
use the result of the sentiment analysis to add an extra field,
`sentimentScore`, to the JSON before saving to the database, and use custom telemetry to record information about the negative review.  Of particular interest for this challenge will be ratings that contain any sentences which receive a `negative` sentiment result having a score of 0.7 or greater.  

To start receiving automated ratings, make a post call to the
`/team/registerRatingEndpoint` method of the OpenHack API System.

* OpenHack API OpenUI Definition:
[Openhack Swagger](https://petstore.swagger.io/?url=https://serverlessohmanagementapi.trafficmanager.net/api/definition)

Your second challenge is to implement a solution to generate an email alert
to your coach whenever at least five bad ice cream reviews with a sentiment
analysis with a `negative` sentiment result greater than or equal to 0.7 have been received in the past five minutes. The email should contain the bad reviews information, or a link to the information about the reviews.

> Hint: This is five individual reviews containing at least one sentence with a negative sentiment score, not five total sentences in one or more reviews.  The threshold should be greater than or equal to five negative reviews in the previous five minutes.

## Success Criteria

* `GetRating` and `GetRatings` should return the `sentimentScore` field
with the sentiment analysis result from the `userNotes` for new ratings
created

* Your coach should receive an email with an alert containing information
about the bad reviews after five are created within five minutes by the
automated system

## References

* [How to detect sentiment in Text Analytics](https://docs.microsoft.com/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis)

* [Monitor Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-monitoring)

* [Log alerts in Azure Monitor - Alerts for Application Insights](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitor-alerts-unified-log)

## Progress Diagram

![Alerting and notification progress diagram](https://serverlessoh.azureedge.net/public/alerting-and-notification-progress-diagram.jpg)

# アラートと通知

## 背景

BFYOC の経営陣は、特定のアイス クリームへの低評価が多数見られる場合に、アラートで通知を受けたいと考えています。これまでにチームが作成したシステムを活用すれば、カスタム テレメトリからビジネス情報を引き出して迅速に対応できるようになるのではないかと期待を寄せています。

## 課題

1 つ目の課題として、`CreateRating` 関数を更新し、`userNotes` フィールドをセンチメント分析サービスに渡します。そのセンチメント分析の結果を、JSON ドキュメントの `sentimentScore` という新規フィールドに追加してからデータベースに保存します。

自動評価の受信を開始するには、OpenHack API システムの `/team/registerRatingEndpoint` メソッドに POST 呼び出しを行います。

* OpenHack API の OpenUI 定義 [OpenHack API システム (Swagger、英語)](https://petstore.swagger.io/?url=https://serverlessohmanagementapi.trafficmanager.net/api/definition)

2 つ目の課題として、センチメント分析のスコアが 0.3 以下の低評価レビューを過去 5 分間に少なくとも 5 件受け取った場合に、メール アラートをコーチ宛てに生成するソリューションを実装します。このメールには、低評価レビューの情報、またはそのレビュー情報へのリンクを含めます。

## 成功条件

* 新たに作成した `userNotes` からのセンチメント分析の結果を格納した `sentimentScore` フィールドを、`GetRating` と `GetRatings` から返す。

* 5 分間に 5 件の低評価レビューが投稿された場合、レビュー情報を含むメール アラートがコーチ宛てに自動システムから送信される。

## 参考資料

* [Text Analytics でセンチメントを検出する](https://docs.microsoft.com/ja-jp/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis)

* [Azure Functions を監視する](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-monitoring)

* [Azure Monitor でのログ アラート、Application Insights のアラート](https://docs.microsoft.com/ja-jp/azure/azure-monitor/platform/alerts-unified-log)

## 進捗図

![進捗図: アラートと通知](https://serverlessoh.azureedge.net/public/alerting-and-notification-progress-diagram.jpg)
