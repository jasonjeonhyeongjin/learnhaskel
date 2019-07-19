<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01//EN"
   "http://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
<title>Starting Out - Learn You a Haskell for Great Good!</title>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<!--<base href="http://learnyouahaskell.com/">-->
<style type="text/css">
	@import url('../reset.css');
	@import url('../style.css');
</style>
<link rel="shortcut icon" href="../favicon.png" type="image/png">
        <link rel="prev" href="../introduction/index.html">
        <link rel="next" href="../types-and-typeclasses/index.html">
<link type="text/css" rel="stylesheet" href="../sh/Styles/SyntaxHighlighter.css">
<link href="../rss.php.html" rel="alternate" type="application/rss+xml" title="Learn You a Haskell for Great Good! feed">
</head>
<body class="introcontent">
<div class="bgwrapper">
    <div id="content">
                <div class="footdiv" style="margin-bottom:25px;">
                <ul>
                    <li style="text-align:left">
                                                        <a href="../introduction/index.html" class="prevlink">Introduction</a>
                                            </li>
                    <li style="text-align:center">
                        <a href="../chapters/index.html">Table of contents</a>
                    </li>
                    <li style="text-align:right">
                                                        <a href="../types-and-typeclasses/index.html" class="nxtlink">Types and Typeclasses</a>
                                            </li>
                </ul>
            </div>
        <h1 style="margin-left:-3px">Starting Out</h1>
<a name="ready-set-go"></a><h2>Ready, set, go!</h2>
<p>
<img src="http://s3.amazonaws.com/lyah/startingout.png" class="right" alt="egg" width="214" height="187">
Alright, let's get started! If you're the sort of horrible person who doesn't read introductions to things and you skipped it, you might want to read the last section in the introduction anyway because it explains what you need to follow this tutorial and how we're going to load functions. The first thing we're going to do is run ghc's interactive mode and call some function to get a very basic feel for haskell. Open your terminal and type in <span class="fixed">ghci</span>. You will be greeted with something like this.
</p>
<pre name="code" class="haskell: ghci">
GHCi, version 6.8.2: http://www.haskell.org/ghc/  :? for help
Loading package base ... linking ... done.
Prelude&gt;</pre>
<p>
Congratulations, you're in GHCI! The prompt here is <span class="fixed">Prelude&gt;</span> but because it can get longer when you load stuff into the session, we're going to use <span class="fixed">ghci&gt;</span>. If you want to have the same prompt, just type in <span class="fixed">:set prompt "ghci&gt; "</span>. 
</p>
<p>
Here's some simple arithmetic.
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; 2 + 15
17
ghci&gt; 49 * 100
4900
ghci&gt; 1892 - 1472
420
ghci&gt; 5 / 2
2.5
ghci&gt;</pre>
<p>
This is pretty self-explanatory. We can also use several operators on one line and all the usual precedence rules are obeyed. We can use parentheses to make the precedence explicit or to change it.
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; (50 * 100) - 4999
1
ghci&gt; 50 * 100 - 4999
1
ghci&gt; 50 * (100 - 4999)
-244950</pre>
<p>
Pretty cool, huh? Yeah, I know it's not but bear with me. A little pitfall to watch out for here is negating numbers. If we want to have a negative number, it's always best to surround it with parentheses. Doing <span class="fixed">5 * -3</span> will make GHCI yell at you but doing <span class="fixed">5 * (-3)</span> will work just fine.
</p>
<p>
Boolean algebra is also pretty straightforward. As you probably know, <span class="fixed">&amp;&amp;</span> means a boolean <i>and</i>, <span class="fixed">||</span> means a boolean <i>or</i>. <span class="fixed">not</span> negates a <span class="fixed">True</span> or a <span class="fixed">False</span>.
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; True &amp;&amp; False
False
ghci&gt; True &amp;&amp; True
True
ghci&gt; False || True
True 
ghci&gt; not False
True
ghci&gt; not (True &amp;&amp; True)
False</pre>
<p>
Testing for equality is done like so.
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; 5 == 5
True
ghci&gt; 1 == 0
False
ghci&gt; 5 /= 5
False
ghci&gt; 5 /= 4
True
ghci&gt; "hello" == "hello"
True </pre>
<p>
What about doing <span class="fixed">5 + "llama"</span> or <span class="fixed">5 == True</span>? Well, if we try the first snippet, we get a big scary error message!
</p>
<pre name="code" class="haskell: ghci">
No instance for (Num [Char])
arising from a use of `+' at &lt;interactive&gt;:1:0-9
Possible fix: add an instance declaration for (Num [Char])
In the expression: 5 + "llama"
In the definition of `it': it = 5 + "llama" </pre>
<p>
Yikes! What GHCI is telling us here is that <span class="fixed">"llama"</span> is not a number and so it doesn't know how to add it to 5. Even if it wasn't <span class="fixed">"llama"</span> but <span class="fixed">"four"</span> or <span class="fixed">"4"</span>, Haskell still wouldn't consider it to be a number. <span class="fixed">+</span> expects its left and right side to be numbers. If we tried to do <span class="fixed">True == 5</span>, GHCI would tell us that the types don't match. Whereas <span class="fixed">+</span> works only on things that are considered numbers, <span class="fixed">==</span> works on any two things that can be compared. But the catch is that they both have to be the same type of thing. You can't compare apples and oranges. We'll take a closer look at types a bit later. Note: you can do <span class="fixed">5 + 4.0</span> because <span class="fixed">5</span> is sneaky and can act like an integer or a floating-point number. <span class="fixed">4.0</span> can't act like an integer, so <span class="fixed">5</span> is the one that has to adapt.
</p>
<p>
You may not have known it but we've been using functions now all along. For instance, <span class="fixed">*</span> is a function that takes two numbers and multiplies them. As you've seen, we call it by sandwiching it between them. This is what we call an <i>infix</i> function. Most functions that aren't used with numbers are <i>prefix</i> functions. Let's take a look at them. 
</p>
<p>
<img src="http://s3.amazonaws.com/lyah/ringring.png" alt="phoen" class="right" width="160" height="161">
Functions are usually prefix so from now on we won't explicitly state that a function is of the prefix form, we'll just assume it. In most imperative languages functions are called by writing the function name and then writing its parameters in parentheses, usually separated by commas. In Haskell, functions are called by writing the function name, a space and then the parameters, separated by spaces. For a start, we'll try calling one of the most boring functions in Haskell.
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; succ 8
9 </pre>
<p>
The <span class="fixed">succ</span> function takes anything that has a defined successor and returns that successor. As you can see, we just separate the function name from the parameter with a space. Calling a function with several parameters is also simple. The functions <span class="fixed">min</span> and <span class="fixed">max</span> take two things that can be put in an order (like numbers!). <span class="fixed">min</span> returns the one that's lesser and <span class="fixed">max</span> returns the one that's greater. See for yourself:
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; min 9 10
9
ghci&gt; min 3.4 3.2
3.2
ghci&gt; max 100 101
101 </pre>

