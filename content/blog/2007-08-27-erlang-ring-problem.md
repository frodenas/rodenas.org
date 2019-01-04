---
title: Erlang ring problem
author: ferdy
date: 2007-08-27T21:46:48+00:00
url: /blog/2007/08/27/erlang-ring-problem/
b2007:
  - 08
bcategories:
  - Languages

---
As I am on vacation, I have had some time to read part of the [Programming Erlang][1] book I mentioned some posts ago. After reading the firsts chapters, I was surprised to see that one of the not so much mentioned [Erlang][2] central features is that relies extremely on the [pattern matching][3] idiom. Just one example, the &#8220;=&#8221; operator is a pattern matching operator, which behaves like assignment when the variable is unbound, and act like a pattern matching expression when it is bound.

Another feature that I was glad to see is the [actor model][4] paradigm, with messages sent from and to Actors (like [Scala][5] or [Smalltalk][6]) to deal with highly complex concurrency models.

But after playing with some of the examples that appear on the book, I found this exercise at the end of the chapter 8 :

> Write a ring benchmark. Create N processes in a ring. Send a message round the ring M times so that a total of N * M messages get sent. Time how long this takes for different values of N and M. 

Ok, so here it is my solution ([ring.erl][7]):

```erlang
-module (ring).
-export ([start/2]).

start(N, M) ->
     statistics(runtime),
     statistics(wall_clock),
     Main_process = self(),
     io:format("Creating ~p ring processes~n", [N]),
     spawn(fun() -> ring(1, N, M, self(), Main_process) end),
     receive
          ended -> void
     end,
     {_, Time1} = statistics(runtime),
     {_, Time2} = statistics(wall_clock),
     U1 = Time1,
     U2 = Time2,
     io:format("Ring benchmark for ~p processes and ~p messages =
                    ~p (~p) milliseconds~n", [N, M, U1, U2]).

ring(_, N, _, _, _) when(N =&lt; 0)->
     io:format("Empty ring~n"),
     erlang:error(emptyRing);
ring(_, _, M, _, _) when(M =&lt; 0)->
     io:format("No messages to send~n"),
     erlang:error(noMessagesToSend);
ring(N, N, M, First_process, Main_process) ->
     io:format("Ring process ~p (~p) created~n", [N, self()]),
     io:format("Sending ~p messages through the ring~n", [M]),
     First_process ! {send, main_process, Main_process},
     loop(M, N, N, First_process, Main_process);
ring(I, N, M, First_process, Main_process) ->
     io:format("Ring process ~p (~p) created~n", [I, self()]),
     Next_process = spawn(fun() -> 
          ring(I+1, N, M, First_process, Main_process) end),
     loop(M, I, N, Next_process, Main_process).

loop(0, N, N, _, Main_process) ->
     io:format("Ring process ~p (~p) finished~n", [N, self()]),
     Main_process ! ended;
loop(0, I, _, _, _) -> 
     io:format("Ring process ~p (~p) finished~n", [I, self()]);
loop(M, I, N, Next_process, Main_process) ->
     receive
          {send, From, From_process} ->
               io:format("Process ~p (~p) received message ~p 
                    from process ~p (~p) ~n", [I, self(), M, From, From_process]),
               Next_process ! {send, I, self()},
               loop(M-1, I, N, Next_process, Main_process)
     end.
```

And here the [benchmark results][8] based on Erlang R11B, two different configuration machines and running the above code but without I/O ([ring_noio.erl][9]):

  1. Mac OS-X 10.4.10:
  * Processor: Intel Core 2 Duo Processor 2.2 GHz
  * Memory: 2 Gb 667 MHz DDR2

  2. Windows XP Professional SP2:
  * Processor: AMD Athlon 64 X2 Dual Core Processor 4200+ (working each core at 2.2 GHz)
  * Memory: 2 Gb 667 MHz DDR2

[<img src='/blog/images/2007/08/erlang-1.jpg' alt='Erlang ring problem: Benchmark' width="450" height="270" />][10]

The exercise illustrates how long it takes to spawn a large number of processes and the cost of message passing between them. There is no parallelism in this exercise, as there is only one process active at a time (the others are waiting for a message), but demonstrates how well Erlang can deal with lots of processes and lots of sending and receiving messages. Although I believe I need to do more serious tests, creating 10.000 process and passing 100 million messages in 35 seconds is a great mark.

