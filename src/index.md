# Intro to Elixir

by <a href="https://twitter.com/tednaleid">@tednaleid</a>


!SLIDE shout
# Intro to Elixir

<img src="images/elixir-lang-logo.png" alt="" height="200px"/>

## by <a href="https://twitter.com/tednaleid">@tednaleid</a>


!SLIDE shout
# Quick Background


!SLIDE quieter shout
# Why should you spend time with Elixir?


!SLIDE quieter shout
# Linguistic Relativity

## (AKA Sapir-Whorf Hypothesis)<br/> <em>"The structure of a language affects the way in which its respective speakers conceptualize their world."</em> - [wikipedia](http://en.wikipedia.org/wiki/Linguistic_relativity)


!SLIDE 

<img src="images/seven_languages.jpg" alt="" height="500px"/>
## Covers: Ruby, Io, Prolog, Scala, Erlang, Clojure, Haskell

!SLIDE quieter shout
# <em>The Free Lunch is Over</em>

!SLIDE quietest shout
# Used 5 criteria to determine the language to use

!SLIDE quietest shout
# Natural Syntax <br/><br/> Fast and Repeatable Dev Cycle <br/><br/> Concurrent and Fast <br/><br/> Metaprogramming <br/><br/> Failure Management

!SLIDE quietest 
# Short List Choice #1: Ruby + $$$ 
## <strong>Good</strong><br/>Natural Syntax, Fast and Repeatable Dev Cycle, Metaprogramming
## <strong>Bad</strong><br/>Concurrent and Fast, Failure Management

!SLIDE quietest 
# Short List Choice #2: Erlang
## <strong>Good</strong><br/>Failure Management, Concurrent and Fast
## <strong>Bad</strong><br/>Natural Syntax, Fast and Repeatable Dev Cycle, Metaprogramming

!SLIDE quietest 
# Short List Choice #3: Clojure
## <strong>Good</strong><br/>Concurrent and Fast, Metaprogramming, Fast &amp; Repeatable Dev Cycle
## <strong>OK</strong><br/>Failure Management
## <strong>Bad</strong><br/>Natural Syntax

!SLIDE quieter shout
# Met José, Found Elixir 
## "Twisted Love Child of all 3 options"

!SLIDE shout quieter
# What is Elixir?

## Mostly immutable, functional language with ruby-like syntax running on the battle-tested Erlang BEAM VM

!SLIDE shout quieter
# What is Erlang/BEAM?

## Language + VM, Created by Ericsson in 1986 to support distributed, fault-tolerant, always-up systems

!SLIDE shout
# How does Elixir satisfy 5 criteria?

!SLIDE shout quieter
# 1. Natural Syntax

## Comfortable for most programmers, heavy weighting on quick parsing &amp; readability

!SLIDE shout
# Feels Rubyish

!SLIDE
# Basic Types

    iex> my_utf8_string = "hello Iñtërnâtiônàlizætiøn"
    "hello Iñtërnâtiônàlizætiøn"

    iex> my_atom = :hello
    :hello

    iex> 1000 == 1_000
    true

    iex> 0.314159e1 == 314159.0e-5
    true

    iex> my_range = 1..5
    1..5

!SLIDE 
# Tuples, Lists, Maps

    iex> my_tuple = {:ok, "return value", 715}
    {:ok, "return value", 715}

    iex> my_list = [1, 2, 3, 4, 5]
    [1, 2, 3, 4, 5]

    iex> my_map = %{:first => "Ted", :last => "Naleid"}
    %{first: "Ted", last: "Naleid"}


!SLIDE 
# Closures

    iex> sum = fn a, b -> a + b end
    #Function<12.90072148/2 in :erl_eval.expr/5>

    iex> sum.(1, 2)
    3
    
    # shortened closure syntax:

    iex> short_sum = &(&1 + &2)
    &:erlang.+/2

    iex> short_sum.(1, 2)
    3

!SLIDE

# Structs

    iex> defmodule Person do
    ...>   defstruct first: "Ted", last: "Naleid"
    ...> end
    {:module, Person, …}

    iex> %Person{}
    %Person{first: "Ted", last: "Naleid"}

    iex> %Person{first: "Hazel"}
    %Person{first: "Hazel", last: "Naleid"}

    iex> %Person{nope: "Bad Field"}
    ** (CompileError) iex:4: unknown key :nope for struct

!SLIDE

# Protocols

    iex> defprotocol Stringable do
    ...>   def to_string(value)
    ...> end

    iex> defimpl Stringable, for: Person do
    ...>   def to_string(value) do
    ...>     "#{value.first} #{value.last}"
    ...>   end
    ...> end

    iex> Stringable.to_string(%Person{})
    "Ted Naleid"

## Some similarities to an OOP Interface

!SLIDE 

# Pattern Matching
    iex> a = {:ok, 1}
    {:ok, 1}  

    iex> {:ok, b} = {:ok, 1}
    {:ok, 1}

    iex> b
    1    

!SLIDE 

