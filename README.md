# Try C# on .NET

.NET環境を構築して、C#をMacで動かしてみる。

## 試した環境

MacBook Pro (Retina, 13-inch, Early 2015)
macOS Monterey 12.0.1（21A559）


## やったこと

### .NETインストール

https://dotnet.microsoft.com/download からSDKをDLする。
DLページに行くとDirect Linkがあったので、curlでとる。

```zsh
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet % curl https://download.visualstudio.microsoft.com/download/pr/14a45451-4cc9-48e1-af69-0aff75891d09/ff6e83986a2a9a535015fb3104a90a1b/dotnet-sdk-6.0.100-osx-x64.pkg --output dotnet-sdk-6.0.100-osx-x64.pkg
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  328M  100  328M    0     0  5263k      0  0:01:03  0:01:03 --:--:-- 4936k
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet %
```

インストーラーを起動して、GUIでポチポチ

```zsh
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet % open ./dotnet-sdk-6.0.100-osx-x64.pkg
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet %
```

dotnetが入っているかバージョン確認！しても、コマンドが見つからない。

```zsh
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet % dotnet --version
zsh: command not found: dotnet
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet %

```

PATHが通っていないとかそういうわけではないらしい

```zsh
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet % dotnet --version
zsh: command not found: dotnet
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet %
```

DLサイトにあった[チュートリアル](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro?sdk-installed=true)を開いてHello Worldしてみる

→だめ

2日前に同じことをissueに挙げている人がいた。

リンクあるといいなと思ったのでコメントした
https://github.com/dotnet/core/issues/6912

dotnetがインストールされているのはissueで紹介されていたページを参考にするとわかった。

```zsh
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet % /usr/local/share/dotnet/dotnet --version
6.0.100
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet %
```

```zsh
ln -s /usr/local/share/dotnet/dotnet /usr/local/bin
```

シンボリックリンクはって解消。
```zsh
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet % dotnet --version
6.0.100
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet %
```

### Hello World

ドキュメント通りにアプリケーションを作成した。
こちらは問題なく実行できた。

```zsh
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet % dotnet new console --output sample1
テンプレート "コンソール アプリ" が正常に作成されました。

作成後の操作を処理しています...
/Users/vaivailx/work/csharp/try_csharp_on_dotnet/sample1/sample1.csproj で ' dotnet restore ' を実行しています...
  復元対象のプロジェクトを決定しています...
  /Users/vaivailx/work/csharp/try_csharp_on_dotnet/sample1/sample1.csproj を復元しました (157 ms)。
正常に復元されました。

vaivailx@MacBook-Pro-2 try_csharp_on_dotnet % dotnet run --project sample1
Hello, World!
```

ちなみにMacで作れるアプリケーションのテンプレートの種類はCLIでも確認できるようだった。

```zsh
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet % dotnet new --list
これらのテンプレートは、入力:  と一致しました

テンプレート名                     短い名前            言語          タグ
--------------------------  --------------  ----------  --------------------------
ASP.NET Core Empty          web             [C#],F#     Web/Empty
ASP.NET Core gRPC Service   grpc            [C#]        Web/gRPC
ASP.NET Core Web API        webapi          [C#],F#     Web/WebAPI
ASP.NET Core Web App        webapp,razor    [C#]        Web/MVC/Razor Pages
ASP.NET Core Web App (M...  mvc             [C#],F#     Web/MVC
ASP.NET Core with Angular   angular         [C#]        Web/MVC/SPA
ASP.NET Core with React.js  react           [C#]        Web/MVC/SPA
Blazor Server App           blazorserver    [C#]        Web/Blazor
Blazor WebAssembly App      blazorwasm      [C#]        Web/Blazor/WebAssembly/PWA
dotnet gitignore ファイル       gitignore                   Config
dotnet ローカル ツール マニフェスト ...  tool-manifest               Config
EditorConfig ファイル           editorconfig                Config
global.json ファイル            globaljson                  Config
MSTest Test Project         mstest          [C#],F#,VB  Test/MSTest
MVC ViewImports             viewimports     [C#]        Web/ASP.NET
MVC ViewStart               viewstart       [C#]        Web/ASP.NET
NuGet Config                nugetconfig                 Config
NUnit 3 Test Item           nunit-test      [C#],F#,VB  Test/NUnit
NUnit 3 Test Project        nunit           [C#],F#,VB  Test/NUnit
Protocol Buffer File        proto                       Web/gRPC
Razor Class Library         razorclasslib   [C#]        Web/Razor/Library
Razor Component             razorcomponent  [C#]        Web/ASP.NET
Razor Page                  page            [C#]        Web/ASP.NET
Web 構成                      webconfig                   Config
Worker Service              worker          [C#],F#     Common/Worker/Web
xUnit Test Project          xunit           [C#],F#,VB  Test/xUnit
クラス ライブラリ                   classlib        [C#],F#,VB  Common/Library
コンソール アプリ                   console         [C#],F#,VB  Common/Console
ソリューション ファイル                sln                         Solution

vaivailx@MacBook-Pro-2 try_csharp_on_dotnet %
```

