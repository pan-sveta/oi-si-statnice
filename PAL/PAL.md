# PAL

## Topics
Polynomial algorithms for standard graph problems. Combinatorial and number-theoretical
algorithms, isomorphism, prime numbers. Search trees and their use. Text search based
on finite automata.

## Questions

- Notation of asymptotic complexity of algorithms. Basic notation of graph problems - degree, path, circuit, cycle. Graph representations by adjacency, distance, Laplacian and incidence matrices. Adjacency list representation.
- Algorithms for minimum spanning tree (Prim-Jarník, Kruskal, Borůvka), strongly connected components (Kosaraju-Sharir, Tarjan), Euler trail. Union-find problem. Graph isomorphism, tree isomorphism.
- Silně propojená komponenta (SCC) orientovaného grafu je podgraf, kde existuje cesta z každého vrcholu do každého jiného vrcholu v podgrafu.
- Generation and enumeration of combinatorial objects - subsets, k-element subsets, permutations. Gray codes. Prime numbers, sieve of Eratosthenes. Pseudorandom numbers properties. Linear congruential generator.
- Finite automata, regular expressions, operations over regular languages. Bit representation of nondeterministic finite automata. Text search algorithms - exact pattern matching, approximate pattern matching (Hamming and Levenshtein distance), dictionary automata.

# Asymptotická složitost algoritmů

- Asymptotická složitost algoritmu popisuje, jak se doba běhu nebo prostorová náročnost algoritmu mění s velikostí vstupních dat. Využívá se pro porovnání efektivnosti algoritmů.

## O Notace (Big O)

- Popisuje **horní hranici** složitosti algoritmu.
- Například: `O(n)` znamená, že složitost algoritmu roste lineárně s velikostí vstupu.

## Ω Notace (Big Omega)

- Popisuje **dolní hranici** složitosti algoritmu.
- Například: `Ω(n)` znamená, že složitost algoritmu roste alespoň lineárně s velikostí vstupu.

## Θ Notace (Big Theta)

- Popisuje **přesnou hranici** složitosti algoritmu.
- Například: `Θ(n)` znamená, že složitost algoritmu roste přesně lineárně s velikostí vstupu.

## o Notace (Little O)

- Popisuje **horní hranici**, kterou algoritmus nikdy nepřekročí.
- Například: `o(n)` znamená, že složitost algoritmu roste méně než lineárně s velikostí vstupu.

## ω Notace (Little Omega)

- Popisuje **dolní hranici**, kterou algoritmus vždy překročí.
- Například: `ω(n)` znamená, že složitost algoritmu roste více než lineárně s velikostí vstupu.

# Základní notace problémů s grafy

- **Vrchol (Vertex)**: Základní jednotka grafu, také známý jako uzel.

- **Hrana (Edge)**: Spojení mezi dvěma vrcholy v grafu.

- **Stupeň vrcholu (Degree)**: Počet hran spojených s daným vrcholem. Pro orientované grafy rozlišujeme stupeň dovnitř (in-degree) a stupeň ven (out-degree).

- **Cesta (Path)**: Sekvence vrcholů, kde je každý vrchol spojen s dalším hranou. Cesta je jednoduchá, pokud žádný vrchol nebo hrana není v sekvenci vícekrát.

- **Cyklus (Cycle)**: Jednoduchá cesta, která začíná a končí ve stejném vrcholu.

- **Obvod (Circuit)**: Cesta, která začíná a končí ve stejném vrcholu. Na rozdíl od cyklu může obsahovat opakující se vrcholy a hrany.

- **Souslednost (Adjacency)**: Dva vrcholy jsou sousední, pokud jsou spojeni hranou.

- **Incidence**: Hrana je incidní s vrcholem, pokud vrchol leží na hraně.

- **Podgraf (Subgraph)**: Graf tvořený vrcholy a hranami původního grafu.

- **Kompletní graf (Complete graph)**: Graf, ve kterém je každý vrchol spojen s každým jiným vrcholem.

- **Spojitý graf (Connected graph)**: Graf, ve kterém existuje cesta mezi každým párem vrcholů.

# Reprezentace grafů

## Matice sousednosti (Adjacency Matrix)

- Kvadratická matice, kde hodnota v i-tém řádku a j-tém sloupci je 1, pokud je mezi vrcholy i a j hrana, a 0, pokud ne.
- Pro neorientovaný graf je matice symetrická.
- Časová složitost pro zjištění sousednosti: O(1).

