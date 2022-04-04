# Putting it All Together

## Background

As Best For You Organics Company (BFYOC) now has data from customer reviews, distributor
orders, and POS sales for the new fruit flavored ice cream line, the
product managers would like to know how the new line of ice creams are
doing.

## Challenge

Your challenge is to work on a solution that monitors and forwards the
reviews, distributor orders, and POS sales data to an event-processing
engine that will then, every 5 minutes, summarize the following:

* A list of ice creams based on total distributor orders total sales,
from highest to lowest
* A list of ice creams based on total POS sales, from highest to lowest
* The average sentiment analysis value for each ice cream

Aggregate the data for each 5 minute tumbling window and then use that
data to generate a report for your manager (your coach) with these insights.

## Success Criteria

* Demonstrate to your coach how you implemented the solution

* The coach should have access to a report that includes all the required
info as per the Challenge section.

## References

* [What is Stream Analytics?](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-introduction)

* [Stream data as input into Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-define-inputs)

* [Query examples for common Stream Analytics usage patterns](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-stream-analytics-query-patterns)

* [Azure Stream Analytics output to Azure Cosmos DB](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-documentdb-output)

* [Working with the change feed support in Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/change-feed)

## Progress Diagram

![Final progress diagram](https://serverlessoh.azureedge.net/public/final-progress-diagram.jpg)

# すべてを集約する

## 背景

BFYOC は、新商品のフルーツ フレーバー アイス クリームに関して、顧客のレビュー、流通業者からの注文、POS の販売データなどのデータを集められるようになりました。そこで、プロダクト マネージャーは、新商品の売れ行きを把握したいと考えています。

## 課題

レビュー、流通業者からの注文、POS の販売データを監視し、それらをイベント処理エンジンに転送するソリューションを構築し、このイベント処理エンジンで 5 分ごとに以下をまとめます。

* 流通業者から注文の合計売上高を降順に並べたアイス クリームのリスト
* POS の合計売上高を降順に並べたアイス クリームのリスト
* 各アイス クリームのセンチメント分析の平均スコア

これらを 5 分ごとに集約し、レポートにまとめてマネージャー (チームのコーチ) 宛てに送信します。

## 成功条件

* 必要なソリューションの実装をコーチに見せる。

* 課題セクションで指示されている情報すべてを記載したレポートにコーチがアクセスできるようにする。

## 参考資料

* [Azure Stream Analytics とは](https://docs.microsoft.com/ja-jp/azure/stream-analytics/stream-analytics-introduction)

* [Stream Analytics に入力としてデータをストリーム配信する](https://docs.microsoft.com/ja-jp/azure/stream-analytics/stream-analytics-define-inputs)

* [一般的な Stream Analytics 使用パターンのクエリ例](https://docs.microsoft.com/ja-jp/azure/stream-analytics/stream-analytics-stream-analytics-query-patterns)

* [Azure Cosmos DB への Azure Stream Analytics の出力](https://docs.microsoft.com/ja-jp/azure/stream-analytics/stream-analytics-documentdb-output)

* [Azure Cosmos DB でサポートされている変更フィードの操作](https://docs.microsoft.com/ja-jp/azure/cosmos-db/change-feed)

## 進捗図

![進捗図全体](https://serverlessoh.azureedge.net/public/final-progress-diagram.jpg)