# Pattern Matching Lists
    iex> [a, b, c] = [1, 2, 3]
    [1, 2, 3]

    iex> a
    1

    iex> [head | tail] = [1, 2, 3]
    [1, 2, 3]

    iex> head
    1

    iex> tail
    [2, 3]

!SLIDE 

# Pattern Matching Structs

    case HTTP.get(url) do
      {:ok, %HTTP.Resp{ status: 200, body: body }} ->
        IO.puts body
      {:ok, %HTTP.Resp{ status: 404 }} ->
        IO.puts "Not found :("
      {:ok, %HTTP.Resp{ status: status }} ->
        IO.puts "HTTP Status: #{status}"
      {:error, %HTTP.Error{ reason: reason }} ->
        IO.inspect reason
      _ ->
        IO.puts "¯\_(ツ)_/¯"
    end     


!SLIDE

# Even More Pattern Matching

    def execute({:ok, good_value}) do
      IO.puts "Known good value: #{good_value}"
    end

    def execute({:error, error_reason}) do
      IO.puts "Error! #{error_reason}"
    end

    iex> execute({:ok, "Yay!"})
    Known good value: Yay!

    iex> execute({:error, "Boo!"})
    Error! Boo!

!SLIDE 

# Pipe Operator `|>`

    defmodule Shop do
      defp apply_tax(prices) do 
        Enum.map(prices, fn v -> v * 1.1 end)
      end

      def cart_total(items) do
        Enum.sum(
          apply_tax(
            Enum.map(items, fn item -> item.price end)))
      end
    end 
    
    Shop.cart_total([%{:price=>5.00}, %{:price=>2.00}])
    # => 7.7

Nested `cart_total` is hard to read, have to read inside out

!SLIDE 

# Pipe Operator `|>`

      def cart_total(items) do
        prices = Enum.map(items, fn itm -> itm.price end)
        prices_with_tax = apply_tax(prices)
        Enum.sum(prices_with_tax)
      end

Intermediate variables cleans up a bit

!SLIDE 

# Pipe Operator `|>`

    def cart_total(items) do
      items
      |> Enum.map(fn item -> item.price end)
      |> add_tax
      |> Enum.sum
    end

`|>` operator passes result from last method as first param in next
<br/>

Similar to unix pipe: `ps ax | grep iex | awk '{ print $1 }'` 

!SLIDE quietest

# Simple Interop with Erlang

<br/>

    iex> :crypto.md5("sekr1t")
    <<192, 151, 240, 131, 252, 86, 1, 90, 71, 171, 2, …

Can easily leverage 20+ years of Erlang libraries


!SLIDE quieter shout

# 2. Fast &amp; Repeatable Dev Cycle

!SLIDE shout quieter

# Immutability

## Very Testable, Easy to Parallelize, No Side Effects

!SLIDE shout quieter

# Hot Reloading Without Restarting   

!SLIDE quietest smaller-code

# Mix Build Tool

    $ mix new myapp
    * creating README.md
    * creating .gitignore
    * creating mix.exs
    * creating config
    * creating config/config.exs
    * creating lib
    * creating lib/myapp.ex
    * creating test
    * creating test/test_helper.exs
    * creating test/myapp_test.exs

    Your mix project was created successfully.
    You can use mix to compile it, test it, and more:

        cd myapp
        mix test

    Run `mix help` for more commands.

!SLIDE quietest smaller-code

# Hex Package Manager
 
    defmodule MyProject.Mixfile do
      use Mix.Project

      def project do
        [app: :myapp,
         version: "0.0.1",
         elixir: "~> 1.0",
         deps: deps]
      end   

      def application do
        [applications: [:logger]]
      end

      defp deps do
        [{:ecto, "~> 0.11.3"},
         {:postgrex, "~> 0.8.1"},
         {:cowboy, github: "extend/cowboy"}]
      end
    end


!SLIDE quietest smaller-code

# `iex` is a Great REPL 

    iex> h Enum.map<tab>
    map/2           map_join/3      map_reduce/3

    iex> h Enum.map/2

                                def map(collection, fun)

    Returns a new collection, where each item is the result of invoking fun 
    on each corresponding item of collection.

    For dicts, the function expects a key-value tuple.

    Examples

    ┃ iex> Enum.map([1, 2, 3], fn(x) -> x * 2 end)
    ┃ [2, 4, 6]
    ┃
    ┃ iex> Enum.map([a: 1, b: 2], fn({k, v}) -> {k, -v} end)
    ┃ [a: -1, b: -2]


!SLIDE

# Debugging via `pry`

    require IEx

    def index(conn, _params) do
      IEx.pry
      conn |> render "index"
    end

Similar to the JavaScript `debugger;` command

!SLIDE  

# Erlang Activity Monitor

    iex> :observer.start

<img src="images/observer.png" alt="" height="500px"/>

!SLIDE shout
# Quick Demo
    

!SLIDE quieter shout
# 3. Metaprogramming

## How expressive can you make your code

!SLIDE quietest

