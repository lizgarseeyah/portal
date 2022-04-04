# Notify all distributors of the new ice cream line

## Background

The food development, marketing, production, and quality teams at Best For You Organics (BFYOC) have released the details about their new line of ice creams to the sales department. The sales department has now asked your team to allow for notification of the main contact at each distributor with the information about the new line so they can review and start sending in orders.

In this challenge you will create a workflow between Best For You Organics CRM systems (Dynamics 365) and the company's distributors.  

## Challenge

Your team should implement an HTTP triggered workflow that will generate an HTML email with the list of products, and then send an email to each of the main contacts at the distributors.

BFYOC has provided HTML that you can use as a starting point for the body of the emails.  

**Note that this HTML includes a section that you need to programmatically loop through each product to finish creating the table.**

```HTML
<!DOCTYPE html>
<html>
<body style="background-color: whitesmoke; color: #454545; font-family:'Gill Sans',
 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif; padding-bottom: 3em;">
  <table style="width:100%; color:#454545">
    <tr>
      <td style="width:11em;">
        <img style="margin-left:1em;"
        src="https://serverlessoh.azureedge.net/public/ice-cream-2202561_320-circle.jpg"
          height="160" width="160" alt="Fruit Ice Cream">
      </td>
      <td>
        <p style="font-style: italic; font-size: 50px;
        font-weight:600; margin-left: 1em;">Best For You Organics</p>
      </td>
    </tr>
  </table>
  <p style="text-align: center; font-style: italic; font-size:
  80px;">New Ice Cream Line!</p>
  <p style="margin:2em 0em; font-size: 20px; text-align: center;">
  Best For You Organics have a new line of fruit flavored ice creams.
  Below is the information so you can start the ordering process:
  </p>
  <table style="width:100%; border-top: 1px solid #454545;
  border-bottom: 1px solid #454545; color:#454545; padding: 1em; font-size: 20px;">
    <thead>
      <tr>
        <th style="padding-bottom: 1em;" align="left">Ice Cream</th>
        <th style="padding-bottom: 1em;" align="left">Description</th>
        <th style="padding-bottom: 1em;" align="left">Product ID</th>
      </tr>
    </thead>
    <tbody style="font-size: 16px;">
  <!-- LOOP THROUGH EACH PRODUCT HERE AND CREATE A TABLE ROW ENTRY FOR EACH -->
    </tbody>
  </table>
  <p style="text-align: center; margin-top: 3em;font-size: 20px;">Please contact
  your representative at Best For You Organics to get more information..</p>
</body>
</html>
```

You can access the list of products via the `GetProducts` method in the existing Azure Function in your subscription.

You can retrieve the main contacts of the distributors from the distributor's Dynamics 365 CRM systems with the following detail:

* User: `duser@microsoftopenhack.onmicrosoft.com`

* Password: `pass@word1`

* Environment: `Microsoft OpenHack (msftopenhack)`

* Entity: `Contacts`

> Viewing records to select the entity from the distributor's Dynamics 365 CRM system can take several seconds. Please be patient.

The `Email` field from each contact contains the email address to be used for each distributor contact.  

The email should also contain your team number in the subject. Feel free to also add the email address of someone in your team in CC so you can see what the emails look like.

>HINT: The same credentials for user and password as listed above can also be used to send emails from `Office 365 Outlook` Add your own email address to the list and/or review the workflow executions to see the emails sent to validate the emails are sent as expected to multiple distributors.  

## Success Criteria  

* The email looks correct in an HTML format and with the list of products  

* Your coach will be able to validate that the distributors have received the email with your HTML content  

* Make sure your team number is in the email subject  

* Once the coach has validated the email, show the implementation to them  
  
## References  
  
* [Create and manage records in Dynamics 365 using Azure Logic Apps](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)  

