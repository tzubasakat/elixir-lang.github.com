---
layout: getting-started
title: Basic types
---

# {{ page.title }}

{% include toc.html %}

この章では、Integers、Floats、Booleans、Atoms、Strings、Lists、Tuples など Elixir の基本的なデータ型について学んでいきます。

```iex
iex> 1          # integer
iex> 0x1F       # integer
iex> 1.0        # float
iex> true       # boolean
iex> :atom      # atom / symbol
iex> "elixir"   # string
iex> [1, 2, 3]  # list
iex> {1, 2, 3}  # tuple
```

## 四則演算

`iex` を起動して以下の演算を試してください。

```iex
iex> 1 + 2
3
iex> 5 * 5
25
iex> 10 / 2
5.0
```

`10 / 2` の結果が Integer の `5` ではなく `5.0` という Float として得られたはずです。Elixir において `/` は常に Float を返します。除算や剰余で整数を得たい場合には、`div` や `rem` 関数を使用できます。

```iex
iex> div(10, 2)
5
iex> div 10, 2
5
iex> rem 10, 3
1
```

Elixr は関数を呼び出す際の括弧を省略できます。これにより、宣言と制御構造での文法的な見晴らしをクリアにします。

2 進法、8 進法、および 16 進法もサポートしています。

```iex
iex> 0b1010
10
iex> 0o777
511
iex> 0x1F
31
```

浮動小数点数は仮数と小数点に続いて小数を必要とし、指数表記の `e` も使用できます。

```iex
iex> 1.0
1.0
iex> 1.0e-10
1.0e-10
```

Elixir の Floats は倍精度浮動小数点数です。

`round` や `trunc` 関数では、引数として与えられた Float をもとに最も近い仮数を得られます。

```iex
iex> round(3.58)
4
iex> trunc(3.58)
3
```

## 関数の確認

Elixir における関数は、その関数名とアリティで成り立ちます。アリティはその関数が受け取る引数の数を示します。これ以降は関数を説明するにあたって、関数名とそのアリティの両方を添えて記述していきます。`round/1` は `round` という関数とその関数が受け取る引数の数 `1` を示します。一方で、例えば `round/2` という関数があった場合に、それは関数名として同名ではあるものの、前者とは異なって引数を `2` 受け取る別の関数です。

## 真偽値

Elixir では `true` と `false` を 真偽値 としています。

```iex
iex> true
true
iex> true == false
false
```

述語的な名前を持った一連の関数 (Predicate functions) を使って、値の型をチェックすることも出来ます。例えば `is_boolean/1` 関数は、値が真偽値か否かをチェックする為に使用します。

```iex
iex> is_boolean(true)
true
iex> is_boolean(1)
false
```

さらに、`is_integer/1` や `is_float/1` 、`is_number/1` なども同様に、それぞれの引数が整数・浮動小数点数・数値であるかをチェックできます。

> Note: `h()` でシェルの使い方に関する情報を表示できます。`h` ヘルパーは関数に関するドキュメントを参照する際にも使用できます。

## アトム

アトムは他のいくつかの言語で言うところのシンボルに相当し、それ自身が定数でもあります。

```iex
iex> :hello
:hello
iex> :hello == :world
false
```

実は `true` と `false` もアトムです。

```iex
iex> true == :true
true
iex> is_atom(false)
true
iex> is_boolean(:false)
true
```

後で触れますが、Elixir はエイリアスと呼ばれる機能を持っています。エイリアスは大文字から始め、それもまた同時にアトムなのです。

```iex
iex> is_atom(Hello)
true
```

## 文字列

文字列リテラルはダブルクォーテーションで囲み、UTF-8 でエンコードされます。

```iex
iex> "hellö"
"hellö"
```

> Note: Windows をお使いの方は、デフォルトで UTF-8 を使用できない可能性があります。これを変更するには、 IEx を起動する前に、`chcp 65001` を実行してください。

Elixir は文字列内での式展開もサポートしています。

```iex
iex> "hellö #{:world}"
"hellö world"
```

文字列内では改行することができ、エスケープシーケンスも利用できます。

```iex
iex> "hello
...> world"
"hello\nworld"
iex> "hello\nworld"
"hello\nworld"
```

文字列の出力には `IO` モジュールの `IO.puts/1` 関数を使用します。

```iex
iex> IO.puts "hello\nworld"
hello
world
:ok
```

`IO.puts/1` 関数がアトムの `:ok` を返していることにも留意してください。