## Matice vzdáleností (Distance Matrix)

- Kvadratická matice, kde hodnota v i-tém řádku a j-tém sloupci je délka nejkratší cesty mezi vrcholy i a j.
- Tato matice je vždy symetrická.

## Laplaceova matice (Laplacian Matrix)

- Kvadratická matice definovaná jako D - A, kde D je diagonální matice stupňů vrcholů a A je matice sousednosti.
- Laplaceova matice má několik důležitých vlastností v teorii grafů, včetně vazby na počet stromů krytí grafu.

## Matice incidence

- Matice s počtem řádků rovným počtu vrcholů a počtem sloupců rovným počtu hran.
- Hodnota v i-tém řádku a j-tém sloupci je 1, pokud hrana j je incidní s vrcholem i, a 0, pokud ne.
- Pro neorientovaný graf jsou hodnoty pouze 1 a 0. Pro orientovaný graf používáme -1 pro označení směru hrany.

## Seznam sousednosti (Adjacency List)

- Pro každý vrchol udržuje seznam všech vrcholů, se kterými je spojen.
- Efektivní pro řešení mnoha problémů v grafech, zejména pro řídké grafy, kde je počet hran mnohem menší než počet vrcholů na druhou.
- Časová složitost pro zjištění sousednosti: O(stupeň vrcholu).

# Algoritmy pro minimální kostru grafu

Minimální kostra grafu je podgraf, který spojuje všechny vrcholy, je strom a minimizuje celkovou váhu hran.

## Algoritmus Prim-Jarník

- Začněte s libovolným vrcholem a postupně přidávejte nejkratší hranu spojující strom s vrcholem mimo strom.
- Postup:
  1. Inicializace: Začněte s prázdným stromem a přidejte libovolný vrchol do stromu.
  2. Hledejte nejkratší hranu spojující vrchol ve stromu s vrcholem mimo strom a přidejte ji do stromu.
  3. Opakujte krok 2, dokud nebudou všechny vrcholy součástí stromu.
- Složitost času: O(E log V) pro binární haldy, kde E je počet hran a V je počet vrcholů.

## Kruskalův algoritmus

- Začněte s prázdným stromem a postupně přidávejte nejkratší hranu, která nevytváří cyklus.
- Postup:
  1. Inicializace: Začněte s prázdným stromem.
  2. Seřaďte všechny hrany podle jejich váhy od nejmenší po největší.
  3. Přidejte do stromu nejkratší hranu, která nevytváří cyklus.
  4. Opakujte krok 3, dokud nebudou všechny vrcholy spojeny.
- Složitost času: O(E log E) nebo O(E log V) pro hranový seznam nebo matice sousednosti.

## Borůvkův algoritmus

- Začněte s lesem, kde každý vrchol je samostatný strom, a postupně přidávejte nejkratší hranu spojující dva stromy.
- Postup:
  1. Inicializace: Začněte s lesem, kde každý vrchol je samostatný strom.
  2. Pro každý strom v lese najděte nejkratší hranu spojující strom s vrcholem mimo strom a přidejte ji do stromu.
  3. Opakujte krok 2, dokud nebude existovat pouze jeden strom (tj. všechny vrcholy jsou spojeny).
- Složitost času: O(E log V) pro binární haldy.

# Silně propojené komponenty

## Kosaraju-Sharirův algoritmus

- Tento algoritmus provádí dva průchody grafem pomocí DFS (depth-first search).
- Postup:
  1. Proveďte DFS na originálním grafu a sledujte pořadí dokončení vrcholů.
  2. Transponujte graf (otočte směr všech hran).
  3. Proveďte DFS na transponovaném grafu, ale začněte s vrcholem, který byl dokončen jako poslední v prvním průchodu.
  4. Každý strom DFS vytvořený v druhém průchodu je silně propojená komponenta.
- Časová složitost: O(V + E), kde V je počet vrcholů a E je počet hran.

## Tarjanův algoritmus

- Tento algoritmus provede jeden průchod grafem pomocí DFS a identifikuje SCC pomocí nízkých spojů a zásobníku.
- Postup:
  1. Proveďte DFS na grafu a sledujte pořadí návštěvy vrcholů a nejnižší vrchol dosažitelný z každého vrcholu.
  2. Během DFS, pokud vrchol je kořenem silně propojené komponenty, pak všechny vrcholy na zásobníku nad a včetně tohoto vrcholu tvoří SCC a jsou odstraněny ze zásobníku.
  3. Každá silně propojená komponenta je identifikována, když je její kořen navštíven.