* [Microsoft Dataverse (legacy)](https://docs.microsoft.com/connectors/commondataservice/)

* [List Records using a Common Data Service (Microsoft Dataverse) connector](https://docs.microsoft.com/azure/connectors/connect-common-data-service#list-records-based-on-a-filter)  

* [Office 365 Connector](https://docs.microsoft.com/connectors/office365/)  

* [Loops in Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-control-flow-loops)  

* [Create variables for saving and managing values in Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-create-variables-store-values)  

* [Perform data operations in Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-perform-data-operations)  

* [Logic Apps workflow actions and triggers](https://docs.microsoft.com/azure/logic-apps/logic-apps-workflow-actions-triggers)  

# すべての流通業者に新商品のアイス クリームを通知する

## 背景

BFYOC の食品開発チーム、マーケティング チーム、製造チーム、品質管理チームが、新商品のアイス クリームに関する詳細を販売部門に公開しました。販売部門から皆さんのチームへの依頼は、流通業者が新商品について確認して発注を開始できるよう、情報を各業者の主要連絡先に通知する機能です。

この機能を実現するために、BFYOC の CRM システム (Dynamics 365) と流通業者の間にワークフローを作成します。

## 課題

HTTP でトリガーされるワークフローを実装します。このワークフローで新商品のリストを記載した HTML メールを生成し、各流通業者の主要連絡先に送信します。

BFYOC が用意した HTML メール本文のひな形を使用します。**この HTML には、商品ごとにループするプログラムを組んで表を完成させる必要があるセクションがあります。**

```HTML
<!DOCTYPE html>
<html>
<body style="background-color: whitesmoke; color: #454545; font-family:'Gill Sans',
 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif; padding-bottom: 3em;">
  <table style="width:100%; color:#454545">
    <tr>
      <td style="width:11em;">
        <img style="margin-left:1em;"
        src="https://serverlessoh.azureedge.net/public/ice-cream-2202561_320-circle.jpg"
          height="160" width="160" alt="Fruit Ice Cream">
      </td>
      <td>
        <p style="font-style: italic; font-size: 50px;
        font-weight:600; margin-left: 1em;">Best For You Organics</p>
      </td>
    </tr>
  </table>
  <p style="text-align: center; font-style: italic; font-size:
  80px;">新商品のアイス クリーム!</p>
  <p style="margin:2em 0em; font-size: 20px; text-align: center;">
  Best For You Organics から新しいフルーツ フレーバー アイス クリームの登場です。
  下記情報をご確認のうえ、今すぐご注文ください。
  </p>
  <table style="width:100%; border-top: 1px solid #454545;
  border-bottom: 1px solid #454545; color:#454545; padding: 1em; font-size: 20px;">
    <thead>
      <tr>
        <th style="padding-bottom: 1em;" align="left">アイス クリーム</th>
        <th style="padding-bottom: 1em;" align="left">説明</th>
        <th style="padding-bottom: 1em;" align="left">商品 ID</th>
      </tr>
    </thead>
    <tbody style="font-size: 16px;">
  <!-- ここで商品ごとにループし、各商品のテーブル行エントリを作成 -->
    </tbody>
  </table>
  <p style="text-align: center; margin-top: 3em;font-size: 20px;">
  詳しくは Best For You Organics の販売担当者までお問い合わせください。</p>
</body>
</html>
```

商品リストは、サブスクリプション内の既存 Azure Functions 関数の `GetProducts` メソッドからアクセスできます。

流通業者の主要連絡先は、以下のアカウントの Dynamics 365 システムから取得できます。

* ユーザー: `duser@microsoftopenhack.onmicrosoft.com`

* パスワード: `pass@word1`

* 組織名: `Microsoft OpenHack (msftopenhack)`

* エンティティ: `Contacts`

> Dynamic 365 からのレコードの表示には数秒かかる場合があります。その場合は少しお待ちください。

流通業者の連絡先メール アドレスは、`emailaddress1` フィールドに格納されています。Office 365 からメールを送信する際に、上記の資格情報を使用することもできます。

メールの件名にはチーム番号が含まれるようにします。チーム内のだれかのメール アドレスを CC に追加しておくと、メールの内容を確認できます。

## 成功条件

* 商品リストを記載したメールを HTML 形式で正しく作成する。

* HTML コンテンツを含むメールを流通業者が受信したことをコーチがチェックできるようにする。

* メールの件名にチーム番号を含める。

* コーチがメールをチェックした後、その実装を見せる。

## 参考資料

* [Azure Logic Apps のワークフローから Dynamics 365 への接続](https://docs.microsoft.com/ja-jp/azure/connectors/connectors-create-api-crmonline#connector-specific-details)
* [Office 365 Outlook コネクタの使用](https://docs.microsoft.com/ja-jp/azure/connectors/connectors-create-api-office365-outlook)
* [Azure Logic Apps 内でのループ](https://docs.microsoft.com/ja-jp/azure/logic-apps/logic-apps-control-flow-loops)
* [Azure Logic Apps で変数を作成して値を格納、管理する](https://docs.microsoft.com/ja-jp/azure/logic-apps/logic-apps-create-variables-store-values)
* [Azure Logic Apps でデータの操作を実行する](https://docs.microsoft.com/ja-jp/azure/logic-apps/logic-apps-perform-data-operations)
* [Logic Apps のワークフローのアクションとトリガー](https://docs.microsoft.com/ja-jp/azure/logic-apps/logic-apps-workflow-actions-triggers)

## 進捗図

![進捗図: 流通業者への通知](https://serverlessoh.azureedge.net/public/distributor-notification-progress-diagram.jpg)
