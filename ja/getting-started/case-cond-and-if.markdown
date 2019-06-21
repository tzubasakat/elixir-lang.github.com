---
layout: getting-started
title: case, cond, and if
---

# {{ page.title }}

{% include toc.html %}

この章では、 case, cond, if といった制御構造について学んでいきます。

## `case`

`case` を使うと、いくつかあるパターンのいずれかにマッチするまで値を比較することができます。

```iex
iex> case {1, 2, 3} do
...>   {4, 5, 6} ->
...>     "This clause won't match"
...>   {1, x, 3} ->
...>     "This clause will match and bind x to 2 in this clause"
...>   _ ->
...>     "This clause would match any value"
...> end
"This clause will match and bind x to 2 in this clause"
```

すでに存在している変数に対してパターンマッチを行うには `^` 演算子を使います。

```iex
iex> x = 1
1
iex> case 10 do
...>   ^x -> "Won't match"
...>   _ -> "Will match"
...> end
"Will match"
```

節はガードを使って条件を指定することもできます。

```iex
iex> case {1, 2, 3} do
...>   {1, x, 3} when x > 0 ->
...>     "Will match"
...>   _ ->
...>     "Would match, if guard condition were not satisfied"
...> end
"Will match"
```

上記の例にある最初の節では `x` が整数の時にマッチします。

ガードにおけるエラーが処理を抜けることはなく、ただガードに失敗するだけであると覚えておいてください。

```iex
iex> hd(1)
** (ArgumentError) argument error
iex> case 1 do
...>   x when hd(x) -> "Won't match"
...>   x -> "Got #{x}"
...> end
"Got 1"
```

いずれの節にもマッチしない時はエラーになります。

```iex
iex> case :ok do
...>   :error -> "Won't match"
...> end
** (CaseClauseError) no case clause matching: :ok
```

ガードの使い方や利用できる式について知りたい時は [the full documentation for guards](https://hexdocs.pm/elixir/guards.html) で詳しい情報を得られます。

NOTE: 無名関数は複数の節とガードを含むこともできます。

```iex
iex> f = fn
...>   x, y when x > 0 -> x + y
...>   x, y -> x * y
...> end
#Function<12.71889879/2 in :erl_eval.expr/5>
iex> f.(1, 3)
4
iex> f.(-1, 3)
-3
```

無名関数の中で節は引数の数が同じでなくてはならず、その数が合わなければエラーになります。

```iex
iex> f2 = fn
...>   x, y when x > 0 -> x + y
...>   x, y, z -> x * y + z
...> end
** (CompileError) iex:1: cannot mix clauses with different arities in anonymous functions
```

## `cond`

`case` は様々な値に対してマッチさせたい時に有用です。それでも、様々な条件を調べて最初に true と評価されるものを見つけたいことが往々にしてあります。そういった場合に取る方法のひとつが `cond` です。

```iex
iex> cond do
...>   2 + 2 == 5 ->
...>     "This will not be true"
...>   2 * 2 == 3 ->
...>     "Nor this"
...>   1 + 1 == 2 ->
...>     "But this will"
...> end
"But this will"
```

これは多くの命令型言語における `else if` に相当するものです(ここではあまり使われません)。

true を返す条件が見つからないと (`CondClauseError`) になります。この理由は、そういった時に最後では必ず `true` に等しくなる条件を書かなくてはならない為です。

```iex
iex> cond do
...>   2 + 2 == 5 ->
...>     "This is never true"
...>   2 * 2 == 3 ->
...>     "Nor this"
...>   true ->
...>     "This is always true (equivalent to else)"
...> end
"This is always true (equivalent to else)"
```

最後に、 `cond` は `nil` と `false` 以外の如何なる値も `true` と見なすことを覚えておきましょう。

```iex
iex> cond do
...>   hd([1, 2, 3]) ->
...>     "1 is considered as true"
...> end
"1 is considered as true"
```

## `if` and `unless`

`case` と `cond` の他、ひとつの条件だけを検証したい時に有用なマクロ `if/2` と `unless/2` も使えます。

```iex
iex> if true do
...>   "This works!"
...> end
"This works!"
iex> unless true do
...>   "This will never be seen"
...> end
nil
```

`false` と `nil` を返す条件では `do/end` のブロック間にある内容が実行されず、代わりに `nil` を返します。 `unless` ではこの逆になります。

これらはブロックで `else` も使えます。

```iex
iex> if nil do
...>   "This won't be seen"
...> else
...>   "This will"
...> end
"This will"
```

`if/2` と `unless/2` がマクロとして実行されることに関して興味深いところですが、他の多くの言語でもそうであるように、取り立てるほど特別な構造ではありません。これらに関するドキュメントや `if/2` のソースは [the `Kernel` module docs](https://hexdocs.pm/elixir/Kernel.html) で確認できます。 `Kernel` モジュールには `+/2` のような演算子や `is_function/2` といった関数も定義されており、すべて自動的にインポートされるので、あなたのコードはデフォルトでそれらを利用することができます。

## `do/end` blocks

At this point, we have learned four control structures: `case`, `cond`, `if`, and `unless`, and they were all wrapped in `do/end` blocks. It happens we could also write `if` as follows:

```iex
iex> if true, do: 1 + 2
3
```

Notice how the example above has a comma between `true` and `do:`, that's because it is using Elixir's regular syntax where each argument is separated by a comma. We say this syntax is using *keyword lists*. We can pass `else` using keywords too:

```iex
iex> if false, do: :this, else: :that
:that
```

`do/end` blocks are a syntactic convenience built on top of the keywords one. That's why `do/end` blocks do not require a comma between the previous argument and the block. They are useful exactly because they remove the verbosity when writing blocks of code. These are equivalent:

```iex
iex> if true do
...>   a = 1 + 2
...>   a + 10
...> end
13
iex> if true, do: (
...>   a = 1 + 2
...>   a + 10
...> )
13
```

One thing to keep in mind when using `do/end` blocks is they are always bound to the outermost function call. For example, the following expression:

```iex
iex> is_number if true do
...>  1 + 2
...> end
** (CompileError) iex:1: undefined function is_number/2
```

Would be parsed as:

```iex
iex> is_number(if true) do
...>  1 + 2
...> end
** (CompileError) iex:1: undefined function is_number/2
```

which leads to an undefined function error because that invocation passes two arguments, and `is_number/2` does not exist. The `if true` expression is invalid in itself because it needs the block, but since the arity of `is_number/2` does not match, Elixir does not even reach its evaluation.

Adding explicit parentheses is enough to bind the block to `if`:

```iex
iex> is_number(if true do
...>  1 + 2
...> end)
true
```

Keyword lists play an important role in the language and are quite common in many functions and macros. We will explore them a bit more in a future chapter. Now it is time to talk about "Binaries, strings, and char lists".
