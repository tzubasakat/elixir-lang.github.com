---
layout: getting-started
title: パターン・マッチング
---

# {{ page.title }}<span hidden>.</span>

{% include toc.html %}

この章で私たちは、 Elixir における `=` 演算子が実際にマッチ演算子である事と、それをデータ構造の中でパターンマッチに使用する為の使い方を案内します。終盤では、事前に指定された値へアクセスする為に使われるピン演算子 `^` について学びます。

## マッチ演算子

私たちは、変数を定義する為に `=` 演算子を何度か使っています。

```iex
iex> x = 1
1
iex> x
1
```

Elixir では、実際のところ `=` 演算子は "マッチ演算子" と呼ばれます。その理由を見ていきましょう。

```iex
iex> 1 = x
1
iex> 2 = x
** (MatchError) no match of right hand side value: 1
```

`1 = x` は有効な式であることに留意してください。さらに、左辺と右辺の両方が 1 に対して等しいのでマッチしています。その一方がマッチしない時は `MatchError` が起こります。

変数は、それが `=` の左辺にある時だけ代入することができます。

```iex
iex> 1 = unknown
** (CompileError) iex:1: undefined function unknown/0
```

事前に定義された `unknown` という変数が存在しない以上、Elixir はあなたが `unknown/0` という関数の呼び出しを試みているものと考えますが、そのような関数は存在していません。

## パターン・マッチ

マッチ演算子は単純にマッチングする為だけのものではなく、より複雑なデータ型を解体する為にも便利なものです。例えば、タプルでパターンマッチを使えます。

```iex
iex> {a, b, c} = {:hello, "world", 42}
{:hello, "world", 42}
iex> a
:hello
iex> b
"world"
```

一方がマッチしないのならパターンマッチは失敗します。例えば、それはタプルが違うサイズである等という時に起こります。

```iex
iex> {a, b, c} = {:hello, "world"}
** (MatchError) no match of right hand side value: {:hello, "world"}
```

さらには異なる型を比較しようとすることでも起こります。

```iex
iex> {a, b, c} = [:hello, "world", 42]
** (MatchError) no match of right hand side value: [:hello, "world", 42]
```

もっと面白いことに、値を指定してパターンマッチを使うこともできます。以下の例では、右辺がタプルかつその最初の要素はアトムの `:ok` である時にだけ、左辺が右辺とマッチすることを名言しています。

```iex
iex> {:ok, result} = {:ok, 13}
{:ok, 13}
iex> result
13

iex> {:ok, result} = {:error, :oops}
** (MatchError) no match of right hand side value: {:error, :oops}
```

リストでもパターンマッチは出来ます。

```iex
iex> [a, b, c] = [1, 2, 3]
[1, 2, 3]
iex> a
1
```

リストはそれ自身の首尾と後尾にマッチすることもサポートしています。

```iex
iex> [head | tail] = [1, 2, 3]
[1, 2, 3]
iex> head
1
iex> tail
[2, 3]
```

`hd/1` と `tl/1` 関数と同様に、首尾と後尾が空のリストにはマッチできません。

```iex
iex> [h | t] = []
** (MatchError) no match of right hand side value: []
```

`[head | tail]` 形式はパターンマッチだけで使われるものではなく、リストの先頭に値を付加することにも使えます。

```iex
iex> list = [1, 2, 3]
[1, 2, 3]
iex> [0 | list]
[0, 1, 2, 3]
```

パターンマッチは、開発者がタプルやリストのようなデータ構造を解体するのを容易にしてくれます。次章で見ていくことになるものとしては、Elixir における再起処理の基礎と、マップやバイナリのようにそれを異なる型へ適用するというものもあります。

## ピン演算子

Elixir の変数は再代入ができます。

```iex
iex> x = 1
1
iex> x = 2
2
```

既存の変数に対して再代入するのではなく、パターンマッチをしたい時には、ピン演算子 `^` を使うことができます。

```iex
iex> x = 1
1
iex> ^x = 2
** (MatchError) no match of right hand side value: 2
iex> {y, ^x} = {2, 1}
{2, 1}
iex> y
2
iex> {y, ^x} = {2, 2}
** (MatchError) no match of right hand side value: {2, 2}
```

上での変数 x には既に 1 という値が代入されています。最後の部分の例については、これまで以下のように書いてきたものと同じです。

```
iex> {y, 1} = {2, 2}
** (MatchError) no match of right hand side value: {2, 2}
```

ある変数がひとつのパターンにおいて二つ以上に言及されると、それに対するリファレンスの全てがそのパターンにマッチしなくてはなりません。

```iex
iex> {x, x} = {1, 1}
{1, 1}
iex> {x, x} = {1, 2}
** (MatchError) no match of right hand side value: {1, 2}
```

場合によってはパターンにおける値を気にしたくないことがあるでしょう。そういった時は、`_` という変数へ値を代入するという慣習的な方法を使います。

```iex
iex> [h | _] = [1, 2, 3]
[1, 2, 3]
iex> h
1
```

変数 `_` はそこから読み出すことができない点で特殊なものです。試しにやってみたら CompileError が返ってくることでしょう。

```iex
iex> _
** (CompileError) iex:1: invalid use of _. "_" represents a value to be ignored in a pattern and cannot be used in expressions
```

パターンマッチはとても有力な構造を表現できますが、その使い方には制限があります。例えば、マッチ演算子の左辺側で関数を呼び出すことができません。

```iex
iex> length([1, [2], 3]) = 3
** (CompileError) iex:1: cannot invoke remote function :erlang.length/1 inside match
```

パターンマッチの入門はこれで終わりです。次の章で理解していくことになりますが、パターンマッチは多くの言語においてとても普遍的な構造なのです。