<p>
Function application (calling a function by putting a space after it and then typing out the parameters) has the highest precedence of them all. What that means for us is that these two statements are equivalent.
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; succ 9 + max 5 4 + 1
16
ghci&gt; (succ 9) + (max 5 4) + 1
16
</pre>
<p>
However, if we wanted to get the successor of the product of numbers 9 and 10, we couldn't write <span class="fixed">succ 9 * 10</span> because that would get the successor of 9, which would then be multiplied by 10. So 100. We'd have to write <span class="fixed">succ (9 * 10)</span> to get 91.
</p>
<p>If a function takes two parameters, we can also call it as an infix function by surrounding it with backticks. For instance, the <span class="fixed">div</span> function takes two integers and does integral division between them. Doing <span class="fixed">div 92 10</span> results in a 9. But when we call it like that, there may be some confusion as to which number is doing the division and which one is being divided. So we can call it as an infix function by doing <span class="fixed">92 `div` 10</span> and suddenly it's much clearer. </p>
<p>Lots of people who come from imperative languages tend to stick to the notion that parentheses should denote function application. For example, in C, you use parentheses to call functions like <span class="fixed">foo()</span>, <span class="fixed">bar(1)</span> or <span class="fixed">baz(3, "haha")</span>. Like we said, spaces are used for function application in Haskell. So those functions in Haskell would be <span class="fixed">foo</span>, <span class="fixed">bar 1</span> and <span class="fixed">baz 3 "haha"</span>. So if you see something like <span class="fixed">bar (bar 3)</span>, it doesn't mean that <span class="fixed">bar</span> is called with <span class="fixed">bar</span> and <span class="fixed">3</span> as parameters. It means that we first call the function <span class="fixed">bar</span> with <span class="fixed">3</span> as the parameter to get some number and then we call <span class="fixed">bar</span> again with that number. In C, that would be something like <span class="fixed">bar(bar(3))</span>.</p>
<a name="babys-first-functions"></a><h2>Baby's first functions</h2>
<p>
In the previous section we got a basic feel for calling functions. Now let's try making our own! Open up your favorite text editor and punch in this function that takes a number and multiplies it by two.
</p>
<pre name="code" class="haskell: hs">
doubleMe x = x + x</pre>
<p>
Functions are defined in a similar way that they are called. The function name is followed by parameters seperated by spaces. But when defining functions, there's a <span class="fixed">=</span> and after that we define what the function does. Save this as <span class="fixed">baby.hs</span> or something. Now navigate to where it's saved and run <span class="fixed">ghci</span> from there. Once inside GHCI, do <span class="fixed">:l baby</span>. Now that our script is loaded, we can play with the function that we defined.
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; :l baby
[1 of 1] Compiling Main             ( baby.hs, interpreted )
Ok, modules loaded: Main.
ghci&gt; doubleMe 9
18
ghci&gt; doubleMe 8.3
16.6 </pre>
<p>
Because <span class="fixed">+</span> works on integers as well as on floating-point numbers (anything that can be considered a number, really), our function also works on any number. Let's make a function that takes two numbers and multiplies each by two and then adds them together.
</p>
<pre name="code" class="haskell: hs">
doubleUs x y = x*2 + y*2 </pre>
<p>
Simple. We could have also defined it as <span class="fixed">doubleUs x y = x + x + y + y</span>. Testing it out produces pretty predictable results (remember to append this function to the <span class="fixed">baby.hs</span> file, save it and then do <span class="fixed">:l baby</span> inside GHCI).
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; doubleUs 4 9
26
ghci&gt; doubleUs 2.3 34.2
73.0
ghci&gt; doubleUs 28 88 + doubleMe 123
478
</pre>
<p>
As expected, you can call your own functions from other functions that you made. With that in mind, we could redefine <span class="fixed">doubleUs</span> like this:
</p>
<pre name="code" class="haskell: hs">
doubleUs x y = doubleMe x + doubleMe y </pre>
<p>
This is a very simple example of a common pattern you will see throughout Haskell. Making basic functions that are obviously correct and then combining them into more complex functions. This way you also avoid repetition. What if some mathematicians figured out that 2 is actually 3 and you had to change your program? You could just redefine <span class="fixed">doubleMe</span> to be <span class="fixed">x + x + x</span> and since <span class="fixed">doubleUs</span> calls <span class="fixed">doubleMe</span>, it would automatically work in this strange new world where 2 is 3.
</p>
<p>Functions in Haskell don't have to be in any particular order, so it doesn't matter if you define <span class="fixed">doubleMe</span> first and then  <span class="fixed">doubleUs</span> or if you do it the other way around.</p>
<p>Now we're going to make a function that multiplies a number by 2 but only if that number is smaller than or equal to 100 because numbers bigger than 100 are big enough as it is!
</p>
<pre name="code" class="haskell: hs">
doubleSmallNumber x = if x &gt; 100
                        then x
                        else x*2 </pre>
