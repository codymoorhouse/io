April 11, 2016 <br>
Blog Post #2 <br>
Cody Moorhouse <br>


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

When writing the program itself I fled to the documentation for the io
language to see the syntax for how to write a program. I also reviewed some of
the sample programs that were already part of the existing project. The syntax
was slightly awkward to work with because it used keywords for things such as
the 'and' and 'or' operators (as opposed to '&&' and '||'). Further to that,
when writing conditonal/iterative statements, braces '{ }' were no longer used
for blocks. Instead a block was started by a ',' and ended with a right
parenthesis. 

E.G.
----
<pre> if ([condition], [do something]) </pre>



Artifact #4 -
===============================