- Časová složitost: O(V + E).

# Eulerova stezka

- **Eulerova stezka** je cesta v grafu, která prochází každou hranu přesně jednou.
- **Eulerův cyklus** je Eulerova stezka, která začíná a končí ve stejném vrcholu.
- Graf má Eulerovu stezku, pokud má nanejvýš dva vrcholy s lichým stupněm. Pokud má graf nula vrcholů s lichým stupněm, má Eulerův cyklus.
- Eulerova stezka se využívá například v problému sedmi královských mostů v Königsbergu, v němž se snažíme najít cestu, která prochází přesně jednou všemi sedmi mosty.

# Union-Find

- **Union-Find** je datová struktura, která řeší problém diskrétních množin.
- Má dvě hlavní operace:
  1. **Find**: Zjistí, do jaké množiny patří daný prvek.
  2. **Union**: Spojí dvě množiny do jedné.
- Využívá se zejména v algoritmech pracujících s grafy (např. Kruskalův algoritmus).

## Naivní implementace

- V nejjednodušší implementaci, každá množina je reprezentována pomocí svého "vedoucího" prvku.
- Operace **Find** prochází celou strukturu, dokud nenajde vedoucího prvku množiny.
- Operace **Union** přiřadí vedoucího prvku jedné množiny vedoucímu prvku druhé množiny.
- Časová složitost: O(n) pro obě operace, kde n je počet prvků.

## Algoritmus pro nalezení Eulerovy stezky

- Existuje několik algoritmů pro nalezení Eulerovy stezky. Nejjednodušší je Fleuryho algoritmus, ale je neefektivní. Hierholzerův algoritmus je efektivnější.

### Fleuryho algoritmus

- Začněte na libovolném vrcholu s lichým stupněm (nebo na libovolném vrcholu, pokud jsou všechny vrcholy sudého stupně).
- Postupně sledujte hrany, přičemž se snažíte vyhnout mostům, pokud je to možné.
- Časová složitost: O(E^2), kde E je počet hran.

# Isomorfismus grafů

- Dva grafy jsou **izomorfní**, pokud existuje bijekce mezi vrcholy grafů tak, že spojení vrcholů je zachováno. To znamená, že grafy jsou "stejné", pouze jsou jinak popsané nebo nakreslené.
- Problém isomorfismu grafů je rozhodnout, zda jsou dva grafy izomorfní. Tento problém je jedním z mála problémů, jejichž složitost zůstává otevřenou otázkou - nevíme, zda patří do třídy P, NP, nebo je NP-úplný.

# Isomorfismus stromů

- Problém isomorfismu stromů je podproblémem isomorfismu grafů, ale je snazší. Existuje lineární algoritmus pro rozhodnutí, zda jsou dva stromy izomorfní.

## Algoritmus certifikátů

- Algoritmus certifikátů je metoda pro nalezení isomorfismu grafů.
- Každému grafu přiřadí unikátní "certifikát", který je stejný pro všechny isomorfní grafy.
- Pokud mají dva grafy stejný certifikát, jsou izomorfní.

# Složitost

- Problém isomorfismu grafů je jedním z mála problémů, jejichž třída složitosti je stále nejasná. Je známo, že je v NP, ale není známo, zda je v P nebo je NP-úplný.
- Problém isomorfismu stromů je v P, protože existuje lineární algoritmus pro jeho řešení.

# Generování a enumerace kombinatorických objektů

## Podmnožiny

- **Podmnožina** je sada, která obsahuje prvky jiné sady, ale žádné další prvky.
- Každá množina má 2^n podmnožin, kde n je počet prvků v množině.

## k-prvkové podmnožiny

- **k-prvková podmnožina** je podmnožina s k prvky.
- Počet k-prvkových podmnožin je daný kombinačním číslem C(n, k), kde n je počet prvků v množině.

## Permutace

- **Permutace** je uspořádaná sekvence prvků, ve které se každý prvek objevuje jednou.
- Počet permutací n prvků je n!.

## Kombinace

- **Kombinace** je výběr prvků, kde nezáleží na pořadí.
- Počet kombinací k prvků z n je C(n, k) = n! / [k!(n-k)!].

## Pořadí

