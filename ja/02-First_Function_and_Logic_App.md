# Create your first serverless function & workflow

## Background

In this challenge you will start creating your first serverless
functions and wokflows, which are key skills for the upcoming
challenges which make up this OpenHack.

## Challenge

Your first goal is for each team member to create and debug an HTTP
triggered Azure Function locally on your own development machine. This
function has the following requirements:

* **Verb**: GET
* **Input parameters**: A `productId` value is passed to it as a
query parameter or an HTTP route
* **Result**: "The product name for your product id
{the id passed in to the function} is Starfruit Explosion"

The second goal is for each team member to create their own Azure Resource
Group in your team's Azure Subscription, and then deploy the function from
the first goal to it.
**Make sure to use different, unique Function App names!** Then test the
function after deployed.

Your final goal for this challenge is for each team member to create an
HTTP triggered Logic App in their Resource Group. The Logic App has the
following trigger requirements:

* **Verb**: POST
* **Input payload example**:

    ```JSON
    {
        "productId": "75542e38-563f-436f-adeb-f426f1dabb5c"
    }
    ```

Next, you should configure the Logic App to call the Azure Function created
 earlier, passing the `productId` into it, then reply successfully with the
 response text content of **"{response from function} and the description
 is This starfruit ice cream is out of this world!"**.

So, for the example inputs above the Logic App would reply with
**"The product name for your product id 75542e38-563f-436f-adeb-f426f1dabb5c
is Starfruit Explosion and the description is This starfruit ice cream is
out of this world!"**.

**Hint**: To pass query parameters from Logic Apps to a function in the Azure
Functions action, you can write the name and values as JSON in the Queries
field. Example:

```JSON
{
  "queryParamName": "queryparamValue"
}
```

## Success Criteria

*Given the complexity and variety of potential solutions, the goals for all
challenge are verified by your team's coach.*

* Everyone on your team must demonstrate that you created an HTTP triggered
Azure Function locally that accepts a GET verb. Show to your coach that you
can call that function and receive a successful response with the right text
provided and the value of `productId` properly filled in.

* Everyone on your team must demonstrate that you deployed that HTTP triggered
Azure Function to Azure. Show to your coach that you can call that deployed
function and receive a successful response.

* Everyone on your team must demonstrate that you can call the Logic App via HTTP
POST which then calls the Function, and that it replies successfully with the
correct extended text.

## References

* [An introduction to Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)

* [Supported languages in Azure Functions](https://docs.microsoft.com/azure/azure-functions/supported-languages)

* [Write Azure functions in VSCode](https://docs.microsoft.com/en-us/azure/azure-functions/functions-develop-vs-code?tabs=csharp)

* [Test your project locally](https://docs.microsoft.com/en-us/azure/developer/javascript/tutorial-vscode-serverless-node-03)

* [Strategies for testing your code in Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-test-a-function)  

* [Code and test Azure Functions locally](https://docs.microsoft.com/azure/azure-functions/functions-develop-local)  

* [Logic Apps Overview](https://docs.microsoft.com/azure/logic-apps/logic-apps-overview)  

* [Create a Logic App](https://docs.microsoft.com/azure/logic-apps/quickstart-create-first-logic-app-workflow)  

* [Logic Apps Call, trigger, or nest workflows with HTTP endpoints in Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-http-endpoint)  

*[First Azure Function Visual Studio](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-your-first-function-visual-studio)  

* [Azure Functions Python developer guide](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-python)  

[Azure Functions create first Python Function](https://docs.microsoft.com/azure/azure-functions/functions-create-first-function-python) for latest version/environment configuration information.  

# サーバーレス関数とワークフローの作成

## 背景

この課題では、手始めにサーバーレス関数とワークフローを作成します。このスキルは、OpenHack の今後の課題で重要となります。

## 課題

1 つ目の目標として、チーム メンバー各自が、HTTP でトリガーされる Azure Functions 関数を開発マシンのローカル環境で作成、デバッグします。この関数の要件は以下のとおりです。

* **動詞**: GET
* **入力パラメーター**: クエリ パラメーターまたは HTTP ルートとして渡す `productId` 値
* **結果**: 「商品 ID {関数に渡した ID} の
商品名は “スターフルーツ エクスプロージョン” です。」というテキスト

2 つ目の目標として、チーム メンバー全員が各自の Azure リソース グループをチーム用の Azure サブスクリプション内に作成し、そこに上記で作成した関数をデプロイします。**関数のアプリ名には一意の名前を付け、重複しないようにしてください。**その後、デプロイした関数のテストを行います。

ここでの最終目標は、チーム メンバー全員が HTTP でトリガーされるロジック アプリをリソース グループ内に作成することです。ロジック アプリのトリガー要件は以下のとおりです。

* **動詞**: POST
* **入力ペイロードの例**

    ```JSON
    {
        "productId": "75542e38-563f-436f-adeb-f426f1dabb5c"
    }
    ```

次に、先ほど作成した Azure Function 関数を呼び出すようにロジック アプリを構成します。 `productId` を関数に渡し、正常な応答として「**{関数からの応答}商品説明は、“このスターフルーツ味のアイスは絶品!” です。**」というテキストを返すようにします。

上記の入力例の場合、ロジック アプリからの応答は「**商品 ID 75542e38-563f-436f-adeb-f426f1dabb5c の商品名は “スターフルーツ エクスプロージョン”です。商品説明は、“このスターフルーツ味のアイス クリームは絶品!” です。**」となります。

**ヒント**: ロジック アプリから Azure Functions アクションの関数にクエリ パラメーターを渡すには、以下の例のように Queries フィールドに JSON 形式で名前と値を指定します。

```JSON
{
  "queryParamName": "queryparamValue"
}
```

## 成功条件

チームを担当するコーチが、ソリューションの複雑さと多様性を考慮しながら、すべての課題の成果を評価します。

* チーム メンバー全員が、HTTP でトリガーされ GET 動詞に応答する Azure Functions 関数をローカルで作成したことを示す。この関数を呼び出して、指定した正しいテキストに `productId` の値が適切に埋め込まれた応答を正常に受け取れることをコーチに見せる。

* チーム メンバー全員が HTTP でトリガーされる Azure Functions 関数を Azure にデプロイしたことを示す。デプロイした関数を呼び出し、正常な応答を受け取れることをコーチに見せる。

* チーム メンバー全員が Functions 関数を呼び出すロジック アプリを HTTP POST で呼び出せることを示す。ロジック アプリが正しい内容のテキストで正常に応答することを実際に示す。

## 参考資料

* [Azure Functions の概要](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-overview)
* [Azure Functions でサポートされている言語](https://docs.microsoft.com/ja-jp/azure/azure-functions/supported-languages)
* [Azure Functions のコードをテストするための戦略](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-test-a-function)
* [Azure Functions をローカルでコーディングしてテストする](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-develop-local)
* [Logic Apps の概要](https://docs.microsoft.com/ja-jp/azure/logic-apps/logic-apps-overview)
* [ロジック アプリを作成する](https://docs.microsoft.com/ja-jp/azure/logic-apps/quickstart-create-first-logic-app-workflow)
* [Logic Apps で HTTP エンドポイントを使用して、ロジック アプリを呼び出しまたはトリガーし、ワークフローを入れ子にする](https://docs.microsoft.com/ja-jp/azure/logic-apps/logic-apps-http-endpoint)
