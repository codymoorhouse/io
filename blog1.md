March 16, 2016 <br>
Blog Post #1 <br>
Cody Moorhouse <br>


Introduction
============

Looking to work on a cool open-source project that is less mainstream? When
scavenging the slew of projects on GitHub, you are not quite sure what you
will find. You could explore quite a range of possibilities depending on what
makes your taste buds tingle. For instance, you can find many different
repositories that fit under a diverse range of categories, such as: Hacking
Minecraft, Emoji's, Social Impact, and even Programming Languages. In fact,
Apple's very own Swift programming language is exclusively featured as its own
category (probably because it needs the extra attention :wink:). But there are
less known programming languages that also exist on GitHub, the one I have in
mind is the <b>io</b> programming language.

What is io programming language you ask? Well simply put, the io programming
language boasts expressiveness through simplicity (well according to their
website anyways...). It establishes that the language is pure, dynamic,
concurrent and accessible.
ADD MORE INTRO CONTENT HERE
===========================

Artifact #1 - Need a Tissue? Grab an Issue 
==========================================
After forking the repository I immediately fled to the README.md in search of
the build instructions. The instructions were fairly straightforward,
especially if you already have homebrew installed on your OSX machine. You
simply type the command <i>brew install io</i> and watch the magic
unfold. Great! Works like a charm! I am now ready to write fizz-buzz in the io
language! But what if I wanted to build it from scratch on my own? Well this
is where I ran into some issues, even with the simple step by step
instructions. I could correctly get past the first three steps, but when I ran
the command <i>make install</i>, explosions went off. After countless attempts
of being unsuccessful, I decided to temporarily give up (Artifact #2 will
resume the adventure). 

I went back to the drawing board, or in this case the main io repository, to
check out the list of ongoing issues. The one that immediately grabbed my
attention was at the top of the list, <i>Issue #324 - Misspelling of
"occurrence"</i>. I immediately knew this was something manageable for me
accomplish and that my degree has thus far prepared me for this exact
situation. I started by reading the comments that were part of the issue to
see exactly where these devious misspellings showed an <i>occurance</i> (Oops!
Now I am misspelling the word too!). It was at this stage that I decided to
dive into the code (and comments).

In my forked copy, I sifted through the code with a useful program known as
<b>grep</b>. Grep is a useful tool can search through files to look for
specific patterns. I also used flags to help me search through all the files
in a quick and easy fashion. 

Flags
-----
<b>-r</b>: Recursively look for this pattern in any existing
	   subdirectories.<br>
<b>-E</B>: Interpret pattern as an extended regular expression. 

Now, because I specified the '-r' flag, I could start at the base directory
and search all the directories/files at once. The '-E' flag allowed me to use
a regular expression in order to use the 'OR' feature of grep. The command I
ended up using was <b>grep -rE "ocurre|ocurra|occura|occure" \*</b>. The '\*'
part of that bit is a wildcard that will search every directory/file in the
current working directory. Since the working directory was the base directory,
it will search the contents of the entire project for any pattern that matches
ocurre, ocurra, occura or occure. Grep will then tell you which files matched
the pattern with the associated line number. All I had to do was go into each
file and fix the spelling accordingly. Once grep would no longer return any
matches to my specified pattern, I submitted my changes through two pull
requests and they were merged in.

Artifact #2 - Resuming the Adventure
====================================
As promised, I am now going to talk about the adventures of getting the io
language to build properly on OSX. When I followed the README.md instructions,
as I said earlier, it failed to build on the command <i>make
install</i>. Luckily for me, there was useful output that helped me debug
where the issue was occurring. 

Error Output
============
<pre>
[ 79%] Linking C shared library _build/dll/libIoPython.dylib
Undefined symbols for architecture x86_64:
  "_PyInt_AS_LONG", referenced from:
      _convertPy in IoPython.c.o
  "_PyInt_Check", referenced from:
      _convertPy in IoPython.c.o
  "_PyString_AsString", referenced from:
      _convertPy in IoPython.c.o
  "_PyString_Check", referenced from:
      _convertPy in IoPython.c.o
  "_PyString_FromString", referenced from:
      _IoPython_import in IoPython.c.o
      _convertIo in IoPython.c.o
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see
invocation)
make[2]: *** [addons/Python/_build/dll/libIoPython.dylib] Error 1
make[1]: *** [addons/Python/CMakeFiles/IoPython.dir/all] Error 2
make: *** [all] Error 2
</pre>