- **Pořadí** je uspořádaná sekvence prvků, kde se mohou objevit opakování.
- Počet uspořádaní k prvků z n je P(n, k) = n! / (n-k)!.

# Grayovy kódy

- **Grayovy kódy** jsou posloupnost binárních čísel, kde se dvě po sobě jdoucí čísla liší pouze v jednom bitu.
- Při přechodu od jednoho čísla k dalšímu se mění vždy jen jeden bit.
- Často se používají v digitálních systémech, kde je důležité minimalizovat šanci na chybu při změně stavu.

## Generování Grayových kódů

- Grayovy kódy lze generovat rekurzivně.
- Pro n-bitový Grayův kód:
  - Začněte s listem, který obsahuje jednobitový Grayův kód [0, 1].
  - Pro každé další i (až do n):
    - Kopírujte list, přidejte '0' na začátek každého čísla v původním listu a přidejte je do nového listu.
    - Kopírujte list, přidejte '1' na začátek každého čísla v původním listu, převraťte pořadí a přidejte je do nového listu.
- Toto dá n-bitový Grayův kód.

# Prvočísla

- **Prvočíslo** je přirozené číslo větší než 1, které má pouze dva kladné dělitele: 1 a samo sebe.
- Prvních pět prvočísel: 2, 3, 5, 7, 11.
- 2 je jediné sudé prvočíslo.

## Síto Eratosthena

- Algoritmus pro nalezení všech prvočísel menších než dané číslo n.
- Postup:
  - Začněte se seznamem všech čísel od 2 do n.
  - Označte 2 jako prvočíslo a označte všechny jeho násobky jako složená čísla.
  - Přejděte k dalšímu neoznačenému číslu a označte ho jako prvočíslo.
  - Označte všechny násobky tohoto nového prvočísla jako složená čísla.
  - Opakujte poslední dva kroky, dokud nezůstanou žádná neoznačená čísla.
- Tento algoritmus je účinný a rychlý pro nalezení všech prvočísel menších než n.

## Naivní algoritmus pro generování prvočísel

- Pro každé číslo n od 2 výše:
  - Zkontrolujte, zda n má nějaké dělitele kromě 1 a n.
  - Pokud ne, je to prvočíslo.
- Tento algoritmus je jednoduchý, ale neefektivní pro velké čísla.

## Zlepšený naivní algoritmus

- Pro každé číslo n od 2 výše:
  - Zkontrolujte, zda n má nějaké dělitele kromě 1 a n, ale jen pro čísla menší než √n.
  - Pokud ne, je to prvočíslo.
- Tento algoritmus je stále poměrně pomalý pro velké čísla, ale je rychlejší než úplně naivní algoritmus.

# Pseudonáhodná čísla

- **Pseudonáhodná čísla** jsou čísla, která se zdají být náhodná, ale jsou generována deterministickým algoritmem.
- Kvalitní pseudonáhodný generátor by měl mít následující vlastnosti:
  - **Uniformita**: Každé číslo v požadovaném rozsahu má stejnou šanci na vygenerování.
  - **Nezávislost**: Generovaná čísla nejsou vzájemně závislá.
  - **Reprodukce**: Za stejných počátečních podmínek (seed) generuje stejnou sekvenci čísel.
  - **Periodicita**: Délka sekvence, než se opakuje, by měla být co možná největší.

## Lineární kongruentní generátor (LCG)

- **Lineární kongruentní generátor** je typ pseudonáhodného generátoru čísel.
- Vytváří sekvenci čísel podle vzorce: X_{n+1} = (a * X_n + c) mod m
- Kde:
  - X_{n+1} je další číslo v sekvenci,
  - X_n je předchozí číslo v sekvenci,
  - a, c, a m jsou konstanty.
- Konstanty a, c, a m by měly být pečlivě vybrány, aby byla zajištěna dobrá kvalita generovaných čísel a maximální perioda.

### Hull-Dobell Theorem

- **Hull-Dobell Theorem** stanovuje podmínky, za kterých má LCG plnou periodu pro každé počáteční číslo (seed).
- Podmínky jsou:
  1. Číslo c a m jsou relativně prvočíselné (tzn. jediné číslo, které dělí jak c tak m, je 1).
  2. Pokud q je jakýkoli prvočíselný faktor m, pak a-1 je dělitelné q.
  3. Pokud 4 je dělitel m, pak a-1 je dělitelné 4.
