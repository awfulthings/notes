# Základy databázových systémů

### DB
Schéma - logická struktura databáze (množina zákazníku, účtů)
Instance - aktuální obsah databáze

### Modely data
Sada nástrojů pro popis (dat, vztahů mezi daty, sémantiky dat, omezení dat)
Lofické modely založené na objektech (entitně-vztahový, objektové orientovaný, sémanticky, funkcionální)
Logické mode založené na záznamech (relařní, síťový, hierarchický)

DDL Jazyk pro definici dat (Data definition language;)
Značení pro sepcifikaci definicice schématu db.
Popis schématu relace, množiny atributů. doménu atributů, integritní omezení, množinu indexu udržovaných pro relici, bezpečnostní opatření

DML Jazyk manipulace s daty (Data manipulation language;)
Jazyk pro zpřístupnění a manipulaci s daty organizovanými příslušným datovým modelem.

1.Procedurální
	Uživatel specifikuje jaká data jsou vyžadována a jak je získat

2.Neprocedurální (deklarativní)
	Uživatel specifikuje jen jaká data jsou vyžadována


## Entitně-vztahový model

### Entita
Objekt odlišitelný od ostatních objektů
(osoba, společnost, ...)

### Množina entit
Atributy
Reprezentována množinou atributů (vlastností) všech člení množiny entit
(zákazník = (jméno, rodné_číslo, ulice, město))

#### Doména
Množina povolených hodnot pro každý atribut

Jednoduché (jméno) x Složené (datum)
Jednohodnotový (křestní jméno) x Vícehodnotový (telefonní čísla)
Nulové atributy
Odvozené atributy

Množiny vztahů
	Vztah = spojení mezi několika entitami
	Množina vztahů (matem. relace mezi >= 2 relacemi)
		1:1
		1:N
		N:1
		M:N

Slabá množina entit
Množina entit, která nemá primární klíč, tato množina závisí na existenci silné množiny entit -- musí být spojena vztrahem N:1
Má parciální klíč, tzv. diskriminátor -- odlišuje od sebe entity slabé množiny.
Primární klíč je primární klíč silné a parciální slabé.

## Generalizace & Specializace 

### Specializace

Podskupiny v množině (proces seshora dolů) - množiny entit nižší úrovně

### Generalizace (zobecnění)
Seskupení množin entit, které sdílejí stejné rysy do množiny entit vyšší úrovně (proces zezdola nahoru)

### Omezení

Daná podmínkou, definovaná uživatelem
Disjunktní x Překrývající se (entita může patřit do jedné / více entitních množin na jedné úrovni)
Úplná specializace x Částečná specializace (musí / nemusí patřit do jedné z entitních množin na nižší úrovni)



## Relační model

### Obecně
Relace je množina n-tic
Relace je podmnožina kartézského součinu domén jednotlivých atributů
Odpovídá jedné tabulce v databázi
Relační schéma R = (A1, ..., An), uspořádaná n-tice atributů, odpovídá záhlaví tabulky

### Relační algebra
procedurální jazyk
relace na vstupu, relace na výstupu

N-ticový relační kalkul
{t| P(t)} -- množina všech n-tic t takových, že predikát P je pravdivý pro t
Př.
{t| t € půjčka ^ t[částka] > 10000}

Lze vytvořit i nebezpečný výraz, který bude generovat nekonečné relace, omezíme množinu použitelných výrazů na bezpečné tzn. 
{t | P(t)}  bezpečný <=> každá komponenta t objeví v doméně P

### Pohled
Vytvoření virtuální relace pro uživatele, kterému není určeno, aby viděl vše. 


## Integritní omezení (integrity constraint)

Brání nechtěnému poškození databáze, když hlídá aby autorizované změny databáze nevedly k poškození konzistence.
(Unique, Not null, Primary Key, Foreign Key, Check(P) | P je predikát)

### Referenční integrita
Zajišťuje, že hodnota, která se objeví v jedné relaci pro danou množinu atributů, se také objeví v určitých množinách atributů v jiné relaci.
Formálně
r1(R1), r2(R2) jsou relace s primárními klíčí K1, K2
Podmnožina a z R2 je cizí klíč odkazující na primární klíč K1 v r1, jestliže pro každé t2 v r2 musí být n-tice v taková, že t1[K1] = t2[a]
π α (r 2)⊆ π K (r 1)
Podmínka říka, že v relaci s cizím klíčem musí být hodnoty cizího klíče podmnožinou hodnot primárního klíče v druhé relaci.

