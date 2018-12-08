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

## Pattern matching

The match operator is not only used to match against simple values, but it is also useful for destructuring more complex data types. For example, we can pattern match on tuples:

```iex
iex> {a, b, c} = {:hello, "world", 42}
{:hello, "world", 42}
iex> a
:hello
iex> b
"world"
```

A pattern match will error if the sides can't be matched, for example if the tuples have different sizes:

```iex
iex> {a, b, c} = {:hello, "world"}
** (MatchError) no match of right hand side value: {:hello, "world"}
```

And also when comparing different types:

```iex
iex> {a, b, c} = [:hello, "world", 42]
** (MatchError) no match of right hand side value: [:hello, "world", 42]
```

More interestingly, we can match on specific values. The example below asserts that the left side will only match the right side when the right side is a tuple that starts with the atom `:ok`:

```iex
iex> {:ok, result} = {:ok, 13}
{:ok, 13}
iex> result
13

iex> {:ok, result} = {:error, :oops}
** (MatchError) no match of right hand side value: {:error, :oops}
```

We can pattern match on lists:

```iex
iex> [a, b, c] = [1, 2, 3]
[1, 2, 3]
iex> a
1
```

A list also supports matching on its own head and tail:

```iex
iex> [head | tail] = [1, 2, 3]
[1, 2, 3]
iex> head
1
iex> tail
[2, 3]
```

Similar to the `hd/1` and `tl/1` functions, we can't match an empty list with a head and tail pattern:

```iex
iex> [h | t] = []
** (MatchError) no match of right hand side value: []
```

The `[head | tail]` format is not only used on pattern matching but also for prepending items to a list:

```iex
iex> list = [1, 2, 3]
[1, 2, 3]
iex> [0 | list]
[0, 1, 2, 3]
```

Pattern matching allows developers to easily destructure data types such as tuples and lists. As we will see in the following chapters, it is one of the foundations of recursion in Elixir and applies to other types as well, like maps and binaries.

## The pin operator

Variables in Elixir can be rebound:

```iex
iex> x = 1
1
iex> x = 2
2
```

Use the pin operator `^` when you want to pattern match against an existing variable's value rather than rebinding the variable:

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

Because we have assigned the value of 1 to the variable x, this last example could also have been written as:

```
iex> {y, 1} = {2, 2}
** (MatchError) no match of right hand side value: {2, 2}
```

If a variable is mentioned more than once in a pattern, all references should bind to the same pattern:

```iex
iex> {x, x} = {1, 1}
{1, 1}
iex> {x, x} = {1, 2}
** (MatchError) no match of right hand side value: {1, 2}
```

In some cases, you don't care about a particular value in a pattern. It is a common practice to bind those values to the underscore, `_`. For example, if only the head of the list matters to us, we can assign the tail to underscore:

```iex
iex> [h | _] = [1, 2, 3]
[1, 2, 3]
iex> h
1
```

The variable `_` is special in that it can never be read from. Trying to read from it gives a compile error:

```iex
iex> _
** (CompileError) iex:1: invalid use of _. "_" represents a value to be ignored in a pattern and cannot be used in expressions
```

Although pattern matching allows us to build powerful constructs, its usage is limited. For instance, you cannot make function calls on the left side of a match. The following example is invalid:

```iex
iex> length([1, [2], 3]) = 3
** (CompileError) iex:1: cannot invoke remote function :erlang.length/1 inside match
```

This finishes our introduction to pattern matching. As we will see in the next chapter, pattern matching is very common in many language constructs.