- Pokud jsou splněny všechny tyto podmínky, pak LCG generuje sekvenci s plnou periodou.

Search trees - data structures, operations, and their complexities. Binary tree, AVL tree, red-black tree (RB-tree), B-tree and B+ tree, splay tree, k-d tree. Nearest neighbor searching in k-d trees. Skip list.

# Binární strom (Binary tree)

- Binární strom je datová struktura, kde každý uzel má maximálně dva potomky, označované jako levý potomek a pravý potomek.
- Každý uzel obsahuje klíč (nebo data), levý odkaz na potomka, pravý odkaz na potomka.
- Neexistuje žádné zvláštní řazení mezi klíči. Může být úplný, úplný, rostoucí, klesající atd.
- **Operace**:
    - Vložení: O(n)
    - Hledání: O(n)
    - Mazání: O(n)
- **Nejlepší využití**: Binární stromy jsou vhodné pro případy, kdy je důležité zachovat přirozené uspořádání dat (např. pro vytváření výrazových stromů v počítačových algoritmech).

# AVL strom

- AVL strom je vyvážený binární vyhledávací strom, kde rozdíl výšky levého a pravého podstromu je maximálně 1. 
- Po každé operaci vložení nebo mazání se provádí vyvažování stromu.
- **Operace**:
    - Vložení: O(log n)
    - Hledání: O(log n)
    - Mazání: O(log n)
- **Nejlepší využití**: AVL stromy jsou nejlepší pro databázové stroje, které často načítají a nikdy neukládají.

# Červeno-černý strom (Red-Black tree)

- Červeno-černý strom je druh vyváženého binárního vyhledávacího stromu, kde každý uzel má přidělenou barvu (červenou nebo černou).
- Splňuje následující vlastnosti: kořen je černý, všechny listy jsou černé, pokud je uzel červený, pak oba jeho potomci jsou černí, každá cesta z každého listu k jinému listu obsahuje stejný počet černých uzlů.
- **Operace**:
    - Vložení: O(log n)
    - Hledání: O(log n)
    - Mazání: O(log n)
- **Nejlepší využití**: Červeno-černé stromy jsou vhodné pro všeobecné použití v mnoha programovacích jazycích, například v implementacích asociativních polí.

# B-strom

- B-strom je samo vyvažující se strom vhodný pro systémy s velkým množstvím dat, které se nedají uchovat v paměti, ale musí být uchovávány na disku.
- Každý uzel v B-stromu může mít více než 2 potomky. Uzel B-stromu s 'm' potomky má 'm-1' klíčů.
- B-stromy mají pravidlo, že všechny listy musí být na stejné úrovni. To znamená, že B-stromy rostou směrem nahoru.
- B-stromy mají také pravidlo, že všechny uzly (kromě kořene) musí být alespoň z poloviny plné.
- **Operace**:
    - Vložení: O(log n)
    - Hledání: O(log n)
    - Mazání: O(log n)
- **Nejlepší využití**: B-stromy jsou široce používány v databázových systémech a souborových systémech.

# B+ strom

- B+ strom je vylepšení B-stromu, kde data jsou ukládána pouze v listových uzlech, což umožňuje rychlejší průchod a efektivnější ukládání na disk.
- Interní uzly v B+ stromu ukládají klíče pro navigaci a ukazatele na potomky, ale ne ukládají data. To umožňuje, aby interní uzly měly více klíčů a tedy nižší výšku stromu.
- Všechny listy v B+ stromu jsou navzájem propojeny, což umožňuje rychlé sekvenční přístupy.
- Stejně jako B-strom, B+ strom se vyvažuje při vkládání a mazání.
- **Operace**:
    - Vložení: O(log n)
    - Hledání: O(log n)
    - Mazání: O(log n)
- **Nejlepší využití**: B+ stromy jsou široce používány v databázových systémech a souborových systémech, kde je důležitá rychlá sekvenční iterace.

# Splay strom

- Splay strom je samo vyvažující se binární vyhledávací strom.
- Klíčová operace je "splay", kdy se při každé operaci přístupu (vložení, hledání, mazání) přesune přístupovaný uzel na kořen stromu.
- Splay stromy nemají pevnou strukturu jako AVL nebo červeno-černé stromy, a jejich tvar se mění s každou operací.
- **Operace**:
    - Vložení: O(log n) v průměru, ale O(n) v nejhorším případě.
    - Hledání: O(log n) v průměru, ale O(n) v nejhorším případě.
    - Mazání: O(log n) v průměru, ale O(n) v nejhorším případě.
