# Development Environment Configuration

Please ensure your machine conforms to these prerequisites.

* A modern laptop running Windows 10, Mac OSX 10.12 or
higher, or one of
[these Ubuntu versions](https://github.com/Azure/azure-functions-core-tools#linux)

* Your preferred IDE (integrated development environments), like
Visual Studio Code or Visual Studio:
    * If using Visual Studio for Windows, make sure you have the
  [latest Visual Studio 2019](https://visualstudio.microsoft.com/)
  with the `Azure development workload` selected,
  and the most recent version of the
  [Azure Functions and Web Jobs Tools extension](https://docs.microsoft.com/azure/azure-functions/functions-develop-vs#check-your-tools-version)

    * If using Visual Studio Code in Windows, OSX, or Linux make sure you
  have the latest Visual Studio Code version for your OS, and the
  [Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)

## Language specific prerequisites

Depending on the language your team uses, there are additional prerequisites that your machine will need to have. Please review these language specific prerequisites to ensure your machine is ready for the open hack.  
  
### C# .NET Core  
  
* Either [Visual Studio 2019](https://visualstudio.microsoft.com/)

or

* [Visual Studio Code](https://code.visualstudio.com/) on one of the [supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms)
* [Azure Functions Core Tools](https://docs.microsoft.com/azure/azure-functions/functions-run-local#v3) version 3x
* Visual Studio Code Extensions:
    * [Azure Functions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)
    * [C# Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)

> .Net 5.0 has not been validated for these OpenHack challenges. Please use .NET Core 3.1. Refer to [supported languages](https://docs.microsoft.com/azure/azure-functions/supported-languages) to determine when .Net Core 5.0 is no longer in preview state.

### Java/Maven

* [Java Developer Kit](https://aka.ms/azure-jdks) version 8
* [Apache Maven](https://maven.apache.org/) version 3.0 or later
* [Azure CLI](https://docs.microsoft.com/cli/azure)
* [Azure Functions Core Tools](https://docs.microsoft.com/azure/azure-functions/functions-run-local#v3) version 3.x

### JavaScript

* [Visual Studio Code](https://code.visualstudio.com/) on one of the [supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms)  

* [Azure Functions Core Tools](https://docs.microsoft.com/azure/azure-functions/functions-run-local#v3) version 3.x  

* [Node.js](https://nodejs.org/) Active LTS and Maintenance LTS versions (8.11.1 and 10.14.1 recommended)  

* Visual Studio Code Extension:
    * [Azure Functions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)  
  
### Python  

#### Previous Versions  

If you have 3.6.x or 3.7.x you **should** have no issues with those versions, just be certain to select the correct version when creating your function apps at Azure.  

#### Use a VM instead of multiple versions  

It is recommended you do not do a side-by-side installation of a new python version for this challenge.  To be clean and avoid potential issues, consider using a low-cost VM running on linux at Azure and install the latest python tools there.  

#### Use VSCode with the Azure Functions Extension  

It is very easy to work with VSCode with python functions at Azure.  Although you may be new to VSCode, it is recommended due to the high availability of extensions that can easily run (locally) and publish Azure functions to your integrated Azure subscription.  

* [Python 3.8.x](https://www.python.org/downloads/)  

    * Using VSCode with Azure Functions extension makes it easy to select the compiler. language, and project and integrate directly to your function app at Azure, including deployment.  

    * VS Code users on Windows, in the past, python interpreter selection can be troublesome. Review [Python in VS Code environments](https://code.visualstudio.com/docs/languages/python#_environments) for assistance with this if you run into issues.  

* [VSCode](https://code.visualstudio.com/download)  

* [VSCode Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)  

* [Azure Functions Core Tools](https://docs.microsoft.com/azure/azure-functions/functions-run-local#v3) version 3x.  You need this to run/test locally.  

* [Azure CLI](https://docs.microsoft.com/cli/azure)

* Recommended for Mac OSX and Linux users to install  [Azurite v2](https://www.nuget.org/packages/Azurite/)  

* [VSCode Azure Storage extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestorage)  

# 開発環境の構成

使用するマシンの前提条件は以下のとおりです。

* Windows 10、Mac OS X 10.12 以降、[こちらに掲載されているバージョンの Ubuntu (英語)](https://github.com/Azure/azure-functions-core-tools#linux) のいずれかが実行されている最新のノート PC

* Visual Studio Code や Visual Studio などのお好みの IDE (統合開発環境)
    * Windows で Visual Studio を使用する場合は、`Azure 開発ワークロード`をインストールした[最新版の Visual Studio 2019](https://visualstudio.microsoft.com/ja/vs/)、および最新版の  [Azure Functions と WebJob ツールの拡張機能](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-develop-vs#check-your-tools-version)

    * Windows、OS X、Linux で Visual Studio Code を使用する場合は、各 OS 用の最新版の Visual Studio Code と
  [Azure Functions 拡張機能 (英語)](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)

## 言語固有の前提条件

チームで使用する言語によって、以下の前提条件が加わります。OpenHack で使用するマシンが言語固有の前提条件を満たしていることを確認してください。

### C# .NET Core

* [Visual Studio 2019](https://visualstudio.microsoft.com/ja/vs/)

または

* [サポート対象のプラットフォーム (英語)](https://code.visualstudio.com/docs/supporting/requirements#_platforms) のいずれかで動作する [Visual Studio Code (英語)](https://code.visualstudio.com/)
* [Azure Functions Core Tools](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-run-local#v3) バージョン 3.x
* Visual Studio Code 拡張機能
    * [Azure Functions (英語)](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)
    * [C# 拡張機能 (英語)](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)

> .Net Core 3.0 は、この OpenHack の課題に関する検証を行っていません。.NET Core 2.2 を使用してください。

### Java/Maven

* [Java Developer Kit](https://docs.microsoft.com/ja-jp/java/azure/jdk/?view=azure-java-stable) バージョン 8
* [Apache Maven (英語)](https://maven.apache.org/) バージョン 3.0 以降
* [Azure CLI](https://docs.microsoft.com/cli/azure)
* [Azure Functions Core Tools](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-run-local#v3) バージョン 3.x 以降

### JavaScript

* [サポート対象のプラットフォーム (英語)](https://code.visualstudio.com/docs/supporting/requirements#_platforms) のいずれかで動作する [Visual Studio Code (英語)](https://code.visualstudio.com/)
* [Azure Functions Core Tools](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-run-local#v3) バージョン 3.x
* [Node.js (英語)](https://nodejs.org/) Active LTS および Maintenance LTS バージョン (8.11.1 および 10.14.1 を推奨)
* Visual Studio Code 拡張機能
    * [Azure Functions (英語)](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)

### Python

* [Python 3.6.x (英語)](https://www.python.org/downloads/)
    * Windows の場合は、[既知の問題 (英語)](https://github.com/protocolbuffers/protobuf/issues/5046) を考慮し、**3.6.8 64-bit 版**の使用を強くお勧めします。
    * Windows で VS Code を使用する場合、Python インタープリターのインストールに手間取る可能性があります。これについては、[VS Code 環境における Python (英語)](https://code.visualstudio.com/docs/languages/python#_environments) に関するガイドを参照してください。
* [Azure Functions Core Tools](https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-run-local#v3) バージョン 3.x 以降
* [Azure CLI](https://docs.microsoft.com/ja-jp/cli/azure/install-azure-cli?view=azure-cli-latest) バージョン 2.x 以降
* Mac OS X および Linux を使用する場合は [Azurite v2 (英語)](https://www.nuget.org/packages/Azurite/) のインストールを推奨