### Cizí klíč
Atribut u jedné relace ukazuje na primární klíč jiné relace (neformálně)
R,S jsou relace obsahující A. A je primární klíč pro S. A je cizím klíčem relace R => jakékoli hodnoty A, které se vyskytují v R se vyskytují i v S.
Integritní omezení cizí klíč pro nedovolené porušení "závislosti"


### Trigger (Spouštěč)
Příkáz vykonáváaný automaticky jako vedlejší efekt při modifikace databáze a splnění podmínky.
1) Nastavujeme podmínku spuštění
2) Specifikujeme akce, které se mají provést

PŘ. Po zapsání do relace, že student složil zkoušku vytvořen trigger, který automaticky přičte studentovi kredity.

PŘ2. V bance se řeší čerpání do minusu ne záporným zůstatkem, ale vytvořením půjčky.

Dříve využívány pro sumarizování dat (změna platu zaměstnance -- změna celkového rozpočtu firmy). Nyní již vhodnější způsoby, které poskytují databáze.

Lze jej vypnout před akcemi, které by jej nechtěně vyvolaly (backup, restore data apod.)



## Funkční závislosti

a -> b když jakékoli dvě n-tice t1 a t2 z r jsou stejné na atributech a ^ stejné na atributech b
t1[a] = t2[a] => t1[b] = t1[b]

### Kanonický tvar
Odstranění nadbytečných fčních závislostí
PŘ. a -> bc, b -> c, ab -> c => stačí jen a -> b, b -> c



## Návrh relačních databází

**Vyhnout se**
Opakování stejné informace
Nemožnost vyjádřit nějakou informaci

**Cíle**
vyhnout se inverse
+ usnadnit kontrolu porušení integritních omezení databáze


Pro snížení redundance používáme rozklad (dekompozici)

### Bezeztrátová dekompozice:
R = R1 ∪ R2 (relační schéma R rozloženo na R1, R2)
r =∏R1(r) |><| ∏R2(r) 

(pomocí fčních závislostí)
R1 průnik R2 -> R1
R1 průnik R2 -> R2


### Uchování závislosti
Fi - množina závislosti z F^+, která obsahuje pouze atributy ve schématu Ri
Musí platit 
Sjednocení Fi = F^+

#### Boyce-Coddova normální forma
Relační schéma R je v BCNG vzhledem k množině F, pokud pro všechny fční závislosti v F^+ tvaru a -> b, (a € R, b € R), je splněna alespoň jedna z:
a -> b je triviální (tj. b podmnožina a)
a je superklíc schématu R

#### 3 Normální forma
Relační schéma R je v 3NF, pokud pro všechny závislosti a -> b z F^+, je splněna alespoň jedna z: 
a -> b je triviální (b podmnožina a)
a je superklíc schématu

pro každý atribut A z R platí něco z: 
A je součástní nějakého kandidátního klíče
A není tranzitivně závislý na žádnem superklíči

### Cíle návrhu
BCNF (3NF když není možno), bezeztrátovost, zachování fčních závislostí



## Diskové a souborové struktury

* Rychlost přistupu
* Cena za jednotku paměti
* Spolehlivost
* Energ. závislost (Nestálá) / Nezávislost (Stálá)

### Hierarche

Cache
- nerychlejší, nejdražší, OS nebo HW

Hlavní paměť
- strojové instrukce pracují s daty z hlavní paměti
- rychlý přístup, ale zatím stále moc drahá na uložení celé databáze
- operační paměť
- nestálá (energet. závislá)

Flash paměť
- skoro stejně rychlé čtení jako hlavní paměť
- velmi pomalé pravé mazání
- přepisovací cykly omezení

Magnetické disky
- primární pro dlouhodobé ukládání
- data přesouváná z disku do hlavní paměti při zppracování
- přímý přístup - obvkle v libovolném pořáddí (náhodný přístup)
- přežijí pád OS, proudu
- chyba disku ne přiliš častá

Optické disky
- DVD, CD-ROM
- většinou pro archivaci
- (Magnetická) Pásková paměť
- stálé, archivace, záloha
- jen sekvenční přístup, velmi pomalé
- vysoká kapacita

1. primární (cache, hl. paměť)
2. sekundární (flash, disk)
3. terciální (megnetické pásky, optické disky)


## Magnetické Disky

Diskový řadič (rozhraní mezi počítačovým systémem a hardware)
Přijímá vyšší příkazy pro čtení/zápis
Spouští akce pro vystavení raménka, hlavy na správnou stopu a vlastní čtení a zápis

### Výkonosti disků

