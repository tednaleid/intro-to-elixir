# Intro to Elixir

by <a href="https://twitter.com/tednaleid">@tednaleid</a>

!SLIDE shout
# Intro to Elixir

<img src="images/elixir-lang-logo.png" alt="" height="200px"/>

## by <a href="https://twitter.com/tednaleid">@tednaleid</a>

!SLIDE quietest shout
# Spent time with 3 "new" languages and learned...

!SLIDE quietest shout
# if you want to improve the safety your low-level systems code (C/C++)

!SLIDE quieter shout
# take a look at Rust

!SLIDE quietest shout
# If you want better uptime and _lots_ of concurrent connections

!SLIDE quieter shout
# take a look at Elixir

!SLIDE quietest shout
# If you want a language that helps you repeat the same mistakes

## (mutable state, shared heap/stack, _lots_ of error handling)

!SLIDE
<a href="https://twitter.com/dysinger/status/622582038982299648">
  <img src="images/golang.png" alt="" height="600px"/>
</a>


!SLIDE shout quieter
# What is Elixir?

## Mostly immutable, functional language with ruby-like syntax running on the battle-tested Erlang BEAM VM

!SLIDE shout quieter
# What is Erlang/BEAM?

## Language + VM, Created by Ericsson in 1986 to support distributed, fault-tolerant, always-up systems

!SLIDE shout
# Why Should _You_ Learn Elixir?

!SLIDE shout quieter

# I could tell you about the great syntax

!SLIDE
# about Pattern Matching

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
# the elegant Pipe Operator

    def cart_total(items) do
      items
      |> Enum.map(fn item -> item.price end)
      |> add_tax
      |> Enum.sum
    end

`|>` operator passes result from last method as first param in next


!SLIDE quieter shout
# about First Class Functions and Hygienic Macros

!SLIDE shout quieter
# but I'm not going to <br/><br/>syntax doesn't really matter

!SLIDE
<img src="images/js_books.jpg" alt="" height="480px"/>
## Languages with some terrible syntax have been very successful
<span style="font-size:50%; float: right;"><a href="https://twitter.com/absinthol/status/571002000135086080">source</a></span>

!SLIDE shout
# syntax is lipstick; what matters is beneath

!SLIDE quietest shout
# you need a big leap in <br/><br/>[reliability]() | [maintainability]() | [performance]() <br/><br/>to change your entire way of development

!SLIDE quietest shout
# With Elixir you get all 3

!SLIDE shout quietest
# Elixir's Greatest Strength: OTP
## Monitoring and Supervision built-in, not an afterthought

!SLIDE quietest
# OTP Apps are Supervision Trees

<img src="images/observer_apps.png" alt="" height="400px"/>

## Supervisors monitor/start/stop Child Workers/Supervisors

!SLIDE shout quietest
# OTP motto: "Let it Crash"

!SLIDE quietest
# IEx Observer Example

    mix new foobar
    cd foobar
    iex -S mix
    iex> :observer.start



!SLIDE shout quietest

# Most Languages Littered with <br/>Defensive Programming

## Miss an edge case and your app crashes<br/> ex: Goroutines aren't memory isolated…one unhandled error takes down entire process

!SLIDE shout quietest
# Better Architecture -> Cleaner Code

## Exception handling is rare


!SLIDE shout quieter
# Immutability

## Very Testable, Easy to Parallelize, No Side Effects


!SLIDE
# WhatsApp Runs On BEAM VM

- 465M monthly users
- 19B messages in & 40B out per day
- 600M pictures, 200M voice, 100M videos
- 147M peak concurrent connections
- 230k peak logins/second
- 342K peak msgs in/sec, 712K out

At time of Facebook acquisition for $19 Billion.

!SLIDE shout
# How Many Developers?


!SLIDE shout
# 10 Developers
## "That work with Erlang, we handle all the development and ops"<br/>- Rick Reed, WhatsApp
<span style="font-size:50%; float: right;"><a href="http://www.infoq.com/presentations/whatsapp-scalability">source</a></span>


!SLIDE quietest
# Other things that run on the BEAM VM
  - Facebook Chat
  - Amazon SimpleDB
  - RabbitMQ
  - Riak
  - League of Legends chat


!SLIDE shout quieter
# Great Single-Box Scalability
## Scales to millions of BEAM processes per machine <br/> ~2KB of stack/heap per thread

!SLIDE shout quieter
# Operational complexity scales with number of nodes, not number of cores

!SLIDE

# hex.pm on Single 512MB Heroku Dyno

<img src="images/hexpm.png" alt="" height="400px"/>

(~0.15 load, from [https://twitter.com/emjii/status/591240463782391808](https://twitter.com/emjii/status/591240463782391808))

!SLIDE quieter shout

<img src="images/The_pragmatic_programmer.jpg" alt="The Pragmatic Programmer" height="450px"/>
## "Learn at least one new language every year"


!SLIDE quietest shout
# Don't make it one that's the same paradigms that you already know.

## That's learning syntax, not better programming

!SLIDE quietest shout
# Functional Programming is everywhere

## Almost all languages now have first class functions<br/>(Java, JavaScript, C#, Ruby, Python, Swift)


!SLIDE quietest

# The problem with OO is tight coupling of data and behavior

    "foo".bar().baz()

<br/>
<br/>
<br/>
<br/>
<br/>
<span style="font-size:50%; float: right;"><a href="https://twitter.com/josevalim/status/635895093149302785">source</a></span>

!SLIDE quietest

# In functional languages behavior lives wherever it makes the most sense

    "foo" |> bar() |> baz()


Pattern Matching and Protocols let us pick the "right" function for our data without the tight coupling

!SLIDE quietest shout

# In OO we spend a lot of our time fighting the data/behavior coupling


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

!SLIDE quieter
# #elixir-lang on Freenode IRC

<br/>
# [Slack Elixir Group](https://elixir-slackin.herokuapp.com/)

!SLIDE shout quieter
# Follow [@ElixirMN](https://twitter.com/elixirmn) and [@elixirlang](https://twitter.com/elixirlang)


!SLIDE shout
# @tednaleid

!SLIDE shout
# Questions?
