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
mind is the <b>io programming language</b>.

What is io programming language you ask? Well simply put, the io programming
language boasts expressiveness through simplicity (well according to their
website anyways...). It establishes that the language is pure, dynamic,
concurrent and accessible. You can find more information about the io language
[here](http://iolanguage.org/about.html).


Artifact #1 - Need a Tissue? Grab an Issue 
==========================================
After forking the repository I immediately fled to the README.md in search of
the build instructions. The instructions were fairly straightforward,
especially if you already have homebrew installed on your OSX machine. You
simply type the command <i>brew install io</i> and watch the magic
unfold. Great! Works like a charm! I am now ready to write fizz-buzz in the io
language! But what if I wanted to build it from scratch on my own? Well this
is where I ran into some issues, despite the simple step by step instructions. 
I could correctly complete the first three steps in the instructions, however, when 
I ran the command <i>make install</i>, the install exploded. After countless 
attempts of being unsuccessful, I decided to temporarily give up (Artifact #2 
will resume the adventure). 

I went back to the drawing board, or in this case, the main io repository, to
check out the list of ongoing issues. The one that immediately grabbed my
attention was at the top of the list, <i>Issue #324 - Misspelling of
"occurrence"</i>. I immediately knew this was something manageable for me to
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

## Artifact #2 - Resuming the Adventure
=======================================
As promised, I am now going to talk about the adventures of getting the io
language to build properly on OSX. When I followed the README.md instructions,
as I said earlier, it failed to build on the command <i>make
install</i>. Luckily for me, there was useful output that helped me debug
where the issue was occurring. 

Error Output
------------
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

Using the above error output, I could see there was something going wrong with
Python in the build process. The first thing I looked at was cmake, which I am
not familiar with at all. When sifting through the repository, I noticed that
every folder had a CMakeLists.txt file. I also noticed there was a Python
specific folder in the addons directory with a CMakeLists.txt file as
well. When looking at the CMakeLists.txt file it looked Greek to me (and I do
not understand Greek), so I decided to look up the CMake documentation in
order to figure out what was going on. It didn't clear up things enough for
me, so I next restarted the build process and looked at the output of what
CMake produced. A particular line of the build immediately caught my eye.

<p>
-- Found PythonLibs: 
/Library/Frameworks/Python.framework/Versions/3.5/lib/libpython3.5m.dylib 
(found version "3.5.1") 
</p>

Since the io programming language has been around for a while, this made me
consider if there was something wrong with the versioning. Python had many
implementation changes when it transitioned from v2 to v3. Even though I had
both versions installed, it seemed that CMake was grabbing the wrong
version. After searching online, I discovered that in the CMakeLists.txt file
you could specify a EXACT field with a version number. Once I made that
change, I tried to build it from scratch. With the change I received an error
through CMake because it could only detect the most recent version of Python
on OSX. I decided that maybe I should update the io language to use Python v3
as opposed to Python v2. I changed the EXACT field to REQUIRED and specified
Python v3.3 because some specific (and needed) methods for particular objects
were introduced at v3.3.


Next, I decided to search the web for the particular functions _PyInt_AS_LONG
and _PyString_AsString which kept bringing me to Python v2.7 documentation. I
began to wonder if these particular functions were deprecated when v3 was
released, and stumbled upon this particular
[document](https://docs.python.org/3/howto/cporting.html). This documentation
stated that _PyInt_ functions was replaced with _PyLong_ functions and that
the _PyString_ functions were replaced by _PyUnicode_ functions. I went
through all the C code and started to replace the functions with v3
functions. This was easy for the object change of _PyInt_ to _PyLong_ because
a lot of the old functions existed within the new object and it was just a
matter of changing the object name. But the _PyString_ to _PyUnicode_ used
different names for some of their methods, so I had to look up which methods
were now used and what the proper name was.


After completing this change I could successfully build and install the io
language through the repository. I had to update the README.md as well to
specify the new requirement for building the io language. Once I was satisfied
with my work, I submitted it as a pull request with a reference to the article
that I used to find all the changes for porting Python to v3. It was accepted
into the repository without any conflicts.
