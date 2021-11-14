# Try C# on .NET

.NET環境を構築して、C#をMacで動かしてみる。

## 試した環境

MacBook Pro (Retina, 13-inch, Early 2015)
macOS Monterey 12.0.1（21A559）


## やったこと

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
