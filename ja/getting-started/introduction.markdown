---
layout: getting-started
title: Introduction
redirect_from: /getting_started/1.html
---

# {{ page.title }}

{% include toc.html %}

さあ、一緒に Elixir を盛り上げていきましょう！

このチュートリアルでは、あなたが Elixir を始めるにあたって重要となる文法、モジュール定義、普遍的なデータ構造の扱い方などの基礎についてお伝えします。この章では、Elixir を確実にインストールし、 "IEx" と呼ばれるインタラクティブ・シェルが正常に動作するように手順をご案内します。

必要構成

  * Elixir - Version 1.5.0 以上
  * Erlang - Version 19.0 以上


さあ、はじめましょう！

このチュートリアル、またはウェブサイトに誤りを見つけた場合、[バグ報告、もしくは Issue tracker 宛に Pull Request ](https://github.com/elixir-lang/elixir-lang.github.com)をお願いします。

> このチュートリアルは電子書籍(EPUB形式)でもご覧になれます。
>
>   * [Getting started guide](https://repo.hex.pm/guides/elixir/elixir-getting-started-guide.epub)
>   * [Mix and OTP guide](https://repo.hex.pm/guides/elixir/mix-and-otp.epub)
>   * [Meta-programming guide](https://repo.hex.pm/guides/elixir/meta-programming-in-elixir.epub)

## インストール

もしも Elixir のインストールがまだでしたら、[Elixir のインストール](/install.html)を参考にしてください。そうしましたら、`elixir --version` で現在のバージョンを確認できます。

## インタラクティヴ・モード

Elixir のインストールが終わりましたら、 `iex`, `elixir`, `elixirc` コマンドが実行できるようになります。ソースコードからコンパイルしたもの、もしくはパッケージ版をご利用の場合は、これらコマンドが `bin` ディレクトリ内にあります。

それでは `iex` コマンド (Windows をお使いの場合は `iex.bat`) を実行してインタラクティヴ・モードで起動してみましょう。インタラクティヴ・モードでは、Elixir のどんな式でも入力することができ、その結果を得られます。試しに簡単な式で準備運動してみましょう。

`iex` コマンドを起動したら、以下のように入力してみてください。

```iex
Erlang/OTP 19 [erts-8.1] [source] [64-bit] [smp:4:4] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]

Interactive Elixir (1.4.0) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)> 40 + 2
42
iex(2)> "hello" <> " world"
"hello world"
```

あなたの環境で表示されるバージョンはここで示しているものと少し異なるかも知れませんが、特に問題はないので気になさらず進めてください。今後、 `iex` ではコードに着目していきましょう。`iex` を終了したい時は、 `Ctrl + C` を二度押してください。

問題なさそうですね。それでは進めて行きましょう！インタラクティヴ・シェルを使い、次章からは皆さんお馴染みの言語構文や基本的な型についてもふんだんに触れていきたいと思います。

> Note: Windows をお使いの場合、あなたが使用するコンソールによっては `iex.bat --werl` をお使い頂けるかも知れません。

> Note: `iex` 内でスクリプトファイルを実行するには、 `iex -S SCRIPTNAME` とします。あとで [Mix](/getting-started/mix-otp/introduction-to-mix.html) や Elixir ビルドツール、そしてコンパイル方法とそのアプリケーションを `iex -S mix run` で起動する方法についても学んでいきます。

## スクリプトの実行

基本が分かってくると、簡単なプログラムを書いてみたくなることでしょう。それでは、その願いを叶える為に、まず以下のコードをファイルに入力してみましょう。

```elixir
IO.puts "Hello world from Elixir"
```

`simple.exs` というファイル名で保存し、 `elixir` コマンドで実行してみてください。如何でしょう。

```console
$ elixir simple.exs
Hello world from Elixir
```

後ほど Elixir コードのコンパイル方法と Mix ビルドツール ([Mix & OTP ガイド](/getting-started/mix-otp/introduction-to-mix.html)) の使い方を学びましょう。今はとりあえず [第2章](/getting-started/basic-types.html) に進みます。

## 質問方法

この入門ガイドを終えたあなたも、よく抱かれる疑問を質問をしたいその一人であることでしょう。それも学習プロセスのうちです。あなたが Elixir を学ぶにあたって疑問や問題を質問できる場はたくさんあります。

  * [#elixir-lang on freenode IRC (英語)](irc://irc.freenode.net/elixir-lang)
  * [Elixir on Slack (英語)](https://elixir-slackin.herokuapp.com/)
  * [Elixir Forum (英語)](http://elixirforum.com)
  * [elixir (英語 StackOverflow)](https://stackoverflow.com/questions/tagged/elixir)
  * [elixir (日本語 StackOverflow)](https://ja.stackoverflow.com/questions/tagged/elixir)

質問する際は以下の二点を念頭においてください。

  * 「Elixir で××のやり方を教えてください」や「Elixir で△△の解決法を教えてください」といった質問はおやめください。それはつまり、何かある特定の解決法を求めるのではなく、今あなたが直面している問題を述べてくださいという意味です。的確な回答をもらう為に、その問題の背景や状況を詳しく記して、なるべく客観的に説明してください。

  * 何かが意図した通りに動作しない場合、把握できる限りの情報を含め記してください。例えば Elixir のバージョン、問題のコードやスタックトレースに表示されるエラーメッセージの抜粋などです。コードを抜粋する際は [Gist](https://gist.github.com/) などを利用するといいでしょう。
