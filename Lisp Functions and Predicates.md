# Primitive lisp functions
[Dotted-Pair-Notation](https://www.gnu.org/software/emacs/manual/html_node/elisp/Dotted-Pair-Notation.html)
### CONS
The CONS function performs the operation of forming a dotted pair: the car of which is object-1 and the cdr of which is object-2.

Arguments:
* object-1---an object.
* object-2---an object.

```lisp
(CONS 'A 'B) = (A . B)
(CONS 'A '(B)) = (A B)
(CONS '(A B) '(C)) = ((A B) C)
(CONS '(A B) '(C D)) = ((A B) C D)
(CONS 'A '(B C)) = (A B C)
(CONS 'A (CONS 'B '(C))) = (A B C)
```
### CAR
CAR extracts the first element of a list or the left side of a dotted pair. Applied to an atom, the value is undefined (some systems return NIL).

```lisp
(CAR '(A B C)) = A
(CAR '(A . B)) = A
(CAR '((A B) C D)) = (A B)
(CAR (CONS '(B C) '(D E)) = (B C)
```
### CDR
CDR function is complementary to CAR and extracts the rest of the list or the right side of a dot pair, respectively

```lisp
(CDR '(A B C)) = (B C)
(CDR '(A . B)) = B
(CDR '((A B) C D)) = (C D)
(CDR (CONS '(B C) '(D E)) = (D E)
```

When repeatedly using the selection functions, the abbreviation Cx1x2 ... xnR can be used, equivalent to Cx1R o Cx2R o ... o CxnR, where the characters xi are either 'A' or 'D'. Depending on the implementations, it will be possible to use in this composition at most three or four CxiR:
```lisp
(CAADDR '((A B) C (D E))) = D

Why? Because:
(CDR '((A B) C (D E))) = (C (D E))
(CDDR '((A B) C (D E))) = ((D E))
(CADDR '((A B) C (D E))) = (D E)
(CAADDR '((A B) C (D E))) = D
```
### SET, SETQ, SETF
SETQ = SET Quoted <br>
SETF = SET Field

You can use SETF in place of set or setq but not vice versa since setf can also set the value of individual elements of a variable if the variable has individual elements. See the exaples below:

All four examples will assign the list (1, 2, 3) to the variable named foo:
```lisp
(set (quote foo) (list 1 2 3))    ;foo => (1 2 3)
(1 2 3)

(set 'foo '(1 2 3))   ;foo => (1 2 3) same function, simpler expression
(1 2 3)

(setq foo '(1 2 3))   ;foo => (1 2 3) similar function, different syntax
(1 2 3)

(setf foo '(1 2 3))   ;foo => (1 2 3) more capable function
(1 2 3)
```
setf has the added capability of setting a member of the list in foo to a new value.
```lisp
foo                   ;foo => (1 2 3) as defined above
(1 2 3)

(car foo)             ;the first item in foo is 1
1

(setf (car foo) 4)    ;set or setq will fail since (car foo) is not a symbol
4

foo                   ;the fist item in foo was set to 4 by setf
(4 2 3)
```

# List processing functions - system function set 
## LIST
It is indicated for constructing lists. It takes every parameter and creates a new list with them. list returns a list containing the supplied objects.
```lisp
(LIST ‘(a b) ‘c) = ((a b) c)
(LIST ‘a) = (CONS ‘a NIL) = (a)
(LIST ‘(a b) ‘(c d)) = ((a b) (c d))
(LIST ‘(a b c) ‘()) = ((a b c) NIL) = (LIST ‘(a b c) ())
```

## APPEND
Arguments and Values:
* **list**-----**each argument must be a proper list except the last, which may be any object.**
* **result**---an object. This will be a list unless the last list was not a list and all preceding lists were null.

Append returns a new list that is the concatenation of the copies. lists are left unchanged; the list structure of each of lists except the last is copied. The last argument is not copied; it becomes the cdr of the final dotted pair of the concatenation of the preceding lists, or is returned directly if there are no preceding non-empty lists.

```lisp
(APPEND ‘(A B) ‘(C D)) = (A B C D)
(APPEND ‘A) = A   ("result will be a list unless the last list was not a list and all preceding lists were null")
(APPEND ‘(A B) ‘C) = (A B . C)   ("it becomes the cdr")
(APPEND ‘(A B C) ‘()) = (A B C)
```

Due to the fact that the last argument of the APPEND function is not copied, it is worth noting what happens when the last argument of the function is destructively modified (for example with SETF):
```lisp
(SETQ X ‘(A)) -> X is evaluated at (A)
(SETQ Y ‘(B)) -> Y is evaluated at (B)
(SETF Z (APPEND X Y)) -> Z is evaluated at (A B)
(SETF (CAR X) ‘D) X is evaluated at (D)
(SETF (CAR Y) ‘E) Y is evaluated at (E) but Z is evaluated at (A E) because Y was not copied!!!!(it's the last argument)
```

## REVERSE
The REVERSE function returns the inverse of the list received as a parameter. The reversal takes place only at the superficial level:
```lisp
(REVERSE ‘(1 2 (3 4))) = ((3 4) 2 1)
(REVERSE ‘((A B) (C D) (E F))) = ((E F) (C D) (A B))
(REVERSE ‘((A B C))) = ((A B C))
(REVERSE ‘(A B C)) = (C B A)
(REVERSE ‘(A)) = (A)
```

## LENGTH
The LENGTH function returns the number of elements at superficial level:
```lisp
(LENGTH NIL) = 0
(LENGTH ‘(A B)) = 2
(LENGTH ‘(A ((B C) D) E)) = 3
(REVERSE NIL) = NIL
```

# Predicates
* **NIL**, with the meaning of false
* **T**, with the meaning of true

## ATOM
Returns T if the argument is an atom and NIL otherwise.
```lisp
(ATOM ‘A) = T;
(ATOM A) = depends on what A is evaluated for;
(ATOM ‘(A B C)) = NIL;
(ATOM NIL) = T;
```

## LISTP
Returns T if the argument is a list and NIL otherwise.
```lisp
(LISTP ‘A) = NIL;
(LISTP A) = T if A is evaluated on a list;
(LISTP ‘(A B C)) = T;
(LISTP NIL) = T;
```
