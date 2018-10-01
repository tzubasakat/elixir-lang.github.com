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

## Anonymous functions

Anonymous functions can be created inline and are delimited by the keywords `fn` and `end`:

```iex
iex> add = fn a, b -> a + b end
#Function<12.71889879/2 in :erl_eval.expr/5>
iex> add.(1, 2)
3
iex> is_function(add)
true
iex> is_function(add, 2) # check if add is a function that expects exactly 2 arguments
true
iex> is_function(add, 1) # check if add is a function that expects exactly 1 argument
false
```

Functions are "first class citizens" in Elixir meaning they can be passed as arguments to other functions in the same way as integers and strings. In the example, we have passed the function in the variable `add` to the `is_function/1` function which correctly returned `true`. We can also check the arity of the function by calling `is_function/2`.

Note that a dot (`.`) between the variable and parentheses is required to invoke an anonymous function. The dot ensures there is no ambiguity between calling an anonymous function named `add` and a named function `add/2`. In this sense, Elixir makes a clear distinction between anonymous functions and named functions. We will explore those differences in [Chapter 8](/getting-started/modules-and-functions.html).

Anonymous functions are closures and as such they can access variables that are in scope when the function is defined. Let's define a new anonymous function that uses the `add` anonymous function we have previously defined:

```iex
iex> double = fn a -> add.(a, a) end
#Function<6.71889879/1 in :erl_eval.expr/5>
iex> double.(2)
4
```

Keep in mind a variable assigned inside a function does not affect its surrounding environment:

```iex
iex> x = 42
42
iex> (fn -> x = 0 end).()
0
iex> x
42
```

## (Linked) Lists

Elixir uses square brackets to specify a list of values. Values can be of any type:

```iex
iex> [1, 2, true, 3]
[1, 2, true, 3]
iex> length [1, 2, 3]
3
```

Two lists can be concatenated or subtracted using the `++/2` and `--/2` operators respectively:

```iex
iex> [1, 2, 3] ++ [4, 5, 6]
[1, 2, 3, 4, 5, 6]
iex> [1, true, 2, false, 3, true] -- [true, false]
[1, 2, 3, true]
```

List operators never modify the existing list. Concatenating to or removing elements from a list returns a new list. We say that Elixir data structures are *immutable*. One advantage of immutability is that it leads to clearer code. You can freely pass the data around with the guarantee no one will change it - only transform it.

Throughout the tutorial, we will talk a lot about the head and tail of a list. The head is the first element of a list and the tail is the remainder of the list. They can be retrieved with the functions `hd/1` and `tl/1`. Let's assign a list to a variable and retrieve its head and tail:

```iex
iex> list = [1, 2, 3]
iex> hd(list)
1
iex> tl(list)
[2, 3]
```

Getting the head or the tail of an empty list throws an error:

```iex
iex> hd []
** (ArgumentError) argument error
```

Sometimes you will create a list and it will return a value in single quotes. For example:

```iex
iex> [11, 12, 13]
'\v\f\r'
iex> [104, 101, 108, 108, 111]
'hello'
```

When Elixir sees a list of printable ASCII numbers, Elixir will print that as a charlist (literally a list of characters). Charlists are quite common when interfacing with existing Erlang code. Whenever you see a value in IEx and you are not quite sure what it is, you can use the `i/1` to retrieve information about it:

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

Keep in mind single-quoted and double-quoted representations are not equivalent in Elixir as they are represented by different types:

```iex
iex> 'hello' == "hello"
false
```

Single quotes are charlists, double quotes are strings. We will talk more about them in the ["Binaries, strings and charlists"](/getting-started/binaries-strings-and-char-lists.html) chapter.

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