<img src="http://s3.amazonaws.com/lyah/baby.png" alt="this is you" class="left" width="140" height="211">
<p>
Right here we introduced Haskell's if statement. You're probably familiar with if statements from other languages. The difference between Haskell's if statement and if statements in imperative languages is that the else part is mandatory in Haskell. In imperative languages you can just skip a couple of steps if the condition isn't satisfied but in Haskell every expression and function must return something. We could have also written that if statement in one line but I find this way more readable. Another thing about the if statement in Haskell is that it is an <i>expression</i>. An expression is basically a piece of code that returns a value. <span class="fixed">5</span> is an expression because it returns 5, <span class="fixed">4 + 8</span> is an expression, <span class="fixed">x + y</span> is an expression because it returns the sum of <span class="fixed">x</span> and <span class="fixed">y</span>. Because the else is mandatory, an if statement will always return something and that's why it's an expression. If we wanted to add one to every number that's produced in our previous function, we could have written its body like this.
</p>
<pre name="code" class="haskell: hs">
doubleSmallNumber' x = (if x &gt; 100 then x else x*2) + 1
</pre>
<p>
Had we omitted the parentheses, it would have added one only if <span class="fixed">x</span> wasn't greater than 100. Note the <span class="fixed">'</span> at the end of the function name. That apostrophe doesn't have any special meaning in Haskell's syntax. It's a valid character to use in a function name. We usually use <span class="fixed">'</span> to either denote a strict version of a function (one that isn't lazy) or a slightly modified version of a function or a variable. Because <span class="fixed">'</span> is a valid character in functions, we can make a function like this.
</p>
<pre name="code" class="haskell: hs">
conanO'Brien = "It's a-me, Conan O'Brien!" </pre>
<p>
There are two noteworthy things here. The first is that in the function name we didn't capitalize Conan's name. That's because functions can't begin with uppercase letters. We'll see why a bit later. The second thing is that this function doesn't take any parameters. When a function doesn't take any parameters, we usually say it's a <i>definition</i> (or a <i>name</i>). Because we can't change what names (and functions) mean once we've defined them, <span class="fixed">conanO'Brien</span> and the string <span class="fixed">"It's a-me, Conan O'Brien!"</span> can be used interchangeably.
</p>
<a name="an-intro-to-lists"></a><h2>An intro to lists</h2>
<p>
<img src="http://s3.amazonaws.com/lyah/list.png" alt="BUY A DOG" class="left" width="150" height="103">
Much like shopping lists in the real world, lists in Haskell are very useful. It's the most used data structure and it can be used in a multitude of different ways to model and solve a whole bunch of problems. Lists are SO awesome. In this section we'll look at the basics of lists, strings (which are lists) and list comprehensions.
</p>
<p>
In Haskell, lists are a <em>homogenous</em> data structure. It stores several elements of the same type. That means that we can have a list of integers or a list of characters but we can't have a list that has a few integers and then a few characters. And now, a list!
</p>
<div class="hintbox"><em>Note</em>: We can use the <span class="fixed">let</span> keyword to define a name right in GHCI. Doing <span class="fixed">let a = 1</span> inside GHCI is the equivalent of writing <span class="fixed">a = 1</span> in a script and then loading it. </div>
<pre name="code" class="haskell: ghci">
ghci&gt; let lostNumbers = [4,8,15,16,23,42]
ghci&gt; lostNumbers
[4,8,15,16,23,42]
</pre>
<p>
As you can see, lists are denoted by square brackets and the values in the lists are separated by commas. If we tried a list like <span class="fixed">[1,2,'a',3,'b','c',4]</span>, Haskell would complain that characters (which are, by the way, denoted as a character between single quotes) are not numbers. Speaking of characters, strings are just lists of characters. <span class="fixed">"hello"</span> is just syntactic sugar for <span class="fixed">['h','e','l','l','o']</span>. Because strings are lists, we can use list functions on them, which is really handy. 
</p>
<p>A common task is putting two lists together. This is done by using the <span class="fixed">++</span> operator. </p>
<pre name="code" class="haskell: ghci">
ghci&gt; [1,2,3,4] ++ [9,10,11,12]
[1,2,3,4,9,10,11,12]
ghci&gt; "hello" ++ " " ++ "world"
"hello world"
ghci&gt; ['w','o'] ++ ['o','t']
"woot"
</pre>
<p>
Watch out when repeatedly using the <span class="fixed">++</span> operator on long strings. When you put together two lists (even if you append a singleton list to a list, for instance: <span class="fixed">[1,2,3] ++ [4]</span>), internally, Haskell has to walk through the whole list on the left side of <span class="fixed">++</span>. That's not a problem when dealing with lists that aren't too big. But putting something at the end of a list that's fifty million entries long is going to take a while. However, putting something at the beginning of a list using the <span class="fixed">:</span> operator (also called the cons operator) is instantaneous.
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; 'A':" SMALL CAT"
"A SMALL CAT"
ghci&gt; 5:[1,2,3,4,5]
[5,1,2,3,4,5]
</pre>
<p>
Notice how <span class="fixed">:</span> takes a number and a list of numbers or a character and a list of characters, whereas <span class="fixed">++</span> takes two lists. Even if you're adding an element to the end of a list with <span class="fixed">++</span>, you have to surround it with square brackets so it becomes a list. </p>
<p>
<span class="fixed">[1,2,3]</span> is actually just syntactic sugar for <span class="fixed">1:2:3:[]</span>. <span class="fixed">[]</span> is an empty list. If we prepend <span class="fixed">3</span> to it, it becomes <span class="fixed">[3]</span>. If we prepend <span class="fixed">2</span> to that, it becomes <span class="fixed">[2,3]</span>, and so on.
</p>
<p class="hintbox"><em>Note:</em> <span class="fixed">[]</span>, <span class="fixed">[[]]</span> and<span class="fixed">[[],[],[]]</span> are all different things. The first one is an empty list, the seconds one is a list that contains one empty list, the third one is a list that contains three empty lists.</p>
<p>If you want to get an element out of a list by index, use <span class="fixed">!!</span>. The indices start at 0.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; "Steve Buscemi" !! 6
'B'
ghci&gt; [9.4,33.2,96.2,11.2,23.25] !! 1
33.2
</pre>
<p>But if you try to get the sixth element from a list that only has four elements, you'll get an error so be careful!</p>
<p>
Lists can also contain lists. They can also contain lists that contain lists that contain lists &hellip;
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; let b = [[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3]]
ghci&gt; b
[[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3]]
ghci&gt; b ++ [[1,1,1,1]]
[[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3],[1,1,1,1]]
ghci&gt; [6,6,6]:b
[[6,6,6],[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3]]
ghci&gt; b !! 2
[1,2,2,3,4] </pre>
<p>The lists within a list can be of different lengths but they can't be of different types. Just like you can't have a list that has some characters and some numbers, you can't have a list that has some lists of characters and some lists of numbers.</p>
<p>Lists can be compared if the stuff they contain can be compared. When using <span class="fixed">&lt;</span>, <span class="fixed">&lt;=</span>, <span class="fixed">&gt;</span> and <span class="fixed">&gt;=</span> to compare lists, they are compared in lexicographical order. First the heads are compared. If they are equal then the second elements are compared, etc.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; [3,2,1] &gt; [2,1,0]
True
ghci&gt; [3,2,1] &gt; [2,10,100]
True
ghci&gt; [3,4,2] &gt; [3,4]
True
ghci&gt; [3,4,2] &gt; [2,4]
True
ghci&gt; [3,4,2] == [3,4,2]
True
</pre>
<p>
What else can you do with lists? Here are some basic functions that operate on lists.
</p>
<p><span class="label function">head</span> takes a list and returns its head. The head of a list is basically its first element.
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; head [5,4,3,2,1]
5 </pre>
<p><span class="label function">tail</span> takes a list and returns its tail. In other words, it chops off a list's head.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; tail [5,4,3,2,1]
[4,3,2,1] </pre>
<p><span class="label function">last</span> takes a list and returns its last element.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; last [5,4,3,2,1]
1 </pre>
<p><span class="label function">init</span> takes a list and returns everything except its last element.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; init [5,4,3,2,1]
[5,4,3,2] </pre>
<p>If we think of a list as a monster, here's what's what.</p>
<img src="http://s3.amazonaws.com/lyah/listmonster.png" alt="list monster" class="center" width="580" height="290">
<p>But what happens if we try to get the head of an empty list?</p>
<pre name="code" class="haskell: ghci">
ghci&gt; head []
*** Exception: Prelude.head: empty list</pre>
<p>Oh my! It all blows up in our face! If there's no monster, it doesn't have a head. When using <span class="fixed">head</span>, <span class="fixed">tail</span>, <span class="fixed">last</span> and <span class="fixed">init</span>, be careful not to use them on empty lists. This error cannot be caught at compile time so it's always good practice to take precautions against accidentally telling Haskell to give you some elements from an empty list.
<p><span class="label function">length</span> takes a list and returns its length, obviously.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; length [5,4,3,2,1]
5</pre>
<p><span class="label function">null</span> checks if a list is empty. If it is, it returns <span class="fixed">True</span>, otherwise it returns <span class="fixed">False</span>. Use this function instead of <span class="fixed">xs == []</span> (if you have a list called <span class="fixed">xs</span>)</p>
<pre name="code" class="haskell: ghci">
ghci&gt; null [1,2,3]
False
ghci&gt; null []
True</pre>
<p><span class="label function">reverse</span> reverses a list.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; reverse [5,4,3,2,1]
[1,2,3,4,5]</pre>
<p><span class="label function">take</span> takes number and a list. It extracts that many elements from the beginning of the list. Watch.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; take 3 [5,4,3,2,1]
[5,4,3]
ghci&gt; take 1 [3,9,3]
[3]
ghci&gt; take 5 [1,2]
[1,2]
ghci&gt; take 0 [6,6,6]
[]</pre>
<p>See how if we try to take more elements than there are in the list, it just returns the list. If we try to take 0 elements, we get an empty list.</p>
<p><span class="label function">drop</span> works in a similar way, only it drops the number of elements from the beginning of a list.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; drop 3 [8,4,2,1,5,6]
[1,5,6]
ghci&gt; drop 0 [1,2,3,4]
[1,2,3,4]
ghci&gt; drop 100 [1,2,3,4]
[] </pre>
<p><span class="label function">maximum</span> takes a list of stuff that can be put in some kind of order and returns the biggest element.</p><p> <span class="label function">minimum</span> returns the smallest.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; minimum [8,4,2,1,5,6]
1
ghci&gt; maximum [1,9,2,3,4]
9 </pre>
<p><span class="label function">sum</span> takes a list of numbers and returns their sum.</p><p><span class="label function">product</span> takes a list of numbers and returns their product.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; sum [5,2,1,6,3,2,5,7]
31
ghci&gt; product [6,2,1,2]
24
ghci&gt; product [1,2,5,6,7,9,2,0]
0 </pre>
<p><span class="label function">elem</span> takes a thing and a list of things and tells us if that thing is an element of the list. It's usually called as an infix function because it's easier to read that way.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; 4 `elem` [3,4,5,6]
True
ghci&gt; 10 `elem` [3,4,5,6]
False
</pre>
<p>Those were a few basic functions that operate on lists. We'll take a look at more list functions <a href="../modules/index.html#data-list">later</a></p>
<a name="texas-ranges"></a><h2>Texas ranges</h2>
<p>
<img src="http://s3.amazonaws.com/lyah/cowboy.png" alt="draw" class="right" width="200" height="258">
What if we want a list of all numbers between 1 and 20? Sure, we could just type them all out but obviously that's not a solution for gentlemen who demand excellence from their programming languages. Instead, we'll use ranges. Ranges are a way of making lists that are arithmetic sequences of elements that can be enumerated. Numbers can be enumerated. One, two, three, four, etc. Characters can also be enumerated. The alphabet is an enumeration of characters from A to Z. Names can't be enumerated. What comes after "John"? I don't know.
</p>
<p>To make a list containing all the natural numbers from 1 to 20, you just write <span class="fixed">[1..20]</span>. That is the equivalent of writing <span class="fixed">[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]</span> and there's no difference between writing one or the other except that writing out long enumeration sequences manually is stupid.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; [1..20]
[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
ghci&gt; ['a'..'z']
"abcdefghijklmnopqrstuvwxyz"
ghci&gt; ['K'..'Z']
"KLMNOPQRSTUVWXYZ" </pre>
<p>
Ranges are cool because you can also specify a step. What if we want all even numbers between 1 and 20? Or every third number between 1 and 20?
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; [2,4..20]
[2,4,6,8,10,12,14,16,18,20]
ghci&gt; [3,6..20]
[3,6,9,12,15,18] </pre>
<p>It's simply a matter of separating the first two elements with a comma and then specifying what the upper limit is. While pretty smart, ranges with steps aren't as smart as some people expect them to be. You can't do <span class="fixed">[1,2,4,8,16..100]</span> and expect to get all the powers of 2. Firstly because you can only specify one step. And secondly because some sequences that aren't arithmetic are ambiguous if given only by a few of their first terms.
</p>
<p>To make a list with all the numbers from 20 to 1, you can't just do <span class="fixed">[20..1]</span>, you have to do <span class="fixed">[20,19..1]</span>.</p>
<p>Watch out when using floating point numbers in ranges! Because they are not completely precise (by definition), their use in ranges can yield some pretty funky results.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; [0.1, 0.3 .. 1]
[0.1,0.3,0.5,0.7,0.8999999999999999,1.0999999999999999]
</pre>
<p>My advice is not to use them in list ranges.</p>
<p>
You can also use ranges to make infinite lists by just not specifying an upper limit. Later we'll go into more detail on infinite lists. For now, let's examine how you would get the first 24 multiples of 13. Sure, you could do <span class="fixed">[13,26..24*13]</span>. But there's a better way: <span class="fixed">take 24 [13,26..]</span>. Because Haskell is lazy, it won't try to evaluate the infinite list immediately because it would never finish. It'll wait to see what you want to get out of that infinite lists. And here it sees you just want the first 24 elements and it gladly obliges.
</p>
<p>A handful of functions that produce infinite lists:</p>
<p><span class="label function">cycle</span> takes a list and cycles it into an infinite list. If you just try to display the result, it will go on forever so you have to slice it off somewhere.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; take 10 (cycle [1,2,3])
[1,2,3,1,2,3,1,2,3,1]
ghci&gt; take 12 (cycle "LOL ")
"LOL LOL LOL " </pre>
<p><span class="label function">repeat</span> takes an element and produces an infinite list of just that element. It's like cycling a list with only one element.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; take 10 (repeat 5)
[5,5,5,5,5,5,5,5,5,5]
</pre>
<p>Although it's simpler to just use the <span class="label function">replicate</span> function if you want some number of the same element in a list. <span class="fixed">replicate 3 10</span> returns <span class="fixed">[10,10,10]</span>.</p>
<a name="im-a-list-comprehension"></a><h2>I'm a list comprehension</h2>
<p>
<img src="http://s3.amazonaws.com/lyah/kermit.png" alt="frog" class="left" width="180" height="156">
If you've ever taken a course in mathematics, you've probably run into <i>set comprehensions</i>. They're normally used for building more specific sets out of general sets. A basic comprehension for a set that contains the first ten even natural numbers is <img src="http://s3.amazonaws.com/lyah/setnotation.png" alt="set notation">. The part before the pipe is called the output function, <span class="fixed">x</span> is the variable, <span class="fixed">N</span> is the input set and <span class="fixed">x &lt;= 10</span> is the predicate. That means that the set contains the doubles of all natural numbers that satisfy the predicate.
</p>
<p>If we wanted to write that in Haskell, we could do something like <span class="fixed">take 10 [2,4..]</span>. But what if we didn't want doubles of the first 10 natural numbers but some kind of more complex function applied on them? We could use a list comprehension for that. List comprehensions are very similar to set comprehensions. We'll stick to getting the first 10 even numbers for now. The list comprehension we could use is <span class="fixed">[x*2 | x &lt;- [1..10]]</span>. <span class="fixed">x</span> is drawn from <span class="fixed">[1..10]</span> and for every element in <span class="fixed">[1..10]</span> (which we have bound to <span class="fixed">x</span>), we get that element, only doubled. Here's that comprehension in action. </p>
<pre name="code" class="haskell: ghci">
ghci&gt; [x*2 | x <- [1..10]]
[2,4,6,8,10,12,14,16,18,20]
</pre>
<p>As you can see, we get the desired results. Now let's add a condition (or a predicate) to that comprehension. Predicates go after the binding parts and are separated from them by a comma. Let's say we want only the elements which, doubled, are greater than or equal to 12.
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; [x*2 | x <- [1..10], x*2 >= 12]
[12,14,16,18,20]
</pre>
<p>Cool, it works. How about if we wanted all numbers from 50 to 100 whose remainder when divided with the number 7 is 3? Easy.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; [ x | x &lt;- [50..100], x `mod` 7 == 3]
[52,59,66,73,80,87,94] </pre>
<p>Success! Note that weeding out lists by predicates is also called <em>filtering</em>. We took a list of numbers and we filtered them by the predicate. Now for another example. Let's say we want a comprehension that replaces each odd number greater than 10 with <span class="fixed">"BANG!"</span> and each odd number that's less than 10 with <span class="fixed">"BOOM!"</span>. If a number isn't odd, we throw it out of our list. For convenience, we'll put that comprehension inside a function so we can easily reuse it.</p>
<pre name="code" class="haskell: ghci">
boomBangs xs = [ if x &lt; 10 then "BOOM!" else "BANG!" | x &lt;- xs, odd x] </pre>
<p>The last part of the comprehension is the predicate. The function <span class="fixed">odd</span> returns <span class="fixed">True</span> on an odd number and <span class="fixed">False</span>  on an even one. The element is included in the list only if all the predicates evaluate to <span class="fixed">True</span>.
<pre name="code" class="haskell: hs">
ghci&gt; boomBangs [7..13]
["BOOM!","BOOM!","BANG!","BANG!"] </pre>
<p>We can include several predicates. If we wanted all numbers from 10 to 20 that are not 13, 15 or 19, we'd do:</p> <pre name="code" class="haskell: ghci">
ghci&gt; [ x | x &lt;- [10..20], x /= 13, x /= 15, x /= 19]
[10,11,12,14,16,17,18,20]</pre>
<p>Not only can we have multiple predicates in list comprehensions (an element must satisfy all the predicates to be included in the resulting list), we can also draw from several lists. When drawing from several lists, comprehensions produce all combinations of the given lists and then join them by the output function we supply. A list produced by a comprehension that draws from two lists of length 4 will have a length of 16, provided we don't filter them. If we have two lists, <span class="fixed">[2,5,10]</span> and <span class="fixed">[8,10,11]</span> and we want to get the products of all the possible combinations between numbers in those lists, here's what we'd do.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; [ x*y | x &lt;- [2,5,10], y &lt;- [8,10,11]]
[16,20,22,40,50,55,80,100,110] </pre>
<p>As expected, the length of the new list is 9. What if we wanted all possible products that are more than 50?</p>
<pre name="code" class="haskell: ghci">
ghci&gt; [ x*y | x &lt;- [2,5,10], y &lt;- [8,10,11], x*y &gt; 50]
[55,80,100,110] </pre>
<p>How about a list comprehension that combines a list of adjectives and a list of nouns &hellip; for epic hilarity.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; let nouns = ["hobo","frog","pope"]
ghci&gt; let adjectives = ["lazy","grouchy","scheming"]
ghci&gt; [adjective ++ " " ++ noun | adjective &lt;- adjectives, noun &lt;- nouns]
["lazy hobo","lazy frog","lazy pope","grouchy hobo","grouchy frog",
"grouchy pope","scheming hobo","scheming frog","scheming pope"] </pre>
<p>I know! Let's write our own version of <span class="fixed">length</span>! We'll call it <span class="fixed">length'</span>.</p>
<pre name="code" class="haskell: hs">
length' xs = sum [1 | _ &lt;- xs] </pre>
<p><span class="fixed">_</span> means that we don't care what we'll draw from the list anyway so instead of writing a variable name that we'll never use, we just write <span class="fixed">_</span>. This function replaces every element of a list with <span class="fixed">1</span> and then sums that up. This means that the resulting sum will be the length of our list.</p>
<p>Just a friendly reminder: because strings are lists, we can use list comprehensions to process and produce strings. Here's a function that takes a string and removes everything except uppercase letters from it.</p>
<pre name="code" class="haskell: hs">
removeNonUppercase st = [ c | c &lt;- st, c `elem` ['A'..'Z']] </pre>
<p>
Testing it out:
</p>
<pre name="code" class="haskell: ghci">
ghci&gt; removeNonUppercase "Hahaha! Ahahaha!"
"HA"
ghci&gt; removeNonUppercase "IdontLIKEFROGS"
"ILIKEFROGS" </pre>
<p>The predicate here does all the work. It says that the character will be included in the new list only if it's an element of the list <span class="fixed">['A'..'Z']</span>. Nested list comprehensions are also possible if you're operating on lists that contain lists. A list contains several lists of numbers. Let's remove all odd numbers without flattening the list.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; let xxs = [[1,3,5,2,3,1,2,4,5],[1,2,3,4,5,6,7,8,9],[1,2,4,2,1,6,3,1,3,2,3,6]]
ghci&gt; [ [ x | x &lt;- xs, even x ] | xs &lt;- xxs]
[[2,2,4],[2,4,6,8],[2,4,2,6,2,6]]
</pre>
<p>You can write list comprehensions across several lines. So if you're not in GHCI, it's better to split longer list comprehensions across multiple lines, especially if they're nested.</p>
<a name="tuples"></a><h2>Tuples</h2>
<img src="http://s3.amazonaws.com/lyah/tuple.png" alt="tuples" class="right" width="160" height="162">
<p>In some ways, tuples are like lists &mdash; they are a way to store several values into a single value. However, there are a few fundamental differences. A list of numbers is a list of numbers. That's its type and it doesn't matter if it has only one number in it or an infinite amount of numbers. Tuples, however, are used when you know exactly how many values you want to combine and its type depends on how many components it has and the types of the components. They are denoted with parentheses and their components are separated by commas.</p>
<p>Another key difference is that they don't have to be homogenous. Unlike a list, a tuple can contain a combination of several types.</p>
<p>Think about how we'd represent a two-dimensional vector in Haskell. One way would be to use a list. That would kind of work. So what if we wanted to put a couple of vectors in a list to represent points of a shape on a two-dimensional plane? We could do something like <span class="fixed">[[1,2],[8,11],[4,5]]</span>. The problem with that method is that we could also do stuff like <span class="fixed">[[1,2],[8,11,5],[4,5]]</span>, which Haskell has no problem with since it's still a list of lists with numbers but it kind of doesn't make sense. But a tuple of size two (also called a pair) is its own type, which means that a list can't have a couple of pairs in it and then a triple (a tuple of size three), so let's use that instead. Instead of surrounding the vectors with square brackets, we use parentheses: <span class="fixed">[(1,2),(8,11),(4,5)]</span>. What if we tried to make a shape like <span class="fixed">[(1,2),(8,11,5),(4,5)]</span>? Well, we'd get this error:</p>
<pre name="code" class="haskell: ghci">
Couldn't match expected type `(t, t1)'
against inferred type `(t2, t3, t4)'
In the expression: (8, 11, 5)
In the expression: [(1, 2), (8, 11, 5), (4, 5)]
In the definition of `it': it = [(1, 2), (8, 11, 5), (4, 5)]
</pre>
<p>It's telling us that we tried to use a pair and a triple in the same list, which is not supposed to happen. You also couldn't make a list like <span class="fixed">[(1,2),("One",2)]</span> because the first element of the list is a pair of numbers and the second element is a pair consisting of a string and a number. Tuples can also be used to represent a wide variety of data. For instance, if we wanted to represent someone's name and age in Haskell, we could use a triple: <span class="fixed">("Christopher", "Walken", 55)</span>. As seen in this example, tuples can also contain lists.</p>
<p>Use tuples when you know in advance how many components some piece of data should have. Tuples are much more rigid because each different size of tuple is its own type, so you can't write a general function to append an element to a tuple &mdash; you'd have to write a function for appending to a pair, one function for appending to a triple, one function for appending to a 4-tuple, etc.</p>
<p>While there are singleton lists, there's no such thing as a singleton tuple. It doesn't really make much sense when you think about it. A singleton tuple would just be the value it contains and as such would have no benefit to us.</p>
<p>Like lists, tuples can be compared with each other if their components can be compared. Only you can't compare two tuples of different sizes, whereas you can compare two lists of different sizes. Two useful functions that operate on pairs:</p>
<p><span class="label function">fst</span> takes a pair and returns its first component.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; fst (8,11)
8
ghci&gt; fst ("Wow", False)
"Wow"</pre>
<p><span class="label function">snd</span> takes a pair and returns its second component. Surprise!</p>
<pre name="code" class="haskell: ghci">
ghci&gt; snd (8,11)
11
ghci&gt; snd ("Wow", False)
False</pre>
<div class="hintbox"><em>Note:</em> these functions operate only on pairs. They won't work on triples, 4-tuples, 5-tuples, etc. We'll go over extracting data from tuples in different ways a bit later.</div>
<p>A cool function that produces a list of pairs: <span class="label function">zip</span>. It takes two lists and then zips them together into one list by joining the matching elements into pairs. It's a really simple function but it has loads of uses. It's especially useful for when you want to combine two lists in a way or traverse two lists simultaneously. Here's a demonstration.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; zip [1,2,3,4,5] [5,5,5,5,5]
[(1,5),(2,5),(3,5),(4,5),(5,5)]
ghci&gt; zip [1 .. 5] ["one", "two", "three", "four", "five"]
[(1,"one"),(2,"two"),(3,"three"),(4,"four"),(5,"five")]
</pre>
<p>It pairs up the elements and produces a new list. The first element goes with the first, the second with the second, etc. Notice that because pairs can have different types in them, <span class="fixed">zip</span> can take two lists that contain different types and zip them up. What happens if the lengths of the lists don't match?</p>
<pre name="code" class="haskell: ghci">
ghci&gt; zip [5,3,2,6,2,7,2,5,4,6,6] ["im","a","turtle"]
[(5,"im"),(3,"a"),(2,"turtle")]
</pre>
<p>The longer list simply gets cut off to match the length of the shorter one. Because Haskell is lazy, we can zip finite lists with infinite lists:</p>
<pre name="code" class="haskell: ghci">
ghci&gt; zip [1..] ["apple", "orange", "cherry", "mango"]
[(1,"apple"),(2,"orange"),(3,"cherry"),(4,"mango")]
</pre>
<img src="http://s3.amazonaws.com/lyah/pythag.png" alt="look at meee" class="center" width="350" height="315">
<p>Here's a problem that combines tuples and list comprehensions: which right triangle that has integers for all sides and all sides equal to or smaller than 10 has a perimeter of 24? First, let's try generating all triangles with sides equal to or smaller than 10:</p>
<pre name="code" class="haskell: ghci">ghci&gt; let triangles = [ (a,b,c) | c &lt;- [1..10], b &lt;- [1..10], a &lt;- [1..10] ] </pre>
<p>We're just drawing from three lists and our output function is combining them into a triple. If you evaluate that by typing out <span class="fixed">triangles</span> in GHCI, you'll get a list of all possible triangles with sides under or equal to 10. Next, we'll add a condition that they all have to be right triangles. We'll also modify this function by taking into consideration that side b isn't larger than the hypothenuse and that side a isn't larger than side b.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; let rightTriangles = [ (a,b,c) | c &lt;- [1..10], b &lt;- [1..c], a &lt;- [1..b], a^2 + b^2 == c^2] </pre>
<p>We're almost done. Now, we just modify the function by saying that we want the ones where the perimeter is 24.</p>
<pre name="code" class="haskell: ghci">
ghci&gt; let rightTriangles' = [ (a,b,c) | c &lt;- [1..10], b &lt;- [1..c], a &lt;- [1..b], a^2 + b^2 == c^2, a+b+c == 24]
ghci&gt; rightTriangles'
[(6,8,10)]
</pre>
<p>And there's our answer! This is a common pattern in functional programming. You take a starting set of solutions and then you apply transformations to those solutions and filter them until you get the right ones.</p>
                <div class="footdiv">
                <ul>
                    <li style="text-align:left">
                                                        <a href="../introduction/index.html" class="prevlink">Introduction</a>
                                            </li>
                    <li style="text-align:center">
                        <a href="../chapters/index.html">Table of contents</a>
                    </li>
                    <li style="text-align:right">
                                                        <a href="../types-and-typeclasses/index.html" class="nxtlink">Types and Typeclasses</a>
                                            </li>
                </ul>
            </div>
        </div>
    <script type="text/javascript" src="../sh/Scripts/shCore.js"></script>
    <script type="text/javascript" src="../shBrushHaskell.js"></script>
    <script type="text/javascript" src="../shBrushPlain.js"></script>
    <script type="text/javascript">
    dp.SyntaxHighlighter.ClipboardSwf = '/sh/Scripts/clipboard.swf';
    dp.SyntaxHighlighter.HighlightAll('code', false, false, false, 1, false);
    </script>
</div>
<script type="text/javascript">
var gaJsHost = (("https:" == document.location.protocol) ? "https://ssl." : "http://www.");
document.write(unescape("%3Cscript src='" + gaJsHost + "google-analytics.com/ga.js' type='text/javascript'%3E%3C/script%3E"));
</script>
<script type="text/javascript">
var pageTracker = _gat._getTracker("UA-4461592-3");
pageTracker._trackPageview();
</script>
</body>
</html>

<!-- Localized -->