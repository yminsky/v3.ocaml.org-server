---
title: "Null Pointers, Asserts and Warnings"
description: >
  Handling warnings and asserting invariants for your code
users:
  - intermediate
  - advanced
tags: [ "language" ]
date: 2021-05-27T21:07:30-00:00
---

## Null pointers
So you've got a survey on your website which asks your readers for their
names and ages. Only problem is that for some reason a few of your
readers don't want to give you their age - they stubbornly refuse to
fill that field in. What's a poor database administrator to do?

Assume that the age is represented by an `int`, there are two possible
ways to solve this problem. The most common one (and the most *wrong*
one) is to assume some sort of "special" value for the age which means
that the age information wasn't collected. So if, say, age = -1 then the
data wasn't collected, otherwise the data was collected (even if it's
not valid!). This method kind of works until you start, for example,
calculating the mean age of visitors to your website. Since you forgot
to take into account your special value, you conclude that the mean age
of visitors is 7½ years old, and you employ web designers to remove all
the long words and use primary colours everywhere.

The other, correct method is to store the age in a field which has type
"int or null". Here's a SQL table for storing ages:

```SQL
create table users
(
  userid serial,
  name text not null,
  age int             -- may be null
);
```

If the age data isn't collected, then it goes into the database as a
special SQL `NULL` value. SQL ignores this automatically when you ask it
to compute averages and so on.

Programming languages also support nulls, although they may be easier to
use in some than in others. In Java, any reference to
an object can be null, so it might make sense in Java to store the
age as an `Integer` and allow references to the age to be null. In C
pointers can, of course, be null, but if you wanted a simple integer to
be null, you'd have to first box it up into an object allocated by
`malloc` on the heap.

OCaml has an elegant solution to the problem of nulls, using a simple
polymorphic variant type defined (in `Stdlib`) as:

```ocaml
type 'a option = None | Some of 'a
```

A "null pointer" is written `None`. The type of age in our example above
(an `int` which can be null) is `int option` (remember: backwards like
`int list` and `int binary_tree`).

```ocaml
# Some 3;;
- : int option = Some 3
```

What about a list of optional ints?

```ocaml
# [None; Some 3; Some 6; None];;
- : int option list = [None; Some 3; Some 6; None]
```
And what about an optional list of ints?

```ocaml
# Some [1; 2; 3];;
- : int list option = Some [1; 2; 3]
```

## Assert, warnings, fatal errors, and printing to stderr
The built-in `assert` takes an expression as an argument and throws an
exception *if* the provided expression evaluates to `false`. 
Assuming that you don't catch this exception (it's probably
unwise to catch this exception, particularly for beginners), this
results in the program stopping and printing out the source file and
line number where the error occurred. An example:

```ocaml
# assert (Sys.os_type = "Win32");;
Exception: Assert_failure ("//toplevel//", 1, 1).
```

(Running this on Win32, of course, won't throw an error).

You can also just call `assert false` to stop your program if things
just aren't going well, but you're probably better to use ...

`failwith "error message"` throws a `Failure` exception, which again
assuming you don't try to catch it, will stop the program with the given
error message. `failwith` is often used during pattern matching, like
this real example:

<!-- $MDX skip -->
```ocaml
match Sys.os_type with
| "Unix" | "Cygwin" ->   (* code omitted *)
| "Win32" ->             (* code omitted *)
| "MacOS" ->             (* code omitted *)
| _ -> failwith "this system is not supported"
```

Note a couple of extra pattern matching features in this example too. A
so-called "range pattern" is used to match either `"Unix"` or
`"Cygwin"`, and the special `_` pattern which matches "anything else".

If you want to debug your program, then you'll probably want to print out a
warning some way through your function. Here's an example:

<!-- $MDX skip -->
```ocaml
open Graphics
  
let () =
  open_graph " 640x480";
  for i = 12 downto 1 do
    let radius = i * 20 in
    prerr_endline ("radius is " ^ string_of_int radius);
    set_color (if i mod 2 = 0 then red else yellow);
    fill_circle 320 240 radius
  done;
  ignore(read_line ())
```

If you prefer C-style `printf`'s then try using OCaml's `Printf` module
instead:

<!-- $MDX skip -->
```ocaml
open Graphics
  
let () =
  open_graph " 640x480";
  for i = 12 downto 1 do
    let radius = i * 20 in
    Printf.eprintf "radius is %d\n" radius;
    set_color (if i mod 2 = 0 then red else yellow);
    fill_circle 320 240 radius
  done;
  ignore(read_line ())
```
