# Principy nízkoúrovňového programování


**Ukazatel a pole. Jak se deklarují? Jak se používají? Jaká je mezi nimi souvislost?**

Pokud vše správně chápu, tak je pole pointer. Můžeme nad ním provádět pointerovou aritmetiku (posouvat se po bytech podle sizeof()) nebo používat notaci [] (je to to samé).

**Co je to typecast**

https://en.wikipedia.org/wiki/Type_conversion

**Problémy s dynamickou alokací. Co je to Segmentation Fault? Co je to memory leak?**

- https://en.wikipedia.org/wiki/Memory_leak
- segfault


## GDB: The GNU Project Debugger

Mac alternative:
https://www.ics.uci.edu/~pattis/common/handouts/macmingweclipse/allexperimental/mac-gdb-install.html

Prerequisities:
- `gcc -g` generates debug information to be used by GDB debugger. 

1. „Load“ program with command line args
```
gdb --args executablename arg1 arg2 arg3
```
2. optionally set breakpoints.
```
break <source code line number>
```

3. `run`
4. Use `next`, `step`.

<br />

## Přednášky


### Týden 4


* Testování
* Vícerozměrné pole
* textové řetězce
* const
* argumenty main
* funkční ukazatel

### Testování
Unit testing - testování elementárních komponent
Integrační testy - test spolupráce několika komponent mezi sebou, dodržení definovaného rozhraní
Systémové testy - test celého programu v reálném prostředí

Při provádění refactoringu je porušení unit testů rychle odhaleno. 

### Vícerozměrné pole (multipole)

Pravoúhlé pole N x M
- Pro všechny řádky má stejný počet prvků
- int array[N][M];
- array[7][5] = 1; 
- Lze i vícerozměrné.

Nepravoúhlé pole
- Pomocí dynamické alokace
- Lze i pomocí statické alokace
- Pole ukazatelů
- int* pArray1D[4]; 
    - Do položek pArray1D přiřadíme pole
        - pArray1D[0] = array0;

### Textové řetězce
Řetězce v C jsou pole znaků ukončených binární nulou \0.

char sentence[10];  for (int i = 0; i < sizeof(sentence); i++) printf(“%c”, sentence[i]);  
Ukončení (zkrácen) věty: 	\0 binární nula - speciální znak jako konec 
* char myString[100]; // max. 99 znaků + koncová nula 
* char myString2[] = “Hello”; // délka pole dle konstanty, viz dále
* wchar_t myWideString[100]; // max. 99 unicode znaků + koncová nula

wchar_t - pro unicode znaky!!

Příklady:
- “” (pouze koncová 0)
- “Hello” (5 znaků a koncová nula) 
- char answers[]={'a','y','n'}; – NEVLOŽÍ koncovou nulu
- char answers2[]="ayn";  – VLOŽÍ koncovou nulu

Řetězcové konstanty nejde měnit.
* strlen(a) – délka řetězce bez koncové nuly
* strcpy(a,b) – kopíruje obsah b do a, vrací ukazatel na začátek a
* strcat(a,b) – připojí řetězec b za a
* strcmp(a,b) – porovná shodu a s b, vrací 0 pokud jsou shodné, >0 pokud je a větší než b a naopak
* strchr(a,c) – hledá výskyt znaku c v řetězci a
* strstr(a,b) – hledá výskyt řetězce b v řetězci a


Argumenty funkce main
* int main(int argc, char **argv, char **envp); 