- **Nejlepší využití**: Splay stromy jsou dobré pro případy, kdy se některé prvky vyhledávají častěji než ostatní.

# k-d strom

- k-d strom (k-dimenzionální strom) je binární vyhledávací strom, kde data v uzlech jsou k-dimenzionální body.
- k-d stromy jsou užitečné pro řadu vyhledávacích úloh, které zahrnují více dimenzí, například rozsahové hledání.
- **Operace**:
    - Vložení: O(log n) v průměru, ale O(n) v nejhorším případě.
    - Hledání: O(log n) v průměru, ale O(n) v nejhorším případě.
    - Mazání: O(log n) v průměru, ale O(n) v nejhorším případě.
- **Nejlepší využití**: k-d stromy jsou vhodné pro úlohy, které zahrnují vyhledávání na základě více klíčů (například geografické vyhledávání).

## Nearest Neighbor Searching v k-d stromech

Nejbližší soused hledání (Nearest Neighbor Searching, NNS) je algoritmus používaný v k-d stromech k nalezení bodu, který je nejbližší k danému dotazu. Je to důležitá operace pro řadu aplikací v oblasti počítačového vidění, strojového učení a datové analýzy.

### Algoritmus
1. Začněte na kořeni a procházejte stromem tak, jak byste to udělali při vyhledávání dotazovaného bodu, až narazíte na list.
2. Nastavte tento list jako "aktuální nejbližší bod".
3. Vraťte se zpět na rodičovský uzel.
4. Zkontrolujte, zda by rodičovský uzel mohl obsahovat bod bližší k dotazovanému bodu než aktuální nejbližší bod. Pokud ano, zkontrolujte, zda je to tak, a případně aktualizujte "aktuální nejbližší bod".
5. Zkontrolujte, zda by jiná větev, než kterou jsme prošli, mohla obsahovat bod bližší k dotazovanému bodu. Pokud ano, projeďte touto větví (začněte od kroku 1) a případně aktualizujte "aktuální nejbližší bod".
6. Pokračujte, dokud nezkontrolujete celý strom.

### Složitost

- Pokud je strom vyvážený a data jsou rovnoměrně rozložená, složitost hledání nejbližšího souseda je O(log n).
- V nejhorším případě, kdy strom není vyvážený nebo data jsou seskupená, může být složitost hledání O(n).

# Porovnání

|   Typ stromu    | Složitost vyhledání | Složitost vložení | Složitost mazání |            Výhody             |                                        Nevýhody                                        |
| :-------------: | :-----------------: | :--------------: | :--------------: | :---------------------------: | :-----------------------------------------------------------------------------------: |
|  Binární strom  |        O(n)         |       O(n)       |       O(n)       | Přirozené uspořádání dat      | Nevyvážené stromy mohou mít vysoké výšky, což vede k neefektivním operacím              |
|    AVL strom    |      O(log n)       |     O(log n)     |     O(log n)     | Dobře vyvážený                | Operace vložení a mazání mohou být pomalé kvůli potřebě vyvažování                     |
| Červeno-černý strom |      O(log n)       |     O(log n)     |     O(log n)     | Dobře vyvážený                | Operace vložení a mazání mohou být pomalé kvůli potřebě udržování vlastností stromu     |
|     B-strom     |      O(log n)       |     O(log n)     |     O(log n)     | Dobré pro velké soubory dat   | Složitější implementace, může být pomalý pro operace v paměti                            |
|    B+ strom     |      O(log n)       |     O(log n)     |     O(log n)     | Rychlé sekvenční přístupy     | Interní uzly neukládají data, což může být neefektivní pro některé typy dotazů          |
|   Splay strom   |   O(log n) průměrně | O(log n) průměrně | O(log n) průměrně | Často přistupované prvky jsou rychle dostupné | Nevyvážený, může vést k O(n) operacím v nejhorším případě                                |
|     k-d strom   |   O(log n) průměrně | O(log n) průměrně | O(log n) průměrně | Dobré pro hledání v mnoha dimenzích | Neefektivní pro vysoké dimenze, operace vkládání a mazání mohou být pomalé v některých případech |

# Skip-list

- Datová struktura umožňující rychlé vyhledávání, vložení a mazání v seřazeném seznamu.
- Jednoduchý na implementaci.
- Průměrná složitost operací srovnatelná s vyváženými stromy (například AVL, Červeno-černý).

