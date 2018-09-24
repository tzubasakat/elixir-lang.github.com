---
layout: getting-started
title: try、catch、rescue
---

# {{ page.title }}

{% include toc.html %}

Elixir は3つのエラー機構を持っています。エラー、スロー、イグジットです。この章では、それらがいつ使われるべきかをみていきましょう。

## エラー

エラー（または例外）はコード内で予期しない出来事が起きた時に使われます。例えば数値をアトムに加えようとした時に、エラーを発生させることが出来ます。

```iex
iex> :foo + 1
** (ArithmeticError) bad argument in arithmetic expression
     :erlang.+(:foo, 1)
```

ランタイムエラーは `raise/1` を使うことでいつでも発生させることが出来ます。

```iex
iex> raise "oops"
** (RuntimeError) oops
```

それ以外のエラーは `raise/2` にエラー名とキーワード引数のリストを渡すことで発生させることが出来ます。

```iex
iex> raise ArgumentError, message: "invalid argument foo"
** (ArgumentError) invalid argument foo
```

モジュールを作り、その中で `defexception/1` マクロを使うことで、独自のエラーを定義することもできます。この方法では、モジュールと同じ名前のエラーを作ることが出来ます。最も一般的な使用法は、独自のメッセージ付きエラーを定義することです。

```iex
iex> defmodule MyError do
iex>   defexception message: "default message"
iex> end
iex> raise MyError
** (MyError) default message
iex> raise MyError, message: "custom message"
** (MyError) custom message
```

エラーは `tru/rescue` 構造を用いることで **捕捉** することが出来ます。

```iex
iex> try do
...>   raise "oops"
...> rescue
...>   e in RuntimeError -> e
...> end
%RuntimeError{message: "oops"}
```

上の例ではランタイムエラーを補足し、 `ies` セッション内でエラーが表示されるように、そのエラー自身を返しています。

もしエラーを使う必要がないのであれば、エラー自身を返す必要はありません。

```iex
iex> try do
...>   raise "oops"
...> rescue
...>   RuntimeError -> "Error!"
...> end
"Error!"
```

しかし実際のところ、Elixirで開発中に `try/rescue` 構造を使うことはほとんどないでしょう。例えば、多くの言語ではファイルを開けなかったときにエラーになるので、あなたがそれを捕捉しなければならないようになっています。一方Elixirが提供する `File.read/1` 関数は、ファイルを開くことに成功したかどうかの情報を含んだタプルを返します。

```iex
iex> File.read "hello"
{:error, :enoent}
iex> File.write "hello", "world"
:ok
iex> File.read "hello"
{:ok, "world"}
```

そこに `try/rescue` は存在しません。ファイルを開く時の複数の結果を取り扱いたい場合は、 `case` 構造と一緒にパターンマッチングを使うことが出来ます。

```iex
iex> case File.read "hello" do
...>   {:ok, body}      -> IO.puts "Success: #{body}"
...>   {:error, reason} -> IO.puts "Error: #{reason}"
...> end
```

要するに、ファイルを開くときのエラーが例外かそうでないかを決めるのはあなたのアプリケーション次第です。だからこそElixirは `File.read/1` やその他の関数で例外を強制しません。その代りに、最も良い例外の処理方法を開発者に委ねます。

ファイルが存在することを期待している時（そしてそのファイルが存在しないときは本当にエラーである時）、 `File.read!/1` を使うでしょう。

```iex
iex> File.read! "unknown"
** (File.Error) could not read file unknown: no such file or directory
    (elixir) lib/file.ex:272: File.read!/1
```

