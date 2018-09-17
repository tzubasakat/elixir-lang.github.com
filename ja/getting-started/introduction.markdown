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

Open up `iex` and type the following expressions:

```iex
Erlang/OTP 19 [erts-8.1] [source] [64-bit] [smp:4:4] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]

Interactive Elixir (1.4.0) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)> 40 + 2
42
iex(2)> "hello" <> " world"
"hello world"
```

Please note that some details like version numbers may differ a bit in your session; that's not important. From now on `iex` sessions will be stripped down to focus on the code. To exit `iex` press `Ctrl+C` twice.

It seems we are ready to go! We will use the interactive shell quite a lot in the next chapters to get a bit more familiar with the language constructs and basic types, starting in the next chapter.

> Note: if you are on Windows, you can also try `iex.bat --werl` which may provide a better experience depending on which console you are using.

> Note: if you want to find and execute a given script in PATH so it will be loaded in `iex` use: `iex -S SCRIPTNAME`.  Later you'll learn about [Mix](/getting-started/mix-otp/introduction-to-mix.html), Elixir's build tool, and how you can compile and load entire applications with `iex -S mix run`. See [Supervisor and application](/getting-started/mix-otp/supervisor-and-application.html) for more details.

## Running scripts

After getting familiar with the basics of the language you may want to try writing simple programs. This can be accomplished by putting the following Elixir code into a file:

```elixir
IO.puts "Hello world from Elixir"
```

Save it as `simple.exs` and execute it with `elixir`:

```console
$ elixir simple.exs
Hello world from Elixir
```

Later on we will learn how to compile Elixir code (in [Chapter 8](/getting-started/modules-and-functions.html)) and how to use the Mix build tool (in the [Mix & OTP guide](/getting-started/mix-otp/introduction-to-mix.html)). For now, let's move on to [Chapter 2](/getting-started/basic-types.html).

## Asking questions

When going through this getting started guide, it is common to have questions; after all, that is part of the learning process! There are many places you could ask them to learn more about Elixir:

  * [#elixir-lang on freenode IRC](irc://irc.freenode.net/elixir-lang)
  * [Elixir on Slack](https://elixir-slackin.herokuapp.com/)
  * [Elixir Forum](http://elixirforum.com)
  * [elixir tag on StackOverflow](https://stackoverflow.com/questions/tagged/elixir)

When asking questions, remember these two tips:

  * Instead of asking "how to do X in Elixir", ask "how to solve Y in Elixir". In other words, don't ask how to implement a particular solution, instead describe the problem at hand. Stating the problem gives more context and less bias for a correct answer.

  * In case things are not working as expected, please include as much information as you can in your report, for example: your Elixir version, the code snippet and the error message alongside the error stacktrace. Use sites like [Gist](https://gist.github.com/) to paste this information.
