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

### MAUI をためす

#### MAUI とは

[Introducing .NET Multi-platform App UI](https://devblogs.microsoft.com/dotnet/introducing-net-multi-platform-app-ui/)
にあるとおり

* Cross-platform
* native ui
* single project
* single codebase

という特徴のもの。

.netを使ってmacでもGUIアプリケーションを作れる。

これに関連するものとして、maui-checkというMAUIのビルド環境として必要なものが揃っているか確認し、
不足があればインストールしてくれるものがあった。

https://github.com/Redth/dotnet-maui-check

#### ためしてみる

MAUIは環境の要件としてVisual Studio For Macをいれていて、かつなんかいろいろインストールしてとかいてあった。
が、このツールは、そういったものをもろもろチェックしてインストールしてくれるらしい。
じゃあ、Visual Studio For Macいれなくても、これでいけるんじゃないか？と思い、
これでインストールして、サンプルアプリを動かしてみる。


https://github.com/davidortinau/WeatherTwentyOne にあるとおり、 maui-checkをインストール

```zsh
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet % dotnet tool install -g redth.net.maui.check
ツール ディレクトリ '/Users/vaivailx/.dotnet/tools' は現在、PATH 環境変数にありません。
zsh を使用している場合、次のコマンドを実行してプロファイルに追加できます:

cat << \EOF >> ~/.zprofile
# .NET Core SDK tools
export PATH="$PATH:/Users/vaivailx/.dotnet/tools"
EOF

`zsh -l` を実行して現在のセッションで利用できるようにします。

これは、次のコマンドを実行することによってのみ、現行のセッションに追加できます:

export PATH="$PATH:/Users/vaivailx/.dotnet/tools"

次のコマンドを使用してツールを呼び出せます。maui-check
ツール 'redth.net.maui.check' (バージョン '0.10.0') が正常にインストールされました。
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet %
```

パスを通して実行

```zsh
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet % source ~/.zprofile
vaivailx@MacBook-Pro-2 try_csharp_on_dotnet % maui-check
      _   _   _____   _____     __  __      _      _   _   ___
     | \ | | | ____| |_   _|   |  \/  |    / \    | | | | |_ _|
     |  \| | |  _|     | |     | |\/| |   / _ \   | | | |  | |
  _  | |\  | | |___    | |     | |  | |  / ___ \  | |_| |  | |
 (_) |_| \_| |_____|   |_|     |_|  |_| /_/   \_\  \___/  |___|

🚑 .NET MAUI Check v0.10.0.0 💉
───────────────────────────────────────────────────────────────────────────────────
This tool will attempt to evaluate your .NET MAUI development environment.
If problems are detected, this tool may offer the option to try and fix them for
you, or suggest a way to fix them yourself.

Thanks for choosing .NET MAUI!
───────────────────────────────────────────────────────────────────────────────────
⏳ Synchronizing configuration... ok
⏳ Scheduling appointments... ok

🔎 OpenJDK 11.0 Checkup...

───────────────────────────────────────────────────────────────────────────────────
💉 Recommendation: Install OpenJDK11
───────────────────────────────────────────────────────────────────────────────────

🔔 Attempt to fix? [y/n] (y): y

...

```

なんか足りないものを検出していろんなものをいれてくれた。

* androidのSDK
* open jdk
* emulator
* etc..

結構時間かかるね。
10分以上は経っているな

```zsh
✔ Congratulations, everything looks great!

Press enter to exit...

vaivailx@MacBook-Pro-2 try_csharp_on_dotnet %
```

気づけば終わっていた。

が、[サンプルアプリ](https://github.com/davidortinau/WeatherTwentyOne)をクローンしてビルドをするもエラー。
ビルド`dotnet build src/WeatherTwentyOne.sln`をするもエラーでまくり。
試行錯誤したが、もし動くのなら試してみたいというところなので、いったん手を止める。
そもそもF#をさわりたくて環境構築し始めたわけで。