標準ライブラリ内の多くの関数は、マッチするタプルを返す代わりに例外を発生させる、という反対のパターンに従います。規約では、 `foo` 関数を作るときは `{:ok, result}` か `{:error, reason}` タプルを返し、 `foo!` という、 `foo` と同じ名前に `!` がつき `foo` と同じ引数を取る関数は、エラーが生じたときは例外を発生させます。 `foo!` はすべてが上手く行った時は、タプルで囲わない結果を返すべきです。 [`File` モジュール](https://hexdocs.pm/elixir/File.html)  はこの規約についての良い例です。

Elixirでは、 `try/rescue` の使用を避けています。なぜなら、 **フローを制御するためにエラーを使わないから** です。私達はエラーを文字通りに受け取ります。エラーは予期しないまたは予期した例外的状況のために用意されています。フローを制御する構造が必要な場合は、 *スロー* が使われるべきです。それでは次にスローを見ていきましょう。

## Throws

In Elixir, a value can be thrown and later be caught. `throw` and `catch` are reserved for situations where it is not possible to retrieve a value unless by using `throw` and `catch`.

Those situations are quite uncommon in practice except when interfacing with libraries that do not provide a proper API. For example, let's imagine the `Enum` module did not provide any API for finding a value and that we needed to find the first multiple of 13 in a list of numbers:

```iex
iex> try do
...>   Enum.each -50..50, fn(x) ->
...>     if rem(x, 13) == 0, do: throw(x)
...>   end
...>   "Got nothing"
...> catch
...>   x -> "Got #{x}"
...> end
"Got -39"
```

Since `Enum` *does* provide a proper API, in practice `Enum.find/2` is the way to go:

```iex
iex> Enum.find -50..50, &(rem(&1, 13) == 0)
-39
```

## Exits

All Elixir code runs inside processes that communicate with each other. When a process dies of "natural causes" (e.g., unhandled exceptions), it sends an `exit` signal. A process can also die by explicitly sending an exit signal:

```iex
iex> spawn_link fn -> exit(1) end
** (EXIT from #PID<0.56.0>) evaluator process exited with reason: 1
```

In the example above, the linked process died by sending an `exit` signal with a value of 1. The Elixir shell automatically handles those messages and prints them to the terminal.

`exit` can also be "caught" using `try/catch`:

```iex
iex> try do
...>   exit "I am exiting"
...> catch
...>   :exit, _ -> "not really"
...> end
"not really"
```

Using `try/catch` is already uncommon and using it to catch exits is even rarer.

`exit` signals are an important part of the fault tolerant system provided by the Erlang <abbr title="Virtual Machine">VM</abbr>. Processes usually run under supervision trees which are themselves processes that listen to `exit` signals from the supervised processes. Once an exit signal is received, the supervision strategy kicks in and the supervised process is restarted.

It is exactly this supervision system that makes constructs like `try/catch` and `try/rescue` so uncommon in Elixir. Instead of rescuing an error, we'd rather "fail fast" since the supervision tree will guarantee our application will go back to a known initial state after the error.

## After

Sometimes it's necessary to ensure that a resource is cleaned up after some action that could potentially raise an error. The `try/after` construct allows you to do that. For example, we can open a file and use an `after` clause to close it--even if something goes wrong:

```iex
iex> {:ok, file} = File.open "sample", [:utf8, :write]
iex> try do
...>   IO.write file, "olá"
...>   raise "oops, something went wrong"
...> after
...>   File.close(file)
...> end
** (RuntimeError) oops, something went wrong
```

The `after` clause will be executed regardless of whether or not the tried block succeeds. Note, however, that if a linked process exits,
this process will exit and the `after` clause will not get run. Thus `after` provides only a soft guarantee. Luckily, files in Elixir are also linked to the current processes and therefore they will always get closed if the current process crashes, independent of the
`after` clause. You will find the same to be true for other resources like ETS tables, sockets, ports and more.

Sometimes you may want to wrap the entire body of a function in a `try` construct, often to guarantee some code will be executed afterwards. In such cases, Elixir allows you to omit the `try` line:

```iex
iex> defmodule RunAfter do
...>   def without_even_trying do
...>     raise "oops"
...>   after
...>     IO.puts "cleaning up!"
...>   end
...> end
iex> RunAfter.without_even_trying
cleaning up!
** (RuntimeError) oops
```

Elixir will automatically wrap the function body in a `try` whenever one of `after`, `rescue` or `catch` is specified.

## Else

If an `else` block is present, it will match on the results of the `try` block whenever the `try` block finishes without a throw or an error.

```iex
iex> x = 2
2
iex> try do
...>   1 / x
...> rescue
...>   ArithmeticError ->
...>     :infinity
...> else
...>   y when y < 1 and y > -1 ->
...>     :small
...>   _ ->
...>     :large
...> end
:small
```

Exceptions in the `else` block are not caught. If no pattern inside the `else` block matches, an exception will be raised; this exception is not caught by the current `try/catch/rescue/after` block.

## Variables scope

It is important to bear in mind that variables defined inside `try/catch/rescue/after` blocks do not leak to the outer context. This is because the `try` block may fail and as such the variables may never be bound in the first place. In other words, this code is invalid:

```iex
iex> try do
...>   raise "fail"
...>   what_happened = :did_not_raise
...> rescue
...>   _ -> what_happened = :rescued
...> end
iex> what_happened
** (RuntimeError) undefined function: what_happened/0
```

Instead, you can store the value of the `try` expression:

```iex
iex> what_happened =
...>   try do
...>     raise "fail"
...>     :did_not_raise
...>   rescue
...>     _ -> :rescued
...>   end
iex> what_happened
:rescued
```

This finishes our introduction to `try`, `catch`, and `rescue`. You will find they are used less frequently in Elixir than in other languages, although they may be handy in some situations where a library or some particular code is not playing "by the rules".