Elixir における文字列は、内部的にバイト列での表現もなされています。

```iex
iex> is_binary("hellö")
true
```

文字列のバイト数も得られます。

```iex
iex> byte_size("hellö")
6
```

上記の文字列は 5 字ですが、バイト数としては 6 が得られました。 "ö" を UTF-8 で表す為には 2 バイトを要するからです。`String.length/1` を使用すると、その文字数に基づいた文字列の長さを得ることもできます。

```iex
iex> String.length("hellö")
5
```

[String モジュール](https://hexdocs.pm/elixir/String.html) には、Unicode に基づいて定義された文字列を操作する為の様々な関数が含まれています。

```iex
iex> String.upcase("hellö")
"HELLÖ"
```

## 無名関数

無名関数は `fn` と `end` で囲んだ内側で定義されます。

```iex
iex> add = fn a, b -> a + b end
#Function<12.71889879/2 in :erl_eval.expr/5>
iex> add.(1, 2)
3
iex> is_function(add)
true
iex> is_function(add, 2) # add が 2 つの引数を期待する関数であるのかを確かめる
true
iex> is_function(add, 1) # add が 1 つの引数を期待する関数であるのかを確かめる
false
```

「Elixir における関数が"第一級オブジェクト"である」ということは、関数そのものも Integer や String と同様に他の関数へ引数として渡すことが出来るという意味です。例として、私達は先ほど変数 `add` にバインドした関数を、引数が関数であれば `true` を返すという `is_function/1` 関数に渡しました。さらには `is_function/2` 関数を使用してアリティを確かめることも出来ました。

無名関数の実行には変数と括弧の間にドット (`.`) を必要とします。このドットによって、 `add` という無名関数の呼び出しと `add/2` という関数の呼び出しを区別し、曖昧がないことを保証します。そういった意味で Elixir は無名関数と通常の関数とを明確に区別します。それについて詳しくは [第 8 章](/getting-started/modules-and-functions.html) で取り上げます。

無名関数はクロージャであり、関数が定義された際のスコープ内にある変数へはそのままアクセスできます。それでは、先ほど定義した `add` を内包する無名関数を新たに定義してみましょう。

```iex
iex> double = fn a -> add.(a, a) end
#Function<6.71889879/1 in :erl_eval.expr/5>
iex> double.(2)
4
```

関数内部に置かれた変数は、その周囲の環境には影響がないことに注意してください。

```iex
iex> x = 42
42
iex> (fn -> x = 0 end).()
0
iex> x
42
```

## リスト

リストを作るには角括弧を使って記述します。リストの要素はどんな型でも構いません。

```iex
iex> [1, 2, true, 3]
[1, 2, true, 3]
iex> length [1, 2, 3]
3
```

`++/2` や `--/2` を使えば、2つのリストを足したり引いたり出来ます。

```iex
iex> [1, 2, 3] ++ [4, 5, 6]
[1, 2, 3, 4, 5, 6]
iex> [1, true, 2, false, 3, true] -- [true, false]
[1, 2, 3, true]
```

リストへの操作は既にあるリストを改変しません。リストを足したり引いたりすると、新しく別のリストを返します。Elixir のデータ構造は *イミュータブル* です。イミュータブルであることのメリットとして、明快なコードを書けるということが挙げられます。このおかげで、データが非破壊であるという保証のもとに我々はデータの自由なやり取りを行うことが出来ます。

このチュートリアルを通してリストの先頭と後尾について何度か触れました。先頭はリストの最初の要素であり、後尾はリストの残りの要素です。これらは `hd/1` と `tl/1` で取り出すことができます。では、リストに要素を加えて先頭や後尾からそれら要素を取り出してみましょう。

```iex
iex> list = [1, 2, 3]
iex> hd(list)
1
iex> tl(list)
[2, 3]
```

空のリストから先頭や後尾の要素を得ようとするとエラーが返ってきます。

```iex
iex> hd []
** (ArgumentError) argument error
```

作成したリストがシングルクォーテーションで要素を返すことがあります。

```iex
iex> [11, 12, 13]
'\v\f\r'
iex> [104, 101, 108, 108, 111]
'hello'
```

出力可能な ASCII ナンバーが見つかると、Elixir はそれらを(文字リテラルのリスト)文字で出力します。

```iex
iex> i 'hello'
Term
  'hello'
Data type
  List
Description
  ...
Raw representation
  [104, 101, 108, 108, 111]
Reference modules
  List
Implemented protocols
  ...
```

Elixir においてシングルクォーテーションとダブルクォーテーションは同等ではなく、異なる型であるということを念頭においてください。

```iex
iex> 'hello' == "hello"
false
```

シングルクォーテーションは文字リストであり、ダブルクォーテーションは文字列です。これについては ["バイナリ、文字列、文字リスト"](/getting-started/binaries-strings-and-char-lists.html) の章に譲ります。

## Tuples

Elixir uses curly brackets to define tuples. Like lists, tuples can hold any value:

```iex
iex> {:ok, "hello"}
{:ok, "hello"}
iex> tuple_size {:ok, "hello"}
2
```

Tuples store elements contiguously in memory. This means accessing a tuple element by index or getting the tuple size is a fast operation. Indexes start from zero:

```iex
iex> tuple = {:ok, "hello"}
{:ok, "hello"}
iex> elem(tuple, 1)
"hello"
iex> tuple_size(tuple)
2
```

It is also possible to put an element at a particular index in a tuple with `put_elem/3`:

```iex
iex> tuple = {:ok, "hello"}
{:ok, "hello"}
iex> put_elem(tuple, 1, "world")
{:ok, "world"}
iex> tuple
{:ok, "hello"}
```

Notice that `put_elem/3` returned a new tuple. The original tuple stored in the `tuple` variable was not modified. Like lists, tuples are also immutable. Every operation on a tuple returns a new tuple, it never changes the given one.

## Lists or tuples?

What is the difference between lists and tuples?

Lists are stored in memory as linked lists, meaning that each element in a list holds its value and points to the following element until the end of the list is reached. This means accessing the length of a list is a linear operation: we need to traverse the whole list in order to figure out its size.

Similarly, the performance of list concatenation depends on the length of the left-hand list:

```iex
iex> list = [1, 2, 3]

# This is fast as we only need to traverse `[0]` to prepend to `list`
iex> [0] ++ list
[0, 1, 2, 3]

# This is slow as we need to traverse `list` to append 4
iex> list ++ [4]
[1, 2, 3, 4]
```

Tuples, on the other hand, are stored contiguously in memory. This means getting the tuple size or accessing an element by index is fast. However, updating or adding elements to tuples is expensive because it requires creating a new tuple in memory:

```iex
iex> tuple = {:a, :b, :c, :d}
iex> put_elem(tuple, 2, :e)
{:a, :b, :e, :d}
```

Note that this applies only to the tuple itself, not its contents. For instance, when you update a tuple, all entries are shared between the old and the new tuple, except for the entry that has been replaced. In other words, tuples and lists in Elixir are capable of sharing their contents. This reduces the amount of memory allocation the language needs to perform and is only possible thanks to the immutable semantics of the language.

Those performance characteristics dictate the usage of those data structures. One very common use case for tuples is to use them to return extra information from a function. For example, `File.read/1` is a function that can be used to read file contents. It returns a tuple:

```iex
iex> File.read("path/to/existing/file")
{:ok, "... contents ..."}
iex> File.read("path/to/unknown/file")
{:error, :enoent}
```

If the path given to `File.read/1` exists, it returns a tuple with the atom `:ok` as the first element and the file contents as the second. Otherwise, it returns a tuple with `:error` and the error description.

Most of the time, Elixir is going to guide you to do the right thing. For example, there is an `elem/2` function to access a tuple item but there is no built-in equivalent for lists:

```iex
iex> tuple = {:ok, "hello"}
{:ok, "hello"}
iex> elem(tuple, 1)
"hello"
```

When counting the elements in a data structure, Elixir also abides by a simple rule: the function is named `size` if the operation is in constant time (i.e. the value is pre-calculated) or `length` if the operation is linear (i.e. calculating the length gets slower as the input grows). As a mnemonic, both "length" and "linear" start with "l".

For example, we have used 4 counting functions so far: `byte_size/1` (for the number of bytes in a string), `tuple_size/1` (for tuple size), `length/1` (for list length) and `String.length/1` (for the number of graphemes in a string). We use `byte_size` to get the number of bytes in a string -- a cheap operation. Retrieving the number of Unicode characters, on the other hand, uses `String.length`, and may be expensive as it relies on a traversal of the entire string.

Elixir also provides `Port`, `Reference`, and `PID` as data types (usually used in process communication), and we will take a quick look at them when talking about processes. For now, let's take a look at some of the basic operators that go with our basic types.