## Struktura

- "Víceúrovňový" seřazený spojový seznam.
- Každý prvek má několik ukazatelů na další prvky, umožňující "přeskočit" přes několik prvků.
- Úrovně přeskakování se určují náhodným generátorem
  - Hodím kostkou která dá ANO s pravděpodobností p
  - Když padne ANO vytvořím pro vložený prvek další level a opakuji hod
  - Když NE vložím prvek s počtem "naházených" linků a předělám reference skoků

## Fungování

- Vyhledávání: Začněte na vrcholu a postupujte doprava, dokud následující prvek není větší než hledaný. Poté jděte dolů a opakujte, dokud nenajdete prvek.
- Vložení: Vložte prvek do seznamu na správné místo a rozhodněte o počtu ukazatelů pomocí náhodného procesu
- Mazání: Nalezněte prvek a odstraňte ho ze všech seznamů, na kterých se nachází.

## Složitost

- Vyhledávání: O(log n) průměrně
- Vložení: O(log n) průměrně
- Mazání: O(log n) průměrně

## Výhody

- Jednoduchost implementace.
- Vysoká rychlost operací v praxi.
- Nepotřebuje dodatečné paměťové nároky jako vyvážené stromy.

## Nevýhody

- V nejhorším případě mohou operace trvat O(n).
- Nezaručuje vyváženost, jako vyvážené stromy.

# Konečné automaty, regulární výrazy a operace nad regulárními jazyky

## Konečné automaty (Finite Automata)

- Konečný automat je model výpočtu, který funguje v diskrétních krocích.
- Dvě hlavní kategorie: Deterministické konečné automaty (DFA) a Nedeterministické konečné automaty (NFA).
- DFA má v každém stavu pro každý symbol vstupní abecedy přesně jedno přechodové pravidlo.
- NFA může mít více přechodových pravidel pro daný stav a symbol a může mít epsilon přechody.

## Regulární výrazy (Regular Expressions)

- Notace pro popis regulárních jazyků.
- Základní operace: konkatenace, unie (reprezentovaná znakem `|`), a Kleeneho hvězda (reprezentovaná znakem `*`).
- Například, regulární výraz `a*b` reprezentuje jazyk, který obsahuje libovolný počet 'a' následovaný jedním 'b'.

## Operace nad regulárními jazyky

- **Unie**: Množina slov, které jsou v jednom nebo druhém jazyku.
- **Konkatenace**: Množina slov, která se skládá ze slov z jednoho jazyka následovaných slovy z druhého jazyka.
- **Kleeneho hvězda**: Množina slov, které se skládají z libovolného počtu slov z daného jazyka.
- **Průnik**: Množina slov, které jsou současně v obou jazycích.
- **Rozdíl**: Množina slov, které jsou v jednom jazyku, ale nejsou v druhém.

Všechny tyto operace vytvářejí regulární jazyky z regulárních jazyků, což je důležitá vlastnost regulárních jazyků.

# Bitová reprezentace nedeterministických konečných automatů (NFA)

Nemůžu najít

# Algoritmy pro vyhledávání textu

## Přesné vyhledávání vzorců

- Přesné vyhledávání vzorců se snaží najít všechny výskyty konkrétního vzorce v textu.
- Příklady algoritmů: Knuth-Morris-Pratt, Boyer-Moore, Rabin-Karp.

## Aproximativní vyhledávání vzorců

- Aproximativní vyhledávání vzorců se snaží najít výskyty vzorce v textu, které mohou obsahovat chyby (vložení, vymazání, substituce).
- Dvě běžné metriky pro měření "vzdálenosti" mezi vzorcem a textem jsou Hammingova a Levenshteinova vzdálenost.

  - **Hammingova vzdálenost**: Počet pozic, na kterých se dvě řetězce stejné délky liší.

  - **Levenshteinova vzdálenost (editační vzdálenost)**: Minimální počet jednotkových operací (vložení, vymazání, substituce), potřebných k převedení jednoho řetězce na druhý.

## Automaty pro vyhledávání ve slovníku

- Automaty pro vyhledávání ve slovníku jsou efektivní pro vyhledávání mnoha vzorců současně.
- Příkladem je Aho-Corasickův algoritmus, který vytváří trie (prefixový strom) ze všech vzorců a poté prochází textem, aby našel výskyty vzorců.
