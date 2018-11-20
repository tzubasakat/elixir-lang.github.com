---
layout: getting-started
title: 基本演算子
---

# {{ page.title }}

{% include toc.html %}

[前章](/getting-started/basic-types.html)では、Elixir で使用できる算数の演算子 `+`, `-`, `*`, `/` に加えて、除算の商と剰余を求める `div/2` と `rem/2` 関数を見てきました。

Elixir はリストを操作する為に `++` と `--` も使えるようになっています。

```iex
iex> [1, 2, 3] ++ [4, 5, 6]
[1, 2, 3, 4, 5, 6]
iex> [1, 2, 3] -- [2]
[1, 3]
```

文字列の連結には `<>` が使われます。

```iex
iex> "foo" <> "bar"
"foobar"
```

Elixir は `or`、 `and` 、 `not` など3つの論理演算子も用意しています。これらの演算子は第一引数として `true` か `false` の論理値を期待しています。

```iex
iex> true and true
true
iex> false or is_atom(:example)
true
```

第一引数に論理値以外を渡すと例外が発生します。

```iex
iex> 1 and true
** (BadBooleanError) expected a boolean on left-side of "and", got: 1
```

`or` と `and` は短絡評価をする演算子です。左辺の結果を確かめるまでもないなら、右辺だけを返します。

```iex
iex> false and raise("This error will never be raised")
false
iex> true or raise("This error will never be raised")
true
```

Note: もしあなたが Erlang エンジニアなら、Elixir の `and` と `or` は Erlang における `andalso` と `orelse` に対応させることでしょう。

これら論理演算子とは対比して、如何なる型の引数でも受け取れる `||` や `&&` 、`!` もあります。これらの演算子は `false` と `nil` を除く値のすべてを `true` として評価します。

```iex
# or
iex> 1 || true
1
iex> false || 11
11

# and
iex> nil && 13
nil
iex> true && 17
17

# !
iex> !true
false
iex> !1
false
iex> !nil
true
```

大雑把な言い方をすると、論理値を用いる時に `and` や `or` 、 `not` を使い、もし引数のどれかが論理値でない時は `&&` や `||` 、 `!` を使うといいでしょう。

比較演算子 `==` 、 `!=` 、 `===` 、 `!==` 、 `<=` 、 `>=` 、 `<` 、 `>` も用意されています。

```iex
iex> 1 == 1
true
iex> 1 != 2
true
iex> 1 < 2
true
```

`==` と `===` の違いは、整数と浮動小数点数を比べる際に後者の方がより厳格であることです。

```iex
iex> 1 == 1.0
true
iex> 1 === 1.0
false
```

Elixir では二つの異なる型を比較できます。

```iex
iex> 1 < :atom
true
```

これはプラグマティズム(実用主義)が理由です。よって異なる型をソートする際に、その違いを心配する必要がないのです。

    number < atom < reference < function < port < pid < tuple < map < list < bitstring

実際にこの順序を暗記する必要はなく、そういうものがあるという事だけを覚えていれば十分です。

演算子とその整列順に関する情報は、[演算子について](https://hexdocs.pm/elixir/operators.html)を参照してください。

次章では、マッチ演算子 `=` を用いたパターンマッチングを取り上げていきます。