The second part of the exercise is to write a similar program in some other programming language and to compare the results. Check these links to see some results:

  * [Performance Measurements of Threads in Java and Processes in Erlang][11]
  * [Erlang vs. Stackless python: a first benchmark][12]
  * [Benchmarking Java Vs Erlang][13]
  * [Erlang, Termite and a Blog][14]
  * [Erlang processes vs. Java threads][15]



Next chapters: distributed programming, OTP and Mnesia (the Erlang Database).

 [1]: http://www.rodenas.org/blog/2007/08/07/learning-erlang/
 [2]: http://www.erlang.org/
 [3]: http://en.wikipedia.org/wiki/Pattern_matching
 [4]: http://en.wikipedia.org/wiki/Actor_model
 [5]: http://en.wikipedia.org/wiki/Scala_%28programming_language%29
 [6]: http://en.wikipedia.org/wiki/Smalltalk
 [7]: /blog/images/2007/08/ring.erl
 [8]: http://spreadsheets.google.com/pub?key=pZQna6NUYg09EEhnbyMOsVw
 [9]: /blog/images/2007/08/ring_noio.erl
 [10]: /blog/images/2007/08/erlang-1.jpg
 [11]: http://www.sics.se/~joe/ericsson/du98024.html
 [12]: http://muharem.wordpress.com/2007/07/31/erlang-vs-stackless-python-a-first-benchmark/
 [13]: http://weblog.plexobject.com/?p=1570
 [14]: http://jaortega.wordpress.com/2007/05/14/erlang-termite-and-a-blog/
 [15]: http://www.lshift.net/blog/2006/09/10/erlang-processes-vs-java-threads

## Comments

### Comment by Simon on 2007-08-30 07:48:07 +0000
Your solution is clearer to me than the one over at <a href="http://muharem.wordpress.com/" rel="nofollow">http://muharem.wordpress.com/</a> though I found that a very interesting article, too.

Thanks for this. I&#8217;m working my way through the book v-e-r-y slowly as coming from a purely flash development background almost all Erlang concepts are new on me.

But, damn, there&#8217;s just something about erlang that makes me want to learn it!

### Comment by Ernest Micklei on 2008-05-27 14:22:04 +0000
Please have a look at my version:
  
<a href="http://philemonworks.wordpress.com/2008/05/23/ring-benchmark-my-first-concurrent-erlang/" rel="nofollow">http://philemonworks.wordpress.com/2008/05/23/ring-benchmark-my-first-concurrent-erlang/</a>

I did not spend much time on gathering significant statistics. Getting a readable compact program was far more challenging.

### Comment by David Grenier on 2011-06-11 03:22:52 +0000
Hello,

The following implementation in C# using Rx.NET runs in 1min58 in LINQPad on quad core <Q6600@2.4ghz>:

```
var listeners =
	  
Enumerable.Range(0, 10000)
		  
.Select(_ => new Subject(Scheduler.TaskPool))
		  
.MemoizeAll();

listeners.Publish(o => o.Zip(o.Skip(1), (l, r) => new { l, r}))
	  
.Run(o => o.l.Subscribe(o.r));

Observable
	  
.Range(0, 10000)
	  
.Delay(TimeSpan.FromMilliseconds(1000))
	  
.Subscribe(listeners.First());

listeners.Last().Last().Dump();

I also have the following F# implementation running in 50s on the same machine (F# interactive):

type Agent = MailboxProcessor

let count = 10000
  
let now = System.DateTime.Now

Agent.Start (fun inbox ->
      
async {
          
while true do
              
let! msg = inbox.Receive()
              
if msg = count then
                  
printfn &#8220;%A&#8221; (System.DateTime.Now &#8211; now).TotalMilliseconds })
  
|> Seq.unfold (fun next ->
                  
let agent = Agent.Start (fun inbox ->
                                  
async {
                                      
while true do
                                          
let! msg = inbox.Receive()
                                          
next.Post msg } )
                  
Some (agent, agent))
  
|> Seq.nth count
  
|> (fun agent -> for i in 1..count do agent.Post i)
```

Both code seems to scale pretty well versus the timing I had on my dual core laptop at work (T7400), although I only remember the time for the C#-Rx version at 5min50.

David