April 11, 2016 <br>
Blog Post #2 <br>
Cody Moorhouse <br>

Table of Contents
=================
 - [Re-Introduction](#re-introduction)
 - [Artifact #3](#artifact-3---a-can-of-fizzbuzz)
 - [Artifact #4](#artifact-4---catching-up)

Re-Introduction
===============

In my [previous blog](/blog1.md#introduction), I went over a brief
introduction of what the io programming language is about. The io programming
language was designed to establish expressiveness through simplicity. It is
advertised as being pure, dynamic, concurent and accessible. The syntax for
the language is unique and information about the language can be found
[here](http://iolanguage.org/about.html).

Artifact #3 - A Can of FizzBuzz
===============================
In [Artifact #2](/blog1.md#artifact-2---resuming-the-adventure) of my previous
blog my goal was to get the io programming language to build correctly on my
machine. Once this was done, I knew immediately my next goal was to write some
sort of simple program in the io language itself. I noticed that the
repository already had a folder created with some sample programs. What I also
noticed is that it was lacking one of the most important simple programs out
there (apart from "hello, world" of course). I knew immediately that it was in
dire need of having a sample program of the FizzBuzz challenge.

What is the FizzBuzz challenge you ask? Well even if you didn't ask I am going
to explain it briefly. The FizzBuzz challenge is based off a
[game](https://en.wikipedia.org/wiki/Fizz_buzz) that was played with a group
of children to help teach them about division. Players of the game would
generally sit in a circle and count in turn from 1 to a specified number. For
instance the first chosen player would start by saying 1, then the next player
in the circle would say 2 and so on. The divison part of the learning came in
to play when a number was evenly divisble by 3 or 5 or both. As the players
are counting, if a number was divisble by 3, they would say <i>Fizz</i>
instead of the number 3. Likewise if a number was divisble by 5, the player
would say <i>Buzz</i> instead of the number 5. If the number was divisible by
both, the player would say <i>Fizz Buzz</i> instead of that number (e.g. 15,
30, 45, ...).

The FizzBuzz challenge was introduced as a coding challenge for screening
applicants interested in a programming job. The applicant would have to write
a program that mimicked the game by printing out a number, Fizz, Buzz, or both
depending on its divisibility. This small screening challenge has turned away
an embarrassing large amount of applicants who should have the neccessary
skills based on their experience. 

When writing the program itself I went to the documentation of the io
language to see the syntax for how to write a program. I also reviewed some of
the sample programs that were already part of the existing project. The syntax
was slightly awkward to work with because it used keywords for things such as
the <i>and</i> and <i>or</i> operators (as opposed to <i>&&</i> and
<i>||</i>). Further to that, when writing conditonal/iterative statements,
braces <i>{ }</i> were no longer used for blocks. Instead a block was started
by a <i>,</i> and ended with a right parenthesis. I also found the print
statements to be backwards to how I would normally think. To print something
out, you specify what you want printed followed by the keyword <i>print</i>.

E.G.
----
<pre> 
if ([condition], [do something]) 
[something] print
</pre>

After I wrote the [program](/samples/misc/FizzBuzz.io) I submitted it as a new
sample program through a [pull
request](https://github.com/stevedekorte/io/pull/330) which was merged in
shortly after.

Artifact #4 - Catching Up
=========================
For my final artifact I decided to look at the pull requests that were
currently listed as outstanding. One [pull
request](https://github.com/stevedekorte/io/pull/262) in particular was
authored by [mig-hub](https://github.com/mig-hub). He had an outstanding pull
reqest dating back from December 14, 2013. The io repository owner
[stevedekorte](https://github.com/stevedekorte) stated that he could not
auto-merge the pull request and was asking for mig-hub to fix it. This is
where I decided to spring into action.

My first step into resolving this conflict was to create a new branch,
appropriately named <b>mig-hub-merge-conflict</b>. The problem with my new
branch however is that it was a copy of my local branch, which is not the
intended behaviour that I desired. So I went onto GitHub to look at the
network graph for the io programming language to see where mig-hub's changes
first started to appear. I then used the command:

<pre> git reset --hard 8956a60c90f9595c0a61e610c9d00a8d810b3282</pre>

This reset my new branch to the point in time just before mig-hub began to
make changes. I now could pull all of mig-hub's changes without any conflicts,
which is exactly what I did. the next command I issed was:

<pre> git pull https://github.com/mig-hub/io.git </pre>

This command allowed me to grab all of mig-hubs changes and <i>mimick</i> his
repository. It was at this point in time that I could start to deal with the
merge conflicts that would ensue. 

<pre> git merge upstream/master </pre>


