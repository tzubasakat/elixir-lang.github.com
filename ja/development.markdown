---
title: "Development"
section: development
layout: default
---

# {{ page.title }}

このセクションでは、Elixir が歩んできたこれまでの過去と、今後の開発における未来についてお話しましょう。

2012 年。Elixir は、ソフトウェアコンサルティング事業を行っている[Plataformatec](http://plataformatec.com.br/)社にて、その共同設立者のうち一人であるジョゼ・ヴァリム(José Valim)氏の総指揮のもと、研究開発プロジェクトとして誕生しました。Elixir は、生産性と保守性の高いコード、そして信頼性の高いソフトウェア開発を目標にして生まれた言語です。

Elixir は Erlang 仮想マシン上で実行されます。高い拡張性と堅牢性を兼ね備えており、パフォーマンスの為に高コストを費やすことなくそれらを実現できること、そして可能な際には必ず広範なエコシステムを提供することを目標として設計されています。

Elixir のソースコードは[Apache 2 ライセンス](https://github.com/elixir-lang/elixir/blob/master/LICENSE)の下にあり、Aleksei Magusev, Andrea Leopardi, Eric Meadows-Jönsson, James Fish, José Valim, そして Michał Muskała らの Elixir Core team によって管理されています。Elixir team のメンバー達は、誰かひとりが抱える負担を大きくしてしまうことのないよう、全員が足並みを揃え協力しあって仕事に取り組んでいます。ソースコードやその他の情報はこちらからご覧いただけますので参照してください。[Elixir-Lang ソースコードリポジトリ](https://github.com/elixir-lang/elixir). 

Elixir v1.0 は 2014 年 9 月にリリースされました。それ以降、マイナーバージョンアップを半年に一度の頻度でリリースしており、毎年度の 1月と 7 月あたりになります。新しいリリースは購読専用の [アナウンスメーリングリスト](https://groups.google.com/group/elixir-lang-ann) にて完全なCHANGELOGと一緒にアナウンスされます。すべてのセキュリティリリースは ["[security]"タグが付けられています](https://groups.google.com/forum/#!searchin/elixir-lang-ann/%5Bsecurity%5D%7Csort:date)。 セキュリティ脆弱性については [elixir-security@googlegroups.com](mailto:elixir-security@googlegroups.com) に報告するべきです。互換性や廃止された施策についてはこちらに纏めてありますので参考にしてください [Compatibility and Deprecation Policies](https://hexdocs.pm/elixir/compatibility-and-deprecations.html#content) 。

v1.0 以降、この言語の開発は小さく一貫したコアを提供することに集中するようになりました。Elixir チームは以下の言語仕様に焦点をあてています。

  1. 言語それ自体の開発の為に必要不可欠であること
  2. その言語が持ってこそ最大に活かせる機能において、コミュニティに重要な特徴的概念をもたらすこと

言語開発についてはオープンです。規約を遵守してソースコードを利用し、開発してください。次のリリースまでに向けて立てられた不具合修正の計画や実装予定の機能などは Issue を参照してください ([in the issues tracker](https://github.com/elixir-lang/elixir/issues)) 。Elixir フォーラム内の [Elixir News](https://elixirforum.com/c/elixir-news) はもちろんのこと、主要な機能や変更などについてはメーリングリスト ([the Elixir mailing list](https://groups.google.com/group/elixir-lang-core)) からも皆さんにお知らせします。 

コミュニティーメンバーはElixirへの新機能の提案を歓迎します。提案を送る前に、どのやり方がベストかについてコミュニティからフィードバックを集めることが推奨されます。しかしながら、Elixir Coreチーム提案する場合は、Elixirのメーリングリストを使わなければなりません。これには議論や提案の改善がよく含まれます。Elixir Coreチームは提案を受け入れるか拒否するかについて最終的な判断をします。コミュニティーメンバーはコミュニティから支持を得ることが推奨されますが、人気があることが提案が受け入れられることを意味するものではありません。

Elixir 自らが持つエコシステムを、その多様性の生産や使用事例の拡張を幅広い人々に対して委ねることが、関心を持ち続けてもらう為に必要となります。それ故にこの言語は拡張性を考慮して設計されており、言語構築に利用できる構成物は、開発者が言語を拡張する為に利用する事も、異分野へ応用する事も可能です。[the Phoenix web framework](http://phoenixframework.org) や [the Nerves embedded framework](http://nerves-project.org) などがその例でしょう。

コミュニティでは、ミートアップ、イベント、学習リソース、オープンソースプロジェクト等など、様々な活動を支援しています。そんな活気あふれるコミュニティの力を、Elixir は更なる発展の為にも必要としています。サイドメニューや [Learning Resources](/learning.html) 、そして [the Hex Package Manager website](https://hex.pm/) 等もぜひご覧ください。詳細な情報もそちらでご入手いただけます。

言語を支援する為に最も最良な方法、それはコミュニティに参加してそのエコシステムに貢献することです。

さあ、一緒に Elixir を盛り上げていきましょう！
