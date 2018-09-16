---
layout: getting-started
title: 次にどこへ行こう
---

# {{ page.title }}

{% include toc.html %}

もっと知りたいですか？こちらをご覧ください！

## 最初のElixirプジェクトを作ってみよう

最初のプロジェクトを始めるために、ElixirはMixと呼ばれているビルドツールを提供しています。以下のように実行すれば簡単に新しいプロジェクトを始められます。

```console
$ mix new path/to/new/project
```

以下のガイドに、どうやってElixirのアプリケーションを構築するか、スーパーバイザーツリー、設定、テストなどについて書かれています。このアプリケーションは、キーとバリューのペアをバケツに入れ、複数のノードにわたってバケツを分散させる、分散キーバリューストアとして動作します。

* [Mix と OTP](/getting-started/mix-otp/introduction-to-mix.html)

もし他の開発者が使うためのライブラリを書こうとしているなら、[ライブラリガイドライン](https://hexdocs.pm/elixir/library-guidelines.html) を読むことをお忘れなく。

## メタプログラミング

Elixirは、Elixir自身のメタプログラミングのサポートにより、拡張性のあるとてもカスタマイズしやすいプログラミング言語です。Elixir内の多くのメタプログラミングは、マクロを通して行われます。マクロはいくつかの状況においてとても便利で、特にDSLを記述する際に便利です。マクロの背後にある基本的なメカニズムについて記述した短いガイドを書きました。どのようにマクロを書くか、DSLを作るためにどうやってマクロを使うかについては以下を参照してください。

* [Elixirのメタプログラミング](/getting-started/meta/quote-and-unquote.html)

## コミュニティとその他のリソース

[Learning](/learning.html) セクションでは、Elixirを学びエコシステムを探すための、本、スクリーンキャストやその他のリソースを掲載しています。これら以外にもカンファレンスでのトークやオープンソースプロジェクト、コミュニティによって作られた学習資料など、Elixirを学ぶためのたくさんのリソースがあります。

また、[Elixir自体のソースコード](https://github.com/elixir-lang/elixir) を確認できることを忘れないでください。ソースコードの多くは主に `lib` ディレクトリ内でElixirによって記述されています。さらに[Elixirのドキュメント](/docs.html)も閲覧できます。

## Erlangについて少しだけ

ElixirはErlang仮想マシン上で動作し、遅かれ早かれ、Elixirの開発者は既存のErlangライブラリとのインターフェースが欲しくなるでしょう。ここではErlangの基礎をカバーするオンラインの資料と、一歩先ゆく特徴をリストアップします。

* [Erlangの構文: 速習講座](/crash-course.html)  ではErlangの構文についての簡潔な入門を用意しています。どのコードスニペットもElixirで等しいコードと対に書かれています。これはErlangの構文を知るだけではなく、今まで学んだことを見直すよい機会になるでしょう。

* Erlangの公式ウェブサイトには画像つきの短い [チュートリアル](http://www.erlang.org/course/concurrent_programming.html) があり、Erlangにおいての並行プログラミングでの基本が簡潔に記述されています。

* [Learn You Some Erlang for Great Good!](http://learnyousomeerlang.com/) はErlangの設計思想、標準ライブラリ、ベストプラクティスなどを知ることができる素晴しい入門です。上で紹介した「Erlangの構文: 速習講座」を読んだなら、主に構文について書かれているこの本の最初のいくつかの章は飛ばしてかまいません。あなたが心底楽しめるような内容は [The Hitchhiker's Guide to Concurrency](http://learnyousomeerlang.com/the-hitchhikers-guide-to-concurrency) の章から始まります。
