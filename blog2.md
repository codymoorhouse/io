April 11th, 2016 <br>
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
advertised as being pure, dynamic, concurrent and accessible. The syntax for
the language is unique and information about the language can be found
[here](http://iolanguage.org/).

Artifact #3 - A Can of FizzBuzz
===============================
In [Artifact #2](/blog1.md#artifact-2---resuming-the-adventure) of my previous
blog my goal was to get the io programming language to build correctly on my
machine. Once this was done, I knew immediately my next goal was to write some
sort of simple program in the io language itself. I noticed that the
repository already had a folder created with some sample programs. What I also
noticed is that it was lacking one of the most important programs out there
(apart from "hello, world" of course). I knew immediately that it was in dire
need the FizzBuzz challenge.

What is the FizzBuzz challenge you ask? Well even if you didn't ask I am going
to explain it briefly. The FizzBuzz challenge is based off a
[game](https://en.wikipedia.org/wiki/Fizz_buzz) that was played with a group
of children to help teach them about division. Players of the game would
sit in a circle and count in turn from 1 to a specified number. For instance
the first chosen player would start by saying 1, then the next player in the
circle would say 2 and so on. The division part came in to play when a number 
was evenly divisible by 3, 5 or both. As the players are counting up, if a
number was divisible by 3, they would say <i>Fizz</i> instead of the number 3.
Likewise, if a number was divisible by 5, the player would say <i>Buzz</i>
instead of the number 5. Finally, if the number was divisible by both, the
player would say <i>Fizz Buzz</i> instead of that number (e.g. 15, 30, 45,
...).

The FizzBuzz challenge was introduced as a coding challenge for screening
applicants interested in a programming job. The applicant would have to write
a program that mimicked the game by printing: a number, Fizz, Buzz, or both
(depending on its divisibility). This small screening challenge has turned
away an embarrassing large amount of applicants who should have had the
necessary skills based on their past experience and education.

When writing the program itself I went to the documentation of the io
language to see the syntax for how to write a program. I also reviewed some of
the sample programs that were already part of the existing project. The syntax
was slightly awkward to work with because it used keywords for things such as
the <i>and</i> and <i>or</i> operators (as opposed to <i>&&</i> and
<i>||</i>). Further to that, when writing conditional/iterative statements,
braces <i>{ }</i> were no longer used for blocks. Instead, consecutive
statements were separated by <i>,</i>'s after the condition. Once you were
done with all your statements, you would conclude the block with a right
parenthesis. I also found the print statements to be backwards to how I would
normally think. To print something out, you specify what you want printed
followed by the keyword <i>print</i>.

E.G.
----
<pre> 
if ([condition], [do something], [do something], ...) 
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
request dating back from December 14, 2013. The io repository owner
[stevedekorte](https://github.com/stevedekorte) stated that he could not
auto-merge the pull request and was asking for mig-hub to fix it. This is
where I decided to spring into action.

My first step into resolving this conflict was to create a new branch,
appropriately named <b>mig-hub-merge-conflict</b>. The problem with my new
branch however is that it was a copy of my local branch, which is not the
intended behavior that I desired. So I went onto GitHub to look at the
network graph for the io programming language to see where mig-hub's changes
first started to appear. I then used the command:

<pre>git reset --hard 8956a60c90f9595c0a61e610c9d00a8d810b3282</pre>

This reset my new branch to the point in time just before mig-hub began to
make changes. I now could pull all of mig-hub's changes without any conflicts,
which is exactly what I did. the next command I issued was:

<pre>git pull https://github.com/mig-hub/io.git</pre>

This command allowed me to grab all of mig-hubs changes and <i>mimic</i> his
repository. It was at this point in time that I could start to deal with the
merge conflicts that would ensue. 

<pre>git merge upstream/master</pre>

To my surprise there was only one conflict. To my next surprise it was a one
line json file the size of North America. Because the repository was so old, I
decided that I would just checkout the latest version because the version
mig-hub had was ancient. Mig-hub's commit said that it only addressed typos
within the file for why it was changed. After I did this, there was no more
merge conflicts. I made a pull request to mig-hub's forked copy of the
repository with my changes. I then realized that the pull request mig-hub
created was from a different branch. So I closed the pull request and started
the entire process over. I just had to add an extra step to make sure that I
was on the correct branch BEFORE I merged with the upstream/master. I issued
the command:

<pre>git checkout -b "implicit-declarations"</pre> 

I then decided it was cruel to just throw away all those typos that mig-hub
had fixed. Utilizing my google skills, I found a
[website](http://tlrobinson.net/projects/javascript-fun/jsondiff/) that takes
two json files and compares them. I took the master branch version and
compared it with mig-hub's version. The website was very nice in that it
highlighted changes with different colors (red - removed, green - added,
yellow - changed). I looked specifically for yellow and found the typos that
mig-hub had found quite quickly. I then made the changes and added that as a
commit to the new [pull request](https://github.com/mig-hub/io/pull/2) I had
made. I then made a comment on the original [pull
request](https://github.com/stevedekorte/io/pull/262) that mig-hub had
created, letting stevedekorte know that I had applied a fix for
mig-hub. 

Normally I would have rebased in a situation like this, but as I
don't have any access to mig-hubs forked copy, I decided to go with a merge,
knowing that he will receive an email for the pull request I created.
