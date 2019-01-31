# Úvod do zpracování přirozené řeči

- [Quizlet](https://quizlet.com/_5tywhr)
- [Historie a aktuální stav](#historie-a-aktuální-stav)
- [Akustika (obecně)](#akustika-obecně)


# Historie a aktuální stav

## Co je to zvuk

* Jedná se o kmitavý pohyb molekul pružného prostředí (vzduch, voda, kov).
* Vyvolán odporem prostředí - vede k opakovanému stlačování prostředí.

## Co je to řeč

* Akustický signál a gesta sloužící ke komunikaci.
* Obsahuje definované vzory - slova, které jsou dána jazykem.

## Historie

* Schopnost artikulované řeči cca před 3 miliony let - australopitekus.
* Starověk - vudování mluvících soch.
* Galileo Galilei - souvislost mezi tónem a frekvencí.
* Systém rezonátorů pro samohlásky a, e, i, o, u.

# Akustika (obecně)

Akustika je věda zabývající se zvukem. Zkoumá zvuk z hlediska:

- fyzikálního - zvuk jako fyzikální vlnění
- fyziologického - tvorba a vnímání řeči u člověka
- hudebního - zvuky a jejich kombinace
- molekulárního - vztah molekulární struktury a akustických vlastností
- zpracování zvuku na počítači - digitální zpracování zvuku

Obsah kurzu:
- fyzikální akustika
- fyziologická akustika
- počítačové zpracování


# Fyzikální akustika

## Základní veličiny

Zvuk je fyzikální vlnění, kmitavý pohyb molekul, mechanické vlnění prostředí vyvolávající sluchový vjem.
Zvuk je charakterizován frekvencí a amplitudou.

### Zvuk

- **Perioda (T):** nejkratší kterou tělesu trvá průchod stejnou fází pohybu
- **Frekvence (f):** = 1/T
- **Jednotka:** Hz
  - 1 Hz = 1 perioda za sekundu
- **Rychlost zvuku:** závisí na prostředí a řadě fyzikáních faktorů (tlak, teplota...)
  - vzduch 340 m/s
  - voda 1500 m/s
  - ocel 5000 m/s
- **Amplituda:** maximální hodnota výchilky dané periodické veličiny (ymax)
- **Tlumené kmity:** vznikají působením vnější síly, která působí proti vlnění (například odpor vlnění.)
  - Způsobuje pozvolné zmenšování amplitudy kmitání.
- **Vlastní kmity/Vnější kmity:**
  - vlastní jsou bez působení vnějších sil
  - vnější jsou vynucené prostředím systému (buzením)
  
### Rezonance, akustická intenzita, akustický tlak

- **Rezonance:** Fyzikální jev - malá budící sílá může způsobit značné změny kmitajícího systému.
- **Akustická intenzita:** Množství energie, které projde jednotkovou plochou za jednotku času - jednotka Wm^-2.
  - P - tlak, S - plocha
  - I = P/S
- Akustický tlak

### Práh citlivosti

Slyšení 20μPa
Bolest 130 Pa
 
### Základní a složený tón

- Základní tón odpovídá sinusoidě
- Složený tón je lineární kombinace základních tónu - (většina reálných zvuků)

### Reálné zvuky

- Lze je rozložit na jednotlivé základní tóny. K jejich získání lze využít [Fourierovu transformaci](https://www.youtube.com/watch?v=spUNpyF58BY)

TODO:
[ ] - co jsou to fourierovy řady? 

## Základní hlasivkový tón

https://wikisofia.cz/wiki/Zvuk_a_zvukov%C3%A9_vln%C4%9Bn%C3%AD
http://www.fyzika007.cz/mechanicke-kmitani-a-vlneni/zakladni-vlastnosti-a-veliciny-charakterizujici-zvuk
https://cs.wikipedia.org/wiki/Frekvence
https://wikisofia.cz/wiki/Anal%C3%BDza_%C5%99e%C4%8Dov%C3%A9ho_sign%C3%A1lu
https://wikisofia.cz/wiki/Artikulace_konsonant%C5%AF


je složený tón s odpovídající harmonickou řadou. Od základního tónu jsou odvozeny všechny tónové složky řeči. 
Nadhrtanové dutiny poté slouží jako rezonátor, který propouští jen některé svrchní harmonické tóny, označované jako rezonanční frekvence nebo formanty. Je tomu tak u samohlásek, ale i u některých souhlásek (sonory). Hlasové ústrojí může ale sloužit i jako zdroj šumu. V tomto případě hlasivky nekmitají, vytvoří pouze štěrbinu, kterou proniká vzduch (neznělé obstruenty).[2]

### Harmonická řada

Harmonická řada je posloupnost částečných součtů posloupnosti převrácených hodnot přirozených čísel

Frekvence kmitání hlasivek = hlasivkový tón
Základní hlasivkový tón - frekvence kmitání hlasivek: F = 1/T

Vzorkovací frekvence: 44100 Hz
Frame: 160 samples or 10 ms
Co potřebuju vypočítat: frekvence kmitání hlasivek

https://dsp.stackexchange.com/questions/22085/how-compute-frequency-of-signal-from-zero-crossing

https://gist.github.com/endolith/129445

## Analýza ve frekvenční oblasti

### Fourierova transformace
Jakýkoliv průběh signálu se dá zapsat pomocí nekonečného množství sinusovek s různými parametry.

### Kepstrální analýza
X(k)=IFFT(FFT(x(k)))

* Kepstrální analýza umožňuje z řeči oddělit:
    * parametry buzení
    * parametry hlasového ústrojí
* Využití:
    * ocenění fonetické struktury řeči - znělost, perioda základního hlasivkového tónu, formanty, ...
    * rozpoznávání slov
    * verifikace a identifikace mluvčího

### Kepstrum
* metoda získání vyhlazeného spektra
* časová reprezentace
* většinou se vyjadřuje ve vzorcích
* T0 = ten nejvyšší vrcholek někde uprostřed = základní perioda (udává se v ms)
* levá část nějakým způsobem popisuje formanty, ale neví se, jak
* jediným jasným výsledkem je právě perioda
* původně navrženo pro získání F0 (až pak se zjistilo, že když F0 odfiltrujeme, získáme vyhlazené spektrum)
* vymýšlejí se stále nové metody na získávání F0 – stále neexistuje spolehlivá metoda
