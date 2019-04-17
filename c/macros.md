# Macros

C preprocesor přeloží makra před kompilací programu.
C kód → Preprocessor → Compiler →

Dobré vědět:
- nemohou obsahovat cyklus (říkali na cviku, zdůvodu kompilace)

## Definice

```c
#define MAKRO(A) puts(A)

int main()
{
  MAKRO("AHOJ");
}
```

## Podmíněné makra
```c
#ifdef MACRO     
     conditional codes
#endif
```

```c
#if expression
   conditional codes
#endif
```

```c
#if expression
   conditional codes if expression is non-zero
#elif expression1
    conditional codes if expression is non-zero
#elif expression2
    conditional codes if expression is non-zero
... .. ...
else
   conditional if all expressions are 0
#endif
```

## Predefined macro	Values

__DATE__	String containing the current date
__FILE__	String containing the file name
__LINE__	Integer representing the current line number
__STDC__	If follows ANSI standard C, then value is a nonzero integer
__TIME__	String containing the current date.

## Zdroje

1. https://www.programiz.com/c-programming/c-preprocessor-macros#introduction