# Hygenic Macros

    defmacro unless(expr, opts) do
      quote do
        if(!unquote(expr), unquote(opts))
      end
    end

    unless true do
      IO.puts "this will never be seen"
    end

## Most of the standard library is written using macros


!SLIDE 

# Easy Access to AST

    iex> ast = quote, do 2 * 2 / 7
    {:/,[context: Elixir, import: Kernel],
     [{:*,[context: Elixir, import: Kernel], [2, 2]}, 7]}

Underlying AST looks a bit like a lisp

## Full discussion bigger than this presentation, check out "Metaprogramming Elixir", by Chris McCord

!SLIDE shout quieter

# 4. Concurrent &amp; Fast

!SLIDE 
# WhatsApp Runs On Erlang VM

- 465M monthly users
- 19B messages in & 40B out per day
- 600M pictures, 200M voice, 100M videos
- 147M peak concurrent connections
- 230k peak logins/second
- 342K peak msgs in/sec, 712K out

At time of Facebook acquisition for $19 Billion


!SLIDE shout
# 10 Developers


!SLIDE shout quieter
# Great Single-Box Scalability
## Often 100's of thousands to millions of processes per machine <br/> ~2KB of stack/heap per thread


!SLIDE 

# hex.pm on Single 512MB Heroku Dyno

<img src="images/hexpm.png" alt="" height="400px"/>

(~0.15 load, from [https://twitter.com/emjii/status/591240463782391808](https://twitter.com/emjii/status/591240463782391808))   

!SLIDE
# Concurrency Built-in

    iex> parent = self()
    #PID<0.90.0>

    iex> spawn(fn -> send parent, "hello world" end)
    #PID<0.93.0>

    iex> receive do message -> IO.puts message end
    hello world
    :ok

!SLIDE shout quietest

# Isolation/Immutability Allows Garbage Collection at Process Level

## No big garbage collection pauses

!SLIDE shout
# 5. Failure Management      

!SLIDE quietest

# OTP Apps are Supervision Trees

<img src="images/observer_apps.png" alt="" height="400px"/>

## Supervisors monitor/start/stop Child Workers/Supervisors

!SLIDE shout quietest

# Elixir/OTP motto: "Let it Crash"


!SLIDE shout quietest

# Most Languages Littered with <br/>Defensive Programming 

## Miss an edge case and your app crashes<br/> ex: Goroutines aren't memory isolated…one dying takes down entire process

!SLIDE shout quietest

# Better Architecture -> Cleaner Code

## Exception handling is rare


!SLIDE shout quieter
# Other Reasons for Picking Elixir

!SLIDE shout
<img src="images/phoenix.png" alt="Phoenix Framework" width="900px" style="margin-top: 200px;"/>

## Elixir killer app; most developers weren't interested in <br/>Ruby till Rails &amp; Groovy till Grails  

!SLIDE 
# Great, Growing Community

<img src="images/hex_downloads.png" alt="" height="400px"/>

Hex Downloads (from [@emjii](https://twitter.com/emjii/status/613370295618007040) on 2015-06-24)


!SLIDE shout
# Solid Documentation

!SLIDE shout quietest

# Elixir's Strengths<br/><br/>Apps with many connections &amp; high uptime requirements

## (i.e. Internet of Things, REST/socket webservices, Mobile App back-end, Telephony)

!SLIDE shout quietest
# Elixir Weaknesses<br/><br/>Significant Graphics/GUI or Sequential Math

## There are better languages for the next Doom or Bitcoin mining


!SLIDE quietest shout

# "Three Major Hurdles to Learning" 
## (from Francesco Cesarini, founder of Erlang Solutions)



!SLIDE quietest shout
# 1. Functional Programming 
## Pattern Matching and Tail Recursion



!SLIDE quietest shout
# 2. Thinking/Reasoning Concurrently 
## Have a process for every truly concurrent activity in your system

!SLIDE quietest shout
# 3. Understanding Fault Tolerance and 'Let it Crash' Mentality


!SLIDE quieter shout

<img src="images/The_pragmatic_programmer.jpg" alt="The Pragmatic Programmer" height="450px"/>
## "Learn at least one new language every year"


!SLIDE quietest shout
# Don't make it one that's the same paradigms that you already know.

## That's learning syntax, not better programming


!SLIDE shout
# Getting Started


!SLIDE shout
# [elixir-lang.org](http://elixir-lang.org)


!SLIDE shout
<img src="images/programming_elixir.jpg" alt="Programming Elixir" height="450px"/>

<br/>
## Notice the author?

!SLIDE shout
<img src="images/elixir_in_action.png" alt="Elixir in Action" height="450px"/>

<br/>
## Released in June 2015

!SLIDE shout quieter
# #elixir-lang on Freenode IRC

!SLIDE shout quieter
# Follow [@ElixirMN](https://twitter.com/elixirmn) and [@elixirlang](https://twitter.com/elixirlang)


!SLIDE shout
# @tednaleid

!SLIDE shout
# Questions? 