#### Přístupová doba
	Doba potřeboná ke čtení/zápisu (od vyslání požadavku na čtení/zápis po zahájení přenostu dat)
	1. Čas vystavení - doba potřebná pro vystavení raménka na požadovanou stopu.
	2. Rotační zpoždění - doba potřebná na otočení plotny, aby se požadovaný sektor dostal pod jeho hlavičku.

#### Rychlost přenosu dat
Střední doba poruchy (MTTF) - průměrná doba mezi dvěma výpadky disku


### Optimalizace

Blok
- Souvislá posloupnnost sektorů na jedné stopě
- Pomocí nich jsou přenášena data mezi diskem a hlavní pamětí
- Typicky 512 bytů po několik kB

Algoritmy pro minimální vystavování raménka (algoritmus )
Organizace souborů (odpovídající pořadí)
Stálé vyrovnávací paměti (Buffer)
- Urychlení zápisu na disk, díky vyrovnávací paměti, ta data drží do chvíle než disk není vytížen a zapíše až potom


#### Čtení bloku
1. Nastavení hlavy nad správnou stopu
2. Rotace sektoru pod hlavu
3. Čtení dat


## RAID (Redundant Arrays of Inexpensive/Independent Disks)

Nezávislá pole levných disků
Technika organizace disků, která spojuje více běžně dostupných disků do jednoho systému.
Původně levná alternativa k velkým - drahým diskům

### Redundance (nadbytečnost)
ukládání zvláštní informaci, kterou lze využít pro opětovné vytvoření informace ztracené při výpadku

### Zrcadlení (mirroring)
Duplikace každého disku. Jeden logický disk se skládá ze 2 fyzických, zápis probíhá na oba fyzické. Při výpadku jsou stále k dispozici data druhého.

### Paralelizace 
Vyvažování zátěže pro zvýšení propustnosti. 
Paralelizace požadavků na velké objemy pro snížení odezvy.

### Dělení (Striping)

### Na bitové úrovni
Každý byte se rozděluje na bity, které se ukládají na různé disky
(Pole 8 disků, každý bit jde na různý disk => čtení může proběhnout 8x rychleji, přístup trvá stejně - každý disk 1 přístup)

### Na blokové úrovni
Každý blok jde na disk (i mod n) + 1 (n počet disků, i pořadí bloku)
Při čtení 1 bloku je vytížen jen 1 disk

### Úrovně RAIDu
Schémata poskytující redundanci při nížkých nákladech pomocí dělení dat na disky spolu s paritními bity.

#### Úroveň 0
Dělení na úrovni bloků, žádná redundance
Vysoké rychlosti čtení/zápis, ztráta dat není kritická

#### Úroveň 1
Zrcadlené disky, rychlost jako u jednoho disku
Redundance zrcadlení, vyšší spolehlivita

#### Úroveň 2
Použití paritní informace pro zvyšení spolehlivosti, schopna opravit chybu v jednom bitu. Bit - jeden disk + paritní disky

#### Úroveň 3 (bitově prokládaná parita)
Bitové dělení. Při zápisu se paritní bit vypočítá a uloží na zvláštní disk. Používá jen jeden paritní disk. Jedno čtení využívá všechny disky.

#### Úroveň 4 (blokově prokládaná parita)
Blokové dělení. Jedno čtení nevyužívá všechny disky, vyšší propustnost požadavků. Paritní informace se ukládá na zvláštní disk -- slabé místo.

#### Úroveň 5
Využíváno pro velká množství dat s nepříliš častými aktualizacemi.
Parita není na disku zvlášť, ale na discích spolu s daty.

#### Úroveň 6
viz 5 + informace pro obnovu více než jednoho disku


## Souborové organizace

Db uložena v kolekci souborů (každý tvořen posloupností záznamů (tvořen z atributů))

Záznamy s pevnou délkou
	záznam i uložen na pouici l*(i-1) (l je délka záznamu)
	mazání
		vše za smazaným posunout
		poslední na uvolněné místo
		udržovat seznam prázných záznamů
			v hlavičce první smazaný a na smazaným ukazatel na další
Záznamy s proměnnou délkou
	vznik
		více druhů záznamů v jednom souboru 
		atributy proměnná délka
	řetězcová repr.
		na konci záznamu speciální znak
	dělený soubor
		hlavička: počet záznamů, pro každý záznam (ukazatel, délka z.)
	pěvná délka rezervovaného místa
		jen pokud znám maximální délku záznamu

Organizace záznamů v souboru 
Halda (záznam uložen na volné místo v souboru)
Sekvenční 
Hashování
Shlukování

