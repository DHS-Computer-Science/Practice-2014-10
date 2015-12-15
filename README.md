# Practice 2014 - 10: The Magic Word

## Background
```
Do not meddle in the affairs of wizards, for they are subtle and quick to anger.
  -Gildor
```
Gandalf has to work with the arcane arts regularly, to aid in his fight against
Sauron. However, this can often be quite dangerous, as an arrangement of runes
can have unintended consequences. He has tasked you, one of his followers, to
design a system that could tell him in advance the magical outcome of a given
set of runes.

The input takes the form of a series of instructions, one per line, all part of
the same spell. As this is somewhat elvish magic, all of the instructions are in
elvish. Gandalf has provided you with the meanings of the instructions below, so
that you can better understand the magical patterns.

|       **Power Word**        | **Translation** |                    **Effect**                   |
| :-------------------------- | :-------------- | :---------------------------------------------- |
| arth [lbl]                  | region          | goto [lbl]                                      |
| pen [var1] [var2] [lbl]     | less            | if [var1] < [var2], goto [lbl]                  |
| muindor [var1] [var2] [lbl] | brother         | if [var1] == [var2], goto [lbl]                 |
| sad [lbl]                   | place           | label [lbl]                                     |
| tangado [var]               | to establish    | declare [var] as an int, set to 0               |
| ost [var1] [var2]           | stronghold      | declare [var1] as an int array of size [var2]   |
| teithant [string]           | to write        | print [string] to stdout, followed by a newline |
| canad [var]                 | to shout        | print [var] to stdout, followed by a newline    |
| anno [var1] [var2]          | give            | var1 := var2                                    |
| aderthad [var1] [var2]      | to reunite      | var1 := var1 + var2                             |
| adlanna [var1] [var2]       | to slant        | var1 := var1 / var2 (integer division)          |
| adlegi [var1] [var2]        | to release      | var1 := var1 - var2                             |
| athrado [var1] [var2]       | to cross        | var1 := var1 * var2                             |
| awarthad                    | to abandon      | exit                                            |

A few notes:
- [var] and [var n] may be of the following forms:
  1. An integer constant, e.g. 6; if attempting to assign to an integer
       constant, do nothing and go to the next command.
  2. A variable which has been declared with tangado, e.g. shadowfax; treat as
       an int would be in C or Java.
  3. An index in an array which has been declared with ost, e.g. moria[4]; the
       index of the array is itself a [var].
- [string] refers to a quote-delimited string constant, which cannot contain
    quotes and cannot contain newline characters.
- [lbl] refers to a label; labels may share names with [var]iables, but should
    be treated completely independently. labels are not pre-declared, so it may
    be advantageous to check the rest of the spell first to figure out label
    locations before interpreting it.
- The arth instruction means that the next command interpreted is the one
    immediately after the [lbl] indicated.
- The sad command has no effect on variables, but is used as a destination for
    arth commands. Note that arth commands may refer to sad commands
    further down in the spell.
- The ost command, for declaring arrays, initalizes all the cells to zero.
- The names of all variables and labels are strings consisting of only
    uppercase and lowercase letters.

For example, the following spell would print out
”Hello World” (without the quotes) and exit.
```
teithant "Hello World"
awarthad
```

The following spell would print out ”to Rohan!” (without the quotes) and exit.
```
tangado shadowfax
anno shadowfax 4
aderthad shadowfax 3
pen shadowfax 6 mordor
teithant "to Rohan!"
awarthad
sad mordor
teithant "to Mordor!"
awarthad
```

## Description

### Input
The input is a series of instructions, one per line. The instructions are
terminated by a single line with the string,“END”.

### Output
For each test case, print the output of the interpreted
instructions (i.e. the teithant and canad lines), with each command
putting its output on its own line.

## Sample
### Input
```
tangado x
anno x 3
aderthad x 2
canad x
adlanna x 2
canad x
adlegi x 1
canad x
athrado x 3
canad x
tangado i
ost sequence 10
anno sequence[0] 0
anno sequence[sequence[0]] 0
anno sequence[2] 1
anno sequence[3] 1
anno sequence[4] 1
anno sequence[5] 1
anno sequence[6] 0
anno sequence[7] 3
anno sequence[8] 4
anno sequence[9] 5
sad loop
muindor i 10 end
muindor sequence[i] 0 ttthti
muindor sequence[i] 1 gar
muindor sequence[i] 2 ggar
muindor sequence[i] 3 wdys
muindor sequence[i] 4 th
muindor sequence[i] 5 ti
muindor sequence[i] 6 tmwhg
muindor sequence[i] 7 abom
muindor sequence[i] 8 sfh
muindor sequence[i] 9 lnancb
sad ttthti
teithant "They're taking the hobbits to Isengard!"
arth pool
sad gar
teithant "Gard"
arth pool
sad ggar
teithant "Ga-gard"
arth pool
sad wdys
teithant "What did you say?"
arth pool
sad th
teithant "The hobbits"
arth pool
sad ti
teithant "To Isengard!"
arth pool
sad tmwhg
teithant "Tell me, where is Gandalf, for I much desire to speak with him."
arth pool
sad abom
teithant "A balrog of Morgoth"
arth pool
sad sfh
teithant "Stupid fat hobbit!"
arth pool
sad lnancb
teithant "Leave now, and never come back!"
arth pool
sad pool
aderthad i 1
arth loop
sad end
awarthad
END
```

### Output
```
5
2
1
3
They're taking the hobbits to Isengard!
They're taking the hobbits to Isengard!
Gard
Gard
Gard
Gard
They're taking the hobbits to Isengard!
What did you say?
The hobbits
To Isengard!
```
