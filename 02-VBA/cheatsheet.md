# Week 2 Cheat Sheet

## Git

Git is a version control (aka source control) tool. One git repo ('repository') corresponds to one folder on your computer. Repos can be synchronized with a remote origin, such as Github or Gitlab. Branching and merging are the two main purposes of git but don't worry about that for now - it just makes a good place to back up code and make it publicly available, too.

To get something onto Github, the steps are:

### 1. Create a folder on your computer. Give it a useful name like homework-week-1. From the terminal (OSX) or Git Bash (Windows), get to your home folder (like /Users/tom/ on OSX or c:\Users\tom on Windows) with these commands:

```
cd
mkdir homework-week-1
```

If you're wondering what Git Bash is, it's a program that provides a Unix-like (Linux is a variant of Unix, which is an operating system like OSX or Windows) terminal (aka command line interface, aka CLI, aka console) on Windows. OSX doesn't need this because it is itself based on Unix. 

__Copy some files__ into that folder (either via the terminal with the `cp` command, or just via the regular file browser/explorer). You need to have [git LFS](https://git-lfs.github.com/) installed to work with the provided UC Berkeley Extension repos, because git is mostly designed to work with text files, not `.xlsx`.

It's good practice to give each repo a README.md file. That's a plain-text file that describes the repo contents and how to use it. The `.md` extension indicates that the file is [markdown](https://https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) - an easy way to write text with formatting. It's worth getting familiar with some basic markdown, because it's how you'll document experiments in your Jupyter notebooks.

BTW, as a technical analyst, a coder, an engineer, a data scientist, or generally just anyone who works with techies, you will be expected to have basic familiarity with the CLI. Try to do as much as you can via the terminal from now on, avoiding the GUI.

### 2. Create a repo on Github.com

Give it the same name as the folder on your computer, i.e. `homework-week-1`.

Github will give you a URL like `https://github.com/tomgrek/homework-week-1.git`. Copy it to the clipboard.

### 3. Meanwhile back on your computer, set up your folder to be tracked by git

Make sure you are inside the `homework-week-1` folder. You can do it like this:

```
cd ~/homework-week-1
```

The ~ (tilde) is a Unix shortcut to your home folder.

Then,

```
git init
git remote add origin https://github.com/tomgrek/homework-week-1.git
```

### 4. Sync your folder with Github (the 'remote origin')

Every time you make changes to a file in the local folder, or create new files in it,

```
git add .
git commit -m "describe the changes you made"
git push origin master
```

This ensures all files in your local folder are tracked by git, 'commits' them (if you mess up and break code later, you can roll back to a previous commit), and pushes those files out to the remote origin (i.e. your Github repo).

Viola, now you can go to your repo on Github and see the files there.

## Anaconda

Ensure you have [Anaconda](https://www.anaconda.com/download/) installed. Anaconda is a distribution of Python that contains everything you need for analytics. It gives you the option of adding to your PATH and I recommend doing that; it only causes problems if you have more than one Python environment which right now you will _not_ have.

Once installed, from the terminal (Anaconda Prompt on Windows - check the Start Menu) you should be able to type `jupyter notebook` whereupon a browser window will open with Jupyter. From there try `New -> Notebook (Python 3)`. Get used to Jupyter because it's your new best friend.

We'll cover it in much more detail, but seriously, if you want to get ahead, use it as much as possible. It's a versatile tool that I use for daily work, hobbies, blogging, presenting (instead of PowerPoint), and indeed I'm writing this cheatsheet in Jupyter.

## Coding in VBA

Many of you had your first experience of coding this week, in VBA ('Visual Basic for Applications'). It's an unpopular, uncommon language - but provides a bridge from the familiarity of Excel to where we're heading.

### General coding stuff

I mentioned 'blank page syndrome' - you've identified a problem to solve, you've taken time to understand the problem and what a solution to it would like like - now what? One of the great things about software engineering is that you can't really break anything - so just get coding and try things out. Fail, try again, fail again, debug, fail again, at some point you arrive at a solution, and usually there are many ways to get there.

In VBA, start by creating a _function_, which lives within a _module_:

```
Sub Do_Something():
End Sub
```

Ok, there's the blank page gone - we have a starting point.

Next, make something, anything, happen:

```
Sub Do_Something():
    MsgBox("Hello Analytics Class")
End Sub
```

Hit play and you should get a popup message. Great, we've confirmed we can make something happen.

I mentioned a couple of stylistic points this week, to recap:

* Indent code blocks to make things easy to read and follow. The code inside a function, or inside a For loop, or inside an If statement, should be pushed out to the right. Whether you do it by spaces or tabs is really up to you.
* Be consistent with variable names and cases: use camelCase or snake_case. Use descriptive variable names.
* Constants - hard-coded variables that don't change in your code - should be in CAPS, for example `SPEED_OF_LIGHT = 299792458`.

### Variables and Cells

Before using a variable we have to create it: `Dim counter as Integer`. Other useful variable types in VBA are `String` and `Double`.

A variable is a container for a value that changes. You can grab a value from Excel into a variable:

```
Dim my_cell_value As Double
my_cell_value = Cells(1,1).Value
my_cell_value = Range("A1").Value
MsgBox(my_cell_value)
```

And you can populate a cell with a variable: 
```
my_cell_value = my_cell_value + 1
Cells(1,1).Value = my_cell_value
```

Remember when referencing cells (or indeed, matrices in general) it's row then column. `Cells(i,j)` refers to the i'th row, j'th column.

Variables can be arrays (aka lists or vectors) too:

```
Dim Ingredients(5) as String
Ingredients(0) = "Chocolate Bar"
MsgBox(Ingredients(0))
```

Finally, remember that `Cells(1,1)` refers to the cell itself, an abstract object. One of the cell's properties (aka attributes) is the value inside it, which we access with `.Value`. As we discovered, we can access other properties too:

```
Range("A1:A3").Font.ColorIndex = 3
Cells("1,1").Interior.ColorIndex = 3
Range("B2").Style = "Currency"
```

### Conditionals (aka If statements)

> If something is true, then do [x]. Otherwise, do [y].

> If it's raining, wear a coat. Otherwise, wear a t-shirt.

A computer program executes all its statements/lines in order, but it won't be very useful unless we can control that flow somehow. So we learned about the If statement:

```
Dim weather As String
Dim wear As String

weather = "raining"

If weather = "raining" then
wear = "coat"
Else
wear = "t-shirt"
End If
```

You don't have to have an `Else` if you don't want. We also looked at `Elseif`. If the first condition is satisfied, the `elseif`s will never be executed.

The If condition doesn't have to be an exact "equals". It could be `>=` (greater than or equal to), or `<=`, or `<`, or `>`, or `<>` (not equal to). And you can combine multiple conditions using the keywords `And` and `Or`: Boolean logic.

We also looked at 'mod', aka modulo aka 'remainder after division by'. If you want your head to explode, check out [the Wikipedia entry](https://en.wikipedia.org/wiki/Modulo_operation). We used it for calculating odd and even, and tried to just get an intuition around it:

```
0 mod 2 = 0
1 mod 2 = 1
2 mod 2 = 0
3 mod 2 = 1
4 mod 2 = 0
...

51 mod 52 = 51
52 mod 52 = 0
53 mod 52 = 1
54 mod 52 = 2
...
```

### Functions

In VBA, our top-level `Sub` statement defines a function (aka sub-routine). Another function we used was `Split`:

```
Dim shakespeare as String
shakespeare = "To be or not to be. That is the question"
words = Split(shakespeare, " ")
```

At this point, the variable `words` will be an array - words(0) is "To", words(1) is "be", etc. The point is that the function `Split` takes some arguments (aka parameters) - in this case a string and a character to split on - and returns something - in this case an array.

### For Loops

Iterators, or loops, allow us to execute some block of code multiple times - for example, to loop down through all the rows of a sheet:

```
Dim i As Integer
For i = 1 to 10
    MsgBox(Cells(i, 1).Value)
Next i
```

And for each row, we could loop through all of its columns too, using a nested loop:

```
Dim i As Integer
For i = 1 to 10
    For j = 1 to 10
        MsgBox(Cells(i, j).Value)
    Next j
Next i
```

#### Tricks

We also had to figure out a few tricks in Saturday's class. Much of coding involves you sitting at a computer with no idea how to do something, or perhaps (and you have seen this with me) you know the Python or Javascript way but forgot the VBA way. So you Google it, and hopefully the top link is to [Stack Overflow](https://stackoverflow.com/). As I mentioned, this happens to most professional software engineers/data scientists about 20x every day. People have actually calculated that number.

So, a couple of tricks we needed to use:

Looping through worksheets: 
```
For Each ws in Worksheets
    worksheet_name = ws.Name
    [do something]
Next ws
```

(This seems a bit of a cheat - Worksheets is a default variable that Excel creates for us).

Inserting a column before cell A1:
```
ws.Range("A1").EntireColumn.Insert
```

Concatenating a string and copying an array to a range of cells:
```
Dim i As Integer
Dim an_array(10) As Long
i = 11
ws.Range("A2:A" & i) = an_array
```

Finding the final row, or column, with data in it:
```
LastRow = ws.Cells(Rows.Count, 1).End(xlUp).Row
LastColumn = ws.Cells(1, Columns.Count).End(xlToLeft).Column
```
