---
title: "Development"
section: development
layout: default
---

# {{ page.title }}

このセクションでは、Elixir が歩んできたこれまでの過去と、今後の開発における未来についてお話しましょう。

2012 年。Elixir は、ソフトウェアコンサルティング事業を行っている[Plataformatec](http://plataformatec.com.br/)社にて、その共同設立者のうち一人であるジョゼ・ヴァリム(José Valim)氏の総指揮のもと、研究開発プロジェクトとして作成されました。Elixir は、生産性と保守性の高いコード、そして信頼性の高いソフトウェア開発を目標にして生まれた言語です。

Elixir は Erlang 仮想マシン上で実行されます。高い拡張性と堅牢性を兼ね備えており、パフォーマンスの為に高コストを費やすことなくそれらを実現できること、そして可能な際には必ず広範なエコシステムを提供することを目標として設計されています。

Elixir のソースコードは[Apache 2 ライセンス](https://github.com/elixir-lang/elixir/blob/master/LICENSE)の下にあり、Aleksei Magusev, Andrea Leopardi, Eric Meadows-Jönsson, James Fish, José Valim, そして Michał Muskała らの Elixir Core team によって管理されています。Elixir team のメンバー達は、誰かひとりが抱える負担を大きくしてしまうことのないよう、全員が足並みを揃え協力しあって仕事に取り組んでいます。ソースコードやその他の情報はこちらからご覧いただけますので参照してください。[Elixir-Lang ソースコードリポジトリ](https://github.com/elixir-lang/elixir). 

言語開発についてはオープンです。規約を遵守してソースコードを利用し、開発してください。次のリリースまでに向けて立てられた不具合修正の計画や実装予定の機能などは Issue を参照してください ([in the issues tracker](https://github.com/elixir-lang/elixir/issues)) 。Elixir フォーラム内の [Elixir News](https://elixirforum.com/c/elixir-news) はもちろんのこと、主要な機能や変更などについてはメーリングリスト ([the Elixir mailing list](https://groups.google.com/group/elixir-lang-core)) からも皆さんにお知らせします。

Elixir v1.0 は 2014 年 9 月にリリースされました。それ以降、マイナーバージョンアップを半年に一度の頻度でリリースしており、毎年度の 1 月と 7 月あたりになります。新バージョンリリースの際には [Official blog](https://elixir-lang.org/blog/) にて変更履歴や主な変更などの概要といった内容とともにアナウンスがあります。互換性や廃止された施策についてはこちらに纏めてあります [Compatibility and Deprecation Policies](https://hexdocs.pm/elixir/compatibility-and-deprecations.html#content) 。

Since v1.0, the language development has become more focused. We believe there is a limited amount of features a language can provide without hindering its learning and without causing fragmentation in the community. Therefore the Elixir team focuses on language features that:

  1. are necessary for developing the language itself
  2. bring important concepts/features to the community in a way its effect can only be maximized or leveraged by making it part of the language

To remain focused, Elixir trusts its ecosystem to bring diversity and broaden its use cases to a wider audience. Therefore the language was designed to be extensible: the constructs available to build the language are also available for developers to extend the language and bring it to different domains. Projects such as [the Phoenix web framework](http://phoenixframework.org) and [the Nerves embedded framework](http://nerves-project.org) are two of such examples.

Elixir also relies on a vibrant community to support its growth. The community is behind the meetups, events, learning resources, open source projects, and more. See the sidebar, the [Learning Resources](/learning.html) and [the Hex Package Manager website](https://hex.pm/) for some examples and more information.

The best way to support the language is by getting involved in its community and contributing to the ecosystem.

Welcome!
