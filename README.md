# design-essays
functional programming
ddd
cupid

# Tidy first
## Guard Clauses
```
if (condition)
 if (not other condition)
 ...some code...

 to:

if (not condition) return
if (other condition) return
...some code...
```

## Dead code
Just delete

## Normalize Symmetries
```
foo()
 return foo if foo not nil
 foo := ...
 return foo


foo()
 if foo is nil
 foo := ...
 return foo
```
Use just one form to similar situations

## New Interface, Old Implementation
So you need to call a routine, and the interface makes it difficult/complicated/
confusing/tedious. Implement the interface you wish you could call and call it. Imple‐
ment the new interface by simply calling the old one (you can inline the implementa‐
tion later, after migrating all other callers).

Creating a pass-through interface is the micro-scale essence of software design. You
want to make some behavior change. If the design were like thus and so, making that
change would be easy(-er). So make the design like that.

The same impulse holds true when you are:
• Coding backward—Start with the last line of a routine, as if you already had all
the intermediate results you needed.
• Coding test-first—Start with the test that needs to pass.
• Designing helpers—If only I had a routine/object/service that did XXX, then the
rest of this would be easy

## Reading Order
Let’s say you’re reading a file (we can have the debate about whether source code
belongs in files some other day). You read the whole file, and you get to the end and
there it is! The detail that would have helped you understand all the rest of the file.

Reorder the code in the file in the order in which a reader (remember, there are many
readers for each writer) would prefer to encounter it.

## Cohesion Order
You read the code, you figure out that to make a behavior change you’re going to have
to change several widely dispersed spots in the code, and you get grumpy. What
should you do?

Reorder the code so the elements you need to change are adjacent. Cohesion order
works for routines in a file: if two routines are coupled, put them next to each other.
It also works for files in directories: if two files are coupled, put them in the same
directory. It even works across repositories: put coupled code in the same repository
before changing it.

## Move Declaration and Initialization Together
```
Here’s what this tidying looks like. Imagine you have some code like this:
  fn()
   int a
   ...some code that doesn't use a
   a = ...
   int b
   ...some more code, maybe it uses a but doesn't use b
   b = ...a...
   ...some code that uses b

Tidy this by moving the initialization up to the declaration:
  fn()
   int a = ...
   ...some code that doesn't use a
   ...some more code, maybe it uses a but doesn't use b
   int b = ...a...
   ...some code that uses b
```

## Explaining Variables
```
You’ll see this frequently in graphics code:
return new Point(
 ...big long expression...,
 ...another big long expression...
)

Before changing one of those expressions, consider tidying first:
x := ...big long expression...
y := ...another big long expression...
return new Point(x, y)
```
## Explaining Constants

## Explicit Parameters

## Chunk Statements
This one wins the prize for simplest tidying. You’re reading a big chunk of code and
you realize, “Oh, this part does this and then that part does that.” 
Put a blank line between the parts.

## Extract Helper
```
routine()
 ...stuff that stays the same...
 ...stuff that needs to change...
 ...stuff that stays the same...
becomes:
helper()
 ...stuff that needs to change...
routine()
 ...stuff that stays the same...
 helper()
 ...stuff that stays the same...
```

## One Pile
Some symptoms you’re looking for are:
• Long, repeated argument lists
• Repeated code, especially repeated conditionals
• Poor naming of helper routines
• Shared mutable data structures

## Explaining Comments
## Delete Redundant Comments