Sekvenční soubor
	Záznamy obvykle uspořádány podle vyhledávacího klíče (atributu)
	Záznamy jsou sekvenčně propojeny.
	Při mazání - řetězení volného místa ukazateli
	Vkládání - najdeme místo pro nový záznam (pomocí klíče)
		pokud volné místo - ulož záznam
		vložit záznam do přetokové oblasti
		v obou případech aktualizovat seznam volnémo místa
	Občas reorganizace souboru

Shlukování
	Vložení více relací v jednom souboru
	Vhodné pro dotazy zahrnující spojení relací
	Proměnná délka záznamu


## Indexování & Hash

Indexové mechanismy používáme pro zrychlení přístupu
Vyhledávací klíc - atrubut (množina) pro vyhledávání záznamu v souboru

Indexový soubor
	záznamy ve tvaru [Vyhl. klíč | ukazatel]
	typicky mnohem menší než původní soubor

Řazené indexy (vyhledávací klíče uspořádané)
Hashovací indexy (index rovnoměrně rozprostřeny po adres. prostoru hashovací fce)

Porovnávání indexů
	typy efektivních ppřístupu
		přesná shoda ve vyhl. klíči
		rozsah vyhl. klíčů
	doba
		přístupová
		vložení záznamu
		smazání záznamu
	prostorová režie (místo pro index)

Řazené indexy
Vyhledávací záznamy uloženy uspořádané podle vyhledávacího klíče

Primární index
	seřazený sekvenční soubor
	index určije pořádní záznamů v souboru
	= shlukující soubor
Sekundární index
	vyhledávací klíč určuje jiné pořadí než v seřazeném sekvenčním souboru
	často dotazy hledající záznamy, které na určitém atributu (není součástí primárního indexu) nabývají nějaké hodnoty
	můžeme definovat sekundární index se záznamy pro každou hodnotu vyhl. klíče, bude určovat blok, který obsahuje ukazatele na záznamy mající danou hodnotu

Index-Sekvenční soubor
	seřazený sekvenční soubor s primárním indexem


Hustý indexový soubor
	indexový záznam uložen pro každou hodnotu vyhledávacího klíče (stejné hodnoty klíče se v indexu neopakují)

	Brno		Brno Žabovřesky
				Brno Jundrov
	Ostrava		Stodolní
	.
	.

Řídký indexový soubor
	indexové záznamy jen pro některé hodnoty vyhl. klíče
	pro nalezení záznamu s vyhledávacím klíčem K
		nalézt záznam s největším vyhled. klíčem menším než K (když nenajdeme přímo záznam)
		sekvenčeně hledat
	menší prostor než hustý, ale pomalejší

Vhodné řešení je řídký indexový soubor pro každý blok souboru


### Víceúrovňový index
Když se primární index nevejde do paměti - přístupy drahé
Považujeme primární index za sekvenční soubor na disku a vytvoří se pro něj řídký index
- Vnější index (nově vytvořený na primárním)
- Vnitřní index 
- Když se nevleze ani vnější - další úroveň
- Nutná aktualizace všech indexů při vkládání / mazání


### B+ stromy
Nejpoužívanější indexová organizace
Při růstu Index-sekvenční soubory častější reorganizace, B+ stromy jen malé lokální změny

Statické hashování
	Bucket (kyblík) základní úložná jednotka obsahující záznamy (obvykle tvořen jedním diskovým blokem)
	Bucket získáme v hashovací souborové organizaci přímo z hashovací fce

	Hashovací fce
	Fce převádějící vyhl. klíč na adresu bucketu
	Záznamy s různymi klíčemi mohou vést na stejný bucket - následné sekvenční prohledání
	Nejhorší mapuje všechny vehledávací klíče do jednoho bucketu
	Ideální hashovací fce
		náhodná - každý bucket stejný počet záznamů
		rovnoměrná - klíče jsou mapovány rovnoměrně

	Přetečení bucketu
	Řešení pomocí přetokových bucketů
		Řetězení přetoků (řetězení do seznamu)

	Hashovací indexy

Dynamické hashování
	Nedostatky statického
		při změně velikosti db (plýtvání místem, častá přetčení apod.)
	Rozšířitelné hashování
		Hash. fce generuje velká čísla, používá se vždy jen prefix 


Hashování obecně vhodnější při vyhledávání záznamů mající danou hodnotu klíče.
Řazené indexy lepší pro rozsahové dotazy

V SQL můžeme index vytvořit create index


External merge sort
1. Do paměti vždy nahrát co se vleze a seřadit běžným algoritmem (quick sort)
2. Potom vždy načtu z každé seřazené časti stejně velký začátek, nyní vyberu nejmenší ze seřazených, odložím na output buffer
3. Až je output buffer plný, tak zapíšu na finální místo
4. Už nemám co řadit -- nahraju další části
