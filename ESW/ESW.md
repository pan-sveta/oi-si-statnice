# ESW

## Topics
Effective algorithms and optimization methods. Data structures, synchronization and multithreaded programs. BE4M36ESW (Course web pages)

## Questions
- Java Virtual Machine, memory layout, frame, stack-oriented machine processing, ordinary object pointer, compressed ordinary object pointer. JVM bytecode, Just-in-time compiler, tired compilation, on-stack replacement, disassembler, decompiler. Global and local safe point, time to safe point. Automatic memory Management, generational hypothesis, garbage collectors. CPU and memory profiling, sampling and tracing approach, warm-up phase.
- Data races, CPU pipelining and superscalar architecture, memory barrier, volatile variable. Synchronization - thin, fat and biased locking, reentrant locks. Atomic operations based on compare-and-set instructions, atomic field updaters. Non-blocking algorithms,  wait free algorithms, non-blocking stack (LIFO).
- Static and dynamic memory analysis, shallow and retained size, memory leak. Data Structures, Java primitives and objects, auto-boxing and unboxing, memory efficiency of complex data structures. Collection for performance, type specific collections, open addressing hashing, collision resolution schemes. Bloom filters, complexity, false positives, bloom filter extensions. Reference types - weak, soft, phantom.
- JVM object allocation, thread-local allocation buffers, object escape analysis, data locality, non-uniform memory allocation.
- Networking, OSI model, C10K problem. Blocking and non-blocking input/output, threading server, event-driven server. Event-based input/output approaches. Native buffers in JVM, channels and selectors.
- Synchronization in multi-threaded programs (atomic operations, mutex, semaphore, rw-lock, spinlock, RCU). When to use which mechanism? Performance bottlenecks of the mentioned mechanisms. Synchronization in “read-mostly workloads”, advantages and disadvantages of different synchronization mechanisms.
- Cache-efficient data structures and algorithms (e.g., matrix multiplication). Principles of cache memories, different kinds of cache misses. Self-evicting code, false sharing – what is it and how deal with it?
- Profiling and optimizations of programs in compiled languages (e.g., C/C++). Hardware performance counters, profile-guided optimization. Basics of C/C++ compilers, AST, intermediate representation, high-level and low-level optimization passes.


## Java Virtual Machine (JVM) a paměťové rozložení:

- **JVM**:
  - Virtuální stroj, který umožňuje spouštět Java aplikace
  - Nezávislý na platformě
  - Překládá Java bytecode do strojového kódu pro konkrétní systém
- **Paměťové rozložení**:
  - Skládá se z následujících oblastí:
    1. Metodický (Method) area
    2. Heap (Haldy)
    3. Java stacks
    4. PC (Program Counter) registry
    5. Nativní (Native) metoda stacks
- **Heap (Haldy)**
    - **New Generation**:
      - Mladší generace, kde se ukládají nově vytvořené objekty
      - Dále rozdělen na:
        - Eden Space: místo pro vytváření nových objektů
        - Survivor Spaces (S0 a S1): oblasti pro přeživší objekty z Eden Space
    - **Old Generation**:
        - Starší generace, kam se přesouvají objekty, které přežily několik cyklů Garbage Collection
        - Slouží pro dlouhodobě žijící objekty
- **Frame**:
  - Jednotka paměťového zásobníku (stack) pro každé volání metody
  - Obsahuje:
    - Lokální proměnné
    - Operandový zásobník
    - Odkaz na runtime konstantní pool
  - Při volání metody se vytváří nový rámec
  - Po dokončení metody se rámec uvolní z paměti

![JVM Memory layout](jvm.png)
![Frame](frame.png)

## Zásobníkově orientované stroje (Stack-oriented machine processing):

- Typ architektury stroje, který využívá zásobník pro provádění operací
- Vlastnosti:
  - Většina operací pracuje s daty na vrcholu zásobníku
  - Instrukce nemají explicitní registry pro uchovávání operandů
  - Operandy jsou načteny na zásobník a výsledky operací jsou uloženy zpět na zásobník
- Proces zpracování:
  1. Načtení operandů na vrchol zásobníku
  2. Provedení operace s vrchními prvky zásobníku
  3. Uložení výsledku operace zpět na vrchol zásobníku
- Výhody:
  - Menší a jednodušší instrukční sada
  - Snadnější implementace v hardwaru nebo softwaru
- Nevýhody:
  - Méně efektivní zpracování dat kvůli častému přesouvání dat na zásobníku
  - Může být pomalejší než registry orientované stroje pro některé úkoly

## Běžný ukazatel na objekt (Ordinary Object Pointer):

- Ukazatel (nebo reference) používaný pro přístup k objektům v paměti
- Vlastnosti:
  - Umožňuje přímý přístup k objektu v paměti
  - Obvykle obsahuje adresu objektu v paměti
  - V některých jazycích (např. Java) může být ukazatel automaticky aktualizován při přesunu objektu (např. během Garbage Collection)
- Použití:
  - Pro přístup k atributům objektu
  - Pro volání metod objektu
  - Pro předávání objektů jako parametrů funkcí nebo metod
- Bezpečnost:
  - V některých jazycích (např. Java, C#) jsou ukazatele na objekty automaticky spravovány a nemohou být modifikovány programátorem
  - V jiných jazycích (např. C, C++) může být práce s ukazateli riskantní kvůli možnosti chyb v alokaci nebo dealokaci paměti

## Komprimovaný ukazatel na objekt (Compressed Ordinary Object Pointer):

- Speciální typ ukazatele na objekt, který šetří paměťový prostor
- Princip:
  - Místo ukládání celé adresy objektu v paměti, ukládá pouze část adresy
  - Tím šetří paměťový prostor při uložení ukazatelů
- Využití:
  - Často používán v prostředích s omezenou pamětí, jako jsou embedded systémy nebo JVM s velkou haldou
- Proces:
  1. Komprese: při vytvoření ukazatele se adresa objektu komprimuje a uloží do komprimovaného ukazatele
  2. Dekomprese: při přístupu k objektu se komprimovaná adresa dekomprimuje, čímž se získá původní adresa objektu v paměti
- Výhody:
  - Šetří paměťový prostor
  - Může zlepšit výkon díky menšímu množství paměťových přístupů
- Nevýhody:
  - Potřeba provádět kompresi a dekompresi při práci s ukazateli
  - Omezený rozsah adres, ke kterým lze přistupovat pomocí komprimovaných ukazatelů (závisí na velikosti komprimovaného ukazatele)

## JVM Bytecode:

- Středně-úrovňový kód generovaný překladačem Java (javac) z Java zdrojového kódu
- Vlastnosti:
  - Platformově nezávislý
  - Interpretován nebo kompilován do strojového kódu pomocí Java Virtual Machine (JVM)
  - Instrukce o délce 1 bajtu (byte), odtud název bytecode
- Struktura:
  - Sestává z posloupnosti instrukcí, které mohou zahrnovat:
    - Načítání a ukládání proměnných
    - Aritmetické a logické operace
    - Kontrola toku (podmínky, smyčky)
    - Volání metod
    - Práce s objekty a třídami
- Proces:
  1. Překlad: Java zdrojový kód je přeložen do bytecode pomocí javac
  2. Načtení: Bytecode je načten do JVM
  3. Interpretace nebo kompilace: Bytecode je interpretován nebo kompilován do strojového kódu pomocí JVM
  4. Spuštění: Strojový kód je spuštěn na cílovém systému
- Výhody:
  - Platformová nezávislost
  - Snadný přenos mezi různými systémy
  - Možnost optimalizace během kompilace do strojového kódu
- Nevýhody:
  - Pomalejší než nativní strojový kód
  - Vyžaduje instalaci JVM na cílovém systému

## Just-In-Time (JIT) kompilátor:
- Kompilátor, který kompiluje kód za běhu programu místo před jeho spuštěním
- Princip:
  - Kompilace zdrojového kódu do nativního strojového kódu za běhu programu
  - Probíhá dynamicky, "na požádání"
- Proces:
  1. Načtení: Zdrojový kód je načten do virtuálního stroje nebo runtime prostředí
  2. Interpretace: Zdrojový kód je nejprve interpretován
  3. Profiling: Během interpretace je prováděn profiling kódu pro zjištění často volaných částí (hotspots)
  4. Kompilace: JIT kompilátor kompiluje často volané části zdrojového kódu do nativního strojového kódu
  5. Spuštění: Nativní strojový kód je spuštěn na cílovém systému
- Příklad: Java Virtual Machine (JVM) používá JIT kompilátor pro kompilaci Java bytecode do nativního strojového kódu za běhu
- Výhody:
  - Rychlejší běh programu než při pouhé interpretaci
  - Možnost optimalizace kódu za běhu na základě aktuálního chování programu
  - Přizpůsobení kódu specifickým vlastnostem hardware a operačního systému za běhu
- Nevýhody:
  - Vyšší režie při kompilaci za běhu, což může zpomalit spuštění programu
  - Vyžaduje více paměti pro uchování kompilovaného kódu

## Tiered Compilation (Stupňovitá kompilace):
- Technika používaná u Just-In-Time (JIT) kompilátorů, která kombinuje různé úrovně optimalizace
- Princip:
  - Kód je postupně kompilován a optimalizován na základě jeho výkonu a četnosti volání
  - Používá více úrovní kompilace s různými úrovněmi optimalizace
- Proces:
  1. Načtení: Zdrojový kód je načten do virtuálního stroje nebo runtime prostředí
  2. Interpretace: Zdrojový kód je nejprve interpretován
  3. Nízkoúrovňová kompilace: Často volané části kódu jsou kompilovány s nízkou úrovní optimalizace (rychlejší kompilace, méně optimalizací)
  4. Profiling: Během běhu programu se sbírají informace o výkonu kompilovaného kódu
  5. Vysokoúrovňová kompilace: Pokud je to výhodné, části kódu mohou být kompilovány s vyšší úrovní optimalizace (pomalejší kompilace, více optimalizací)
- Příklad: Java Virtual Machine (JVM) podporuje tiered compilation v rámci svého JIT kompilátoru
- Výhody:
  - Rychlejší spuštění programu díky rychlé nízkoúrovňové kompilaci
  - Možnost využít vysokoúrovňové optimalizace pro části kódu, které mají zásadní vliv na výkon programu
  - Lepší vyvážení mezi rychlostí kompilace a výkonem programu
- Nevýhody:
  - Vyšší režie při provádění více úrovní kompilace a profilingu za běhu programu
  - Vyžaduje více paměti pro uchování kompilovaného kódu a profilingových dat

## On-Stack Replacement (OSR):

- Technika používaná v Just-In-Time (JIT) kompilátorech pro optimalizaci běžících funkcí za běhu programu
- Princip:
  - Nahrazuje aktuálně běžící funkci (interpretovanou nebo kompilovanou s nižší úrovní optimalizace) její optimalizovanou verzí
  - Umožňuje získat výhody optimalizací i pro dlouho běžící funkce
- Proces:
  1. Profiling: Během běhu programu se sbírají informace o výkonu funkcí
  2. Optimalizace: JIT kompilátor kompiluje optimalizovanou verzi funkce
  3. Nahrazení: Aktuálně běžící funkce je nahrazena optimalizovanou verzí
  4. Spuštění: Optimalizovaná funkce pokračuje v běhu od místa, kde byla původní funkce přerušena
- Příklad: Java Virtual Machine (JVM) podporuje on-stack replacement v rámci svého JIT kompilátoru
- Výhody:
  - Zlepšení výkonu dlouho běžících funkcí díky optimalizacím
  - Umožňuje aplikovat optimalizace za běhu programu bez nutnosti restartu
- Nevýhody:
  - Vyšší režie při provádění nahrazení běžící funkce
  - Složitost implementace OSR ve virtuálním stroji nebo JIT kompilátoru


## Disassembler

- Nástroj, který převádí strojový kód nebo spustitelný soubor zpět na čitelnější formát, jako je assembler
- Princip:
  - Analyzuje strojový kód a hledá odpovídající assemblerové instrukce
  - Vytváří textový výstup s assemblerovým kódem a dalšími informacemi, jako jsou adresy, hodnoty registrů, atd.
- Proces:
  1. Načtení: Disassembler načte strojový kód nebo spustitelný soubor
  2. Dekódování: Strojové instrukce jsou dekódovány na odpovídající assemblerové instrukce
  3. Výstup: Výsledný assemblerový kód je zobrazen nebo uložen do souboru
- Použití:
  - Analýza a ladění spustitelných souborů
  - Zjištění funkcionality neznámého nebo podezřelého kódu (např. malware)
  - Reverzní inženýrství, zkoumání algoritmů a optimalizací v cizím kódu
- Výhody:
  - Umožňuje získat vhled do chování strojového kódu nebo spustitelného souboru
  - Pomáhá při analýze a ladění programů
- Nevýhody:
  - Assemblerový kód je obtížnější číst a porozumět než zdrojový kód vysokoúrovňových jazyků
  - Ztráta informace o proměnných, funkcích a komentářích, které byly v původním zdrojovém kódu
  - Může být omezen na konkrétní architekturu nebo operační systém

## Decompiler

- Nástroj, který převádí strojový kód nebo spustitelný soubor zpět na zdrojový kód vysokoúrovňového programovacího jazyka
- Princip:
  - Analyzuje strojový kód a rekonstruuje odpovídající zdrojový kód vysokoúrovňového jazyka
  - Vytváří textový výstup se zdrojovým kódem a dalšími informacemi, jako jsou názvy proměnných, funkce, atd.
- Proces:
  1. Načtení: Dekompilátor načte strojový kód nebo spustitelný soubor
  2. Dekódování: Strojové instrukce jsou dekódovány a zkonstruován odpovídající zdrojový kód vysokoúrovňového jazyka
  3. Výstup: Výsledný zdrojový kód je zobrazen nebo uložen do souboru
- Použití:
  - Analýza a ladění spustitelných souborů
  - Zjištění funkcionality neznámého nebo podezřelého kódu (např. malware)
  - Reverzní inženýrství, zkoumání algoritmů a optimalizací v cizím kódu
- Výhody:
  - Umožňuje získat vhled do chování strojového kódu nebo spustitelného souboru v čitelnější formě
  - Pomáhá při analýze a ladění programů
- Nevýhody:
  - Získaný zdrojový kód může být méně čitelný a komplexnější než původní zdrojový kód
  - Ztráta informace o původních názvech proměnných, funkcí a komentářích
  - Může být omezen na konkrétní programovací jazyk, architekturu nebo operační systém

## Globální a lokální bezpečný bod (Global and Local Safe Point):
- Koncept používaný v runtime systémech, např. Java Virtual Machine (JVM)
- Bezpečný bod je místo v kódu, kde se runtime prostředí může přesvědčit, že žádné nebezpečné operace nebudou probíhat (např. úpravy objektů v paměti)
- Umožňuje provádět akce, které vyžadují kooperaci mezi vlákny nebo synchronizaci s garbage collectorem

## Globální bezpečný bod (Global Safe Point):
- Všechna vlákna v runtime prostředí jsou pozastavena na bezpečných bodech
- Často využíván při stop-the-world fázi garbage collectoru
- Výhody:
  - Zjednodušuje garbage collection, protože nedochází k současným úpravám objektů
  - Umožňuje provádět operace s globálním dopadem na runtime prostředí
- Nevýhody:
  - Způsobuje přerušení všech vláken, což může způsobit zpoždění a snížení výkonu aplikace

## Lokální bezpečný bod (Local Safe Point):
- Vlákno dosáhne bezpečného bodu nezávisle na ostatních vláknech
- Používá se pro akce, které vyžadují kooperaci mezi vlákny, ale nepotřebují zastavit všechna vlákna
- Výhody:
  - Méně náročné na výkon než globální bezpečný bod, protože nepozastavuje všechna vlákna
  - Umožňuje provádět operace s lokálním dopadem na runtime prostředí
- Nevýhody:
  - Může být složitější koordinovat akce mezi vlákny
  - Méně vhodné pro operace s globálním dopadem na runtime prostředí

## Čas do bezpečného bodu (Time to Safe Point):
- Metrika používaná pro měření doby, kterou trvá jednotlivým vláknům dosáhnout bezpečného bodu v runtime prostředí, např. Java Virtual Machine (JVM)
- Důležitá pro koordinaci akcí mezi vlákny a při garbage collection
- Měří časovou prodlevu mezi rozhodnutím o zastavení vláken na bezpečných bodech a skutečným dosažením těchto bodů

Faktory ovlivňující čas do bezpečného bodu:

- Délka části kódu mezi bezpečnými body
- Výkon a zátěž vláken
- Frekvence volání bezpečných bodů v kódu
- Implementace a nastavení runtime prostředí

Význam času do bezpečného bodu:

- Krátký čas do bezpečného bodu zvyšuje pružnost runtime prostředí a umožňuje rychlejší koordinaci mezi vlákny a garbage collectorem
- Dlouhý čas do bezpečného bodu může způsobit zpoždění a snížení výkonu aplikace, protože vlákna nemohou být rychle zastavena pro kooperaci s garbage collectorem nebo pro jiné akce vyžadující koordinaci mezi vlákny
- Optimalizace kódu a runtime prostředí mohou pomoci snížit čas do bezpečného bodu, např. zvyšováním frekvence volání bezpečných bodů nebo zlepšením implementace bezpečných bodů

## Automatické správa paměti (Automatic Memory Management):
- Koncept, který se používá v programovacích jazycích a runtime prostředích, kde je paměťová správa automaticky řízena systémem, např. Java Virtual Machine (JVM)
- Hlavní součástí automatické správy paměti je garbage collector

Funkce automatické správy paměti:
- Alokace paměti: Přidělení paměti pro nové objekty a proměnné
- Uvolňování paměti: Systém automaticky detekuje a uvolňuje paměť, která již není potřeba (nepoužívané objekty)
- Minimalizace úniku paměti a fragmentace: Garbage collector se snaží minimalizovat úniky paměti a její fragmentaci

Výhody automatické správy paměti:
- Zjednodušuje programování, protože se programátor nemusí starat o přidělování a uvolňování paměti
- Snížení chyb spojených s paměťovou správou, jako jsou úniky paměti nebo přístup k nealokované paměti
- Zvyšuje bezpečnost a stabilitu aplikace, protože garbage collector detekuje a řeší problémy s paměťovou správou

Nevýhody automatické správy paměti:
- Vyšší režie a zátěž systému kvůli garbage collectoru a automatickému přidělování/uvolňování paměti
- Menší kontrola nad správou paměti, což může vést k suboptimálnímu výkonu aplikace v některých případech
- Předvídatelnost a výkon garbage collectoru závisí na implementaci a konfiguraci runtime prostředí

## Generační hypotéza (Generational Hypothesis):
- Teorie, která se používá při návrhu a implementaci garbage collectorů v automatických správách paměti, jako je Java Virtual Machine (JVM)
- Hypotéza předpokládá, že většina objektů v paměti má krátkou životnost, zatímco jen malé procento objektů má dlouhou životnost

Principy generační hypotézy:

1. Mnoho objektů zemře mladých: Většina objektů má krátkou životnost a je rychle zničena
2. Málo starých objektů odkazuje na mladé: Méně často dochází k odkazům mezi starými a mladými objekty
3. Málo objektů přežije dlouhou dobu: Jen malé procento objektů má dlouhou životnost

Aplikace generační hypotézy na garbage collectory:

- Garbage collectory využívají generační hypotézu pro optimalizaci paměťové správy
- Paměť je rozdělena na dvě nebo více generací, např. "new generation" (mladá generace) a "old generation" (stará generace)
- Mladá generace obsahuje nově vytvořené objekty, které mají tendenci rychle zaniknout
- Stará generace obsahuje objekty, které přežily několik cyklů garbage collection a mají tendenci mít delší životnost
- Garbage collector se zaměřuje na mladou generaci, kde často probíhá uvolňování paměti, a méně často na starou generaci

Výhody použití generační hypotézy:

- Zlepšuje výkon garbage collectoru, protože se zaměřuje na části paměti, kde je největší pravděpodobnost uvolnění paměti
- Snížení režie a zátěže systému spojené s garbage collection
- Minimalizace zpoždění a přerušení způsobených garbage collection

Nevýhody použití generační hypotézy:

- Vyšší složitost implementace garbage collectoru
- Možná suboptimální výkon v případech, kdy hypotéza neodpovídá skutečnému chování aplikace

## Garbage Collectory:

- Součást automatické správy paměti v runtime prostředích, jako je Java Virtual Machine (JVM)
- Starají se o automatické uvolňování paměti, která již není používána (nepotřebné objekty)
- Zajišťují, že aplikace nevyčerpá dostupnou paměť a snižují riziko úniků paměti

Některé typy garbage collectorů:

1. Mark and Sweep (Označit a Zamést):
   - Pracuje ve dvou fázích:
     1. Označení: Prochází živé objekty a označuje je jako dosažitelné
     2. Zametání: Uvolňuje paměť obsazenou objekty, které nebyly označeny jako dosažitelné
   - Nevýhody: Může způsobovat fragmentaci paměti a zpoždění při provádění garbage collection

2. Copying (Kopírování):
   - Paměť je rozdělena na dvě poloviny: Aktivní a rezervní
   - Živé objekty jsou kopírovány z aktivní do rezervní paměti
   - Jakmile jsou všechny živé objekty kopírovány, celá aktivní paměť je uvolněna
   - Nevýhody: Vyžaduje více paměti, protože je rozdělena na dvě části, a může způsobit zpoždění při provádění garbage collection

3. Generational (Generační):
   - Paměť je rozdělena na mladou a starou generaci
   - Využívá generační hypotézu pro efektivnější garbage collection
   - Častěji provádí garbage collection v mladé generaci, kde je vyšší pravděpodobnost uvolnění paměti
   - Výhody: Snížení režie a zátěže systému, minimalizace zpoždění způsobených garbage collection
   - Nevýhody: Vyšší složitost implementace

4. Concurrent (Souběžný):
   - Provádí garbage collection současně s během aplikace, bez nutnosti zastavit všechna vlákna
   - Výhody: Snížení zpoždění a přerušení způsobených garbage collection, lepší výkon aplikace
   - Nevýhody: Vyšší složitost implementace a koordinace s běžícími vlákny

5. Incremental (Inkrementální):
   - Rozděluje garbage collection do menších částí, které jsou prováděny postupně
   - Výhody: Snížení zpoždění a přerušení způsoben

## CPU a paměťový profiling:

- Techniky používané pro analýzu výkonu a chování aplikace s ohledem na zpracování CPU a využití paměti
- Cílem je identifikovat horké body (bottlenecks), optimalizovat výkon a zlepšit paměťovou efektivitu aplikace

CPU profiling:
- Zaměřuje se na měření a analýzu výkonu aplikace v souvislosti s využitím procesoru
- Identifikuje funkce a části kódu, které vyžadují nejvíce času na zpracování
- Pomáhá zjistit, kde lze provést optimalizace kódu pro zlepšení celkového výkonu aplikace

Metody CPU profilingu:
1. Sampling (vzorkování): Pravidelně sbírá informace o zásobníku volání (call stack) během běhu aplikace
2. Instrumentace: Vkládá sledovací kód přímo do aplikace, který zaznamenává informace o výkonu a zátěži CPU

Paměťový profiling:
- Zaměřuje se na analýzu využití paměti aplikací
- Identifikuje objekty, které způsobují zvýšené využití paměti, úniky paměti nebo fragmentaci paměti
- Pomáhá zjistit, jak lze zlepšit paměťovou efektivitu a snížit nároky na paměť aplikace

Metody paměťového profilingu:
1. Heap snapshot (snímek haldy): Zaznamenává stav paměti (haldy) v určitém čase, identifikuje objekty a jejich velikosti
2. Allocation tracking (sledování alokace): Sleduje vytváření a uvolňování objektů v paměti během běhu aplikace
3. Garbage collection profiling: Analyzuje chování garbage collectoru, identifikuje dlouhotrvající operace a možné optimalizace

Nástroje pro CPU a paměťový profiling:
- Existuje mnoho nástrojů a knihoven pro různé jazyky a prostředí, například:
  - VisualVM (pro Java)
  - Valgrind (pro C/C++)
  - Py-Spy (pro Python)
  - Ruby-prof (pro Ruby)

## Vzorkování (Sampling) a trasování (Tracing) přístup:
- Dvě hlavní metody používané při profilování výkonu aplikací, zejména v souvislosti s CPU a paměťovým profilingem

Vzorkování (Sampling):

- Pravidelně sbírá informace o zásobníku volání (call stack) během běhu aplikace
- Zkoumá výkon aplikace v pravidelných intervalech a zaznamenává aktuální stav
- Menší režie než u trasování, protože se nezasahuje do každé funkce nebo události
- Méně přesné než trasování, protože data jsou založena na vzorcích a mohou být ovlivněna časováním nebo frekvencí vzorkování

Trasování (Tracing):

- Vkládá sledovací kód přímo do aplikace, který zaznamenává informace o výkonu a zátěži
- Sleduje všechny funkce, události a interakce v aplikaci, což poskytuje detailní informace o výkonu
- Vyšší režie než u vzorkování, protože se zaznamenává každá funkce a událost
- Přesnější než vzorkování, protože data jsou založena na skutečném chování aplikace, nikoli na vzorcích

Kdy použít vzorkování nebo trasování:

- Vzorkování je vhodné pro rychlou a hrubou analýzu výkonu aplikace, kde je důležitější minimalizace režie než přesnost dat
- Trasování je vhodné pro detailní a přesnou analýzu výkonu aplikace, kde je důležitější získat kompletní informace o chování aplikace než minimalizovat režii
- Ve většině případů je vhodné použít kombinaci obou přístupů pro dosažení nejlepších výsledků při analýze výkonu aplikace

## Fáze rozehřátí (Warm-up phase):
- Období, kdy se aplikace nebo systém rozehřívá a dosahuje optimálního výkonu
- Během fáze rozehřátí může aplikace nebo systém provádět různé inicializační úkoly, kompilaci, optimalizace nebo jiné nastavení
- Výkon aplikace nebo systému během fáze rozehřátí může být pomalejší než po dosažení optimálního výkonu

Důvody pro fázi rozehřátí:
1. Just-In-Time (JIT) kompilace: Aplikace založené na bytecode, jako je Java, používají JIT kompilátor pro kompilaci bytecode na strojový kód během runtime. Tato kompilace může trvat určitý čas a zpočátku zpomalit výkon.
2. Profilování a optimalizace: Aplikace nebo systém mohou provádět profilování a optimalizace během fáze rozehřátí, což může způsobit zpoždění v dosažení plného výkonu.
3. Cache a přednačítání: Aplikace mohou mít cache nebo přednačítání dat, které mohou být potřeba pro rychlejší běh. Tyto cache nebo přednačítaná data se mohou postupně naplňovat během fáze rozehřátí.

Jak zohlednit fázi rozehřátí při testování výkonu:
- Během testování výkonu je důležité zohlednit fázi rozehřátí, protože může ovlivnit výsledky testů
- Testy by měly být prováděny po dosažení optimálního výkonu aplikace nebo systému, aby poskytovaly správné a relevantní výsledky
- Mohou být použity různé techniky pro zohlednění fáze rozehřátí, například:
  - Provedení několika krátkých běhů aplikace nebo testů před spuštěním hlavního testu
  - Použití statistických metod pro eliminaci nebo minimalizaci vlivu fáze rozehřátí na výsledky testů

## Data race (soupeření o data):
- Problém v paralelním programování, kdy dojde ke konkurenčnímu přístupu dvou nebo více vláken k témuž datovému objektu bez vhodné synchronizace
- Může vést k nekonzistentním a nepředvídatelným výsledkům, což ztěžuje ladění a opravu chyb
- Nejčastěji se vyskytuje v programovacích jazycích, které umožňují ruční správu vláken a synchronizaci, jako jsou C++, Java nebo C#

Příčiny data race:
1. Neexistující nebo nesprávná synchronizace přístupu k datům
2. Chybějící zámky (locks) nebo bariéry (barriers) pro omezení přístupu k datům
3. Nesprávná implementace atomických operací nebo kritických sekcí

Jak předcházet data race:
1. Použití zámků (locks) pro zajištění vzájemného vyloučení při přístupu k datům
2. Využití atomických operací, které zajišťují, že během provedení operace nedojde k přerušení vlákny
3. Použití bariér (barriers) nebo podmínek (conditions) pro koordinaci a synchronizaci vláken
4. Vhodná dekompozice úloh a dat pro snížení potřeby sdílení dat mezi vlákny
5. Použití vysokoúrovňových abstrakcí a knihoven pro paralelní programování, které řeší synchronizaci za vás (např. OpenMP, TBB, C++11 threads)

Detekce data race:
- Existují nástroje a techniky pro automatickou detekci data race, například:
  - Statická analýza kódu: Nástroje jako Clang Static Analyzer nebo PVS-Studio mohou pomoci identifikovat možné data race v kódu
  - Dynamická analýza běhu: Nástroje jako Helgrind (součást Valgrind), ThreadSanitizer nebo Intel Inspector mohou sledovat běh aplikace a detekovat data race za běhu

## CPU pipelining (potrubí) a superskalární architektura:

CPU pipelining (potrubí):

- Technika zvyšování výkonu procesoru tím, že se zpracování instrukcí rozdělí do několika menších kroků (fází)
- Každá fáze zpracovává část instrukce a poté ji předává další fázi
- Umožňuje paralelní zpracování více instrukcí, kdy každá instrukce prochází jednotlivými fázemi potrubí

Superskalární architektura:

- Rozšíření pipeliningu, které umožňuje zpracovávat více instrukcí současně v rámci jednoho cyklu hodinových tiků
- Superskalární procesory mají více výkonných jednotek, které mohou zpracovávat instrukce paralelně
- Díky této architektuře je možné dosáhnout vyššího výkonu a rychlejšího zpracování instrukcí než u tradičních pipelined procesorů

Kombinace CPU pipeliningu a superskalární architektury:

1. Instrukce jsou načítány do potrubí a rozděleny do menších kroků (fází)
2. Procesor s superskalární architekturou může zpracovávat více instrukcí současně v rámci jednoho cyklu hodinových tiků
3. Výsledkem je vyšší výkon a rychlejší zpracování instrukcí

Příklady procesorů s pipeliningem a superskalární architekturou:

- Většina moderních procesorů (Intel Core, AMD Ryzen) používá kombinaci pipeliningu a superskalární architektury pro dosažení vysokého výkonu

## Paměťová bariéra (Memory barrier):
- Mechanismus v paralelním programování, který zajišťuje správné pořadí přístupu k paměti mezi různými vlákny nebo procesory
- Pomáhá předcházet problémům se souběžností, jako jsou data race nebo nekonzistence paměti
- Paměťové bariéry mohou být implementovány na úrovni hardware (CPU instrukce) nebo software (programovací jazyk, knihovny)

Účel paměťových bariér:

1. Zajištění, že zápis nebo čtení určitých dat je dokončeno před pokračováním dalších operací
2. Zajištění, že změny v paměti provedené jedním vláknem nebo procesorem jsou viditelné pro ostatní vlákna nebo procesory
3. Zajištění, že operace na sdílených datech jsou prováděny ve správném pořadí

Příklady paměťových bariér:

- V jazyce C++ mohou být použity atomické operace s různými paměťovými řády (memory_order) pro zajištění správného pořadí přístupu k paměti
- V jazyce Java mohou být použity synchronizované bloky nebo volatile proměnné pro zajištění správného pořadí přístupu k paměti
- Některé CPU instrukce, jako je mfence, sfence a lfence na platformě x86, poskytují paměťové bariéry na úrovni hardware

Použití paměťových bariér:

- Paměťové bariéry by měly být použity v situacích, kdy je důležité zajistit správné pořadí přístupu k paměti mezi vlákny nebo procesory
- Správné použití paměťových bariér může pomoci předcházet problémům s nekonzistencí paměti a data race, ale může také způsobit pokles výkonu
- Je důležité pečlivě zvážit potřebu paměťových bariér a použít je jen tam, kde je to nezbytné, aby se minimalizoval vliv na výkon

## Volatile proměnná:
- Klíčové slovo `volatile` v programovacích jazycích (jako C, C++ nebo Java) označuje proměnnou, která může být změněna vnějšími procesy nebo paralelními vlákny
- Při použití `volatile` kompilátor a běhové prostředí zajišťují, že přístupy k této proměnné nebudou optimalizovány ani mezipaměťovány, což zajišťuje konzistentní a aktuální hodnoty pro všechna vlákna

### Java
- `volatile` v Javě se používá pro označení proměnné, jejíž hodnota může být modifikována více vlákny a jejíž přístupy by neměly být optimalizovány.
- Klíčové vlastnosti:
  - Viditelnost: Čtení a zápis proměnné označené jako `volatile` jsou zaručeně viditelné pro ostatní vlákna.
  - Pořadí: Ustanovuje vzájemný vztah happens-before, což zajišťuje, že akce před zápisem do `volatile` proměnné se provedou před následujícími akcemi po jejím čtení.
  - Atomické R/W operace
- Použití:
  - Jednoduché příznakové proměnné sdílené mezi více vlákny.
  - Koordinace mezi vlákny pomocí sdílené proměnné.
- Omezení:
  - Neposkytuje atomicitu pro složené operace.
  - Omezené synchronizační schopnosti ve srovnání s `synchronized` bloky, zámky nebo atomickými třídami.

### C++
- Klíčové slovo `volatile` v C++ označuje, že hodnota proměnné se může kdykoliv změnit bez vědomí kompilátoru, často z důvodu externích faktorů.
- Klíčové vlastnosti:
  - Čtení/Zápis volatile: Přikazuje kompilátoru vždy číst a zapisovat do paměti pro danou proměnnou, aniž by se spoléhal na mezipaměťové hodnoty.
  - Externí modifikace: Označuje, že proměnnou mohou měnit externí faktory, jako je hardware nebo jiná vlákna.
- Použití:
  - Přístup k registrům hardware připojených k paměti.
  - Vícevláknové prostředí, kde více vláken přistupuje ke stejné proměnné.
- Omezení:
  - Samotné `volatile` neposkytuje záruky synchronizace nebo atomicity.
  - Pro synchronizaci a viditelnost napříč více jádry nebo vlákny je nutné použít vhodné synchronizační mechanismy, jako jsou mutexy, atomické typy nebo bariéry paměti.


## Synchronizace - tenké (thin), tlusté (fat) a zaujaté (biased) zámky:

Tenký zámek (Thin lock):

- Lehký zámek s nízkým režijním zatížením, používaný v situacích, kdy není vysoká kontestace mezi vlákny
- Rychlý a efektivní způsob zajištění synchronizace pro jednoduché případy
- V případě zvýšené kontestace mezi vlákny může být tenký zámek transformován na tlustý zámek

Tlustý zámek (Fat lock):

- Robustnější zámek s vyšším režijním zatížením, používaný v situacích, kdy je vysoká kontestace mezi vlákny
- Poskytuje lepší výkon při zajištění synchronizace v případě, že se více vláken soupeří o přístup ke sdíleným zdrojům
- Transformace z tenkého zámku na tlustý zámok probíhá za běhu, pokud je to nutné

Zaujatý zámek (Biased locking):

- Optimalizace zámku, která zvyšuje výkon synchronizace v situacích, kdy objekt používá jedno vlákno a ostatní vlákna se o něj nezajímají
- Zámek je "zaujatý" ve prospěch jednoho vlákna, které může provádět synchronizované operace bez nutnosti získávání zámku
- Pokud se objekt stane kontestovaným mezi více vlákny, zaujatý zámek může být zrušen a převeden na tenký nebo tlustý zámek

## Reentrant zámky:
- Typ synchronizačního mechanismu, který umožňuje vláknu získat zámek vícekrát, aniž by došlo k uváznutí (deadlock)
- Reentrant zámek sleduje, které vlákno drží zámek a kolikrát ho získalo
- Vlákno může opustit zámek pouze tehdy, pokud uvolní zámek stejný počet, kolikrát ho získalo

Vlastnosti reentrant zámků:

1. Povolují vnořené zamykání (nested locking), což umožňuje vláknu získat zámek vícekrát, aniž by došlo k uváznutí
2. Zvyšují robustnost kódu tím, že se zabrání uváznutí při opakovaném získání zámku stejným vláknem
3. Mohou poskytnout pokročilé funkce, jako je podpora přerušitelného zamykání, časově omezené zamykání nebo spravedlivé plánování

```java
  import java.util.concurrent.locks.ReentrantLock;

  ReentrantLock lock = new ReentrantLock();

  // Získání zámku
  lock.lock();
  try {
      // kritická sekce
  } finally {
      // Uvolnění zámku
      lock.unlock();
  }
```

```cpp
#include <mutex>

std::recursive_mutex mtx;

// Získání zámku
mtx.lock();
try {
    // kritická sekce
} catch (...) {
    // Uvolnění zámku
    mtx.unlock();
    throw;
}
// Uvolnění zámku
mtx.unlock();

```

## Atomické operace založené na instrukcích porovnat-a-nastavit (compare-and-set):
- Atomické operace, které kombinují porovnání a nastavení hodnoty v jediném nesdíleném (atomic) kroku
- Běžně používány pro implementaci bezpečných a efektivních synchronizačních mechanismů, jako jsou zámky, semafory nebo počítadla
- Základem pro mnoho lock-free a wait-free algoritmů, které umožňují vysoký výkon a škálovatelnost v paralelním prostředí

Princip compare-and-set (CAS) operace:

1. Porovnej hodnotu sdílené proměnné s očekávanou hodnotou
2. Pokud se hodnoty shodují, nastav novou hodnotu proměnné
3. Operace vrátí informaci, zda byla hodnota úspěšně nastavena nebo ne

Výhody compare-and-set operací:

- Poskytují atomičnost a zajišťují konzistenci dat při přístupu více vláken
- Mohou snižovat režijní zatížení v porovnání s tradičními zámky nebo synchronizačními mechanismy
- Umožňují vytvářet lock-free a wait-free algoritmy, které jsou škálovatelné a odolné vůči uváznutí (deadlock) a vyhladovění (starvation)

## Atomické aktualizátory polí (Atomic Field Updaters):

- Specializované utility pro atomické aktualizace polí objektů bez nutnosti vytvářet nové objekty s atomickými proměnnými
- Umožňují provádět operace na jednotlivých polích objektů, které jsou atomické a bezpečné při současném přístupu více vláken
- Zvyšují výkon a snižují režijní zatížení v paralelním prostředí díky snížení počtu vytvořených objektů

Výhody atomických aktualizátorů polí:

- Poskytují atomičnost a zajišťují konzistenci dat při přístupu více vláken k jednotlivým polím objektů
- Snížení režijního zatížení a zlepšení výkonu v paralelním prostředí díky menšímu počtu vytvořených objektů
- Umožňují vytvářet lock-free a wait-free algoritmy pro práci s objekty

Použití atomických aktualizátorů polí:

- V jazyce Java lze použít třídy `AtomicIntegerFieldUpdater`, `AtomicLongFieldUpdater` a `AtomicReferenceFieldUpdater` z balíčku `java.util.concurrent.atomic`
- Pro jejich použití je nutné definovat pole objektu jako `volatile`

## Neblokující algoritmy (Non-blocking algorithms):

- Typ algoritmů, které nezabraňují přístupu k sdíleným datům nebo zdrojům jiným vláknům, když je prováděna operace
- Zajišťují, že žádné vlákno nebude čekat na neomezeně dlouhou dobu na dokončení operace prováděné jiným vláknem
- Mohou být klasifikovány jako lock-free, wait-free nebo obstruction-free, v závislosti na garancích, které poskytují

Typy neblokujících algoritmů:

1. Lock-free algoritmy:
   - Zajišťují, že alespoň jedno vlákno dokončí svou operaci v konečném čase
   - Zabraňují uváznutí (deadlocks) a vyhladovění (starvation)
2. Wait-free algoritmy:
   - Poskytují garanci, že každé vlákno dokončí svou operaci v konečném čase
   - Zabraňují uváznutí, vyhladovění a čekání na dokončení jiných vláken
3. Obstruction-free algoritmy:
   - Poskytují garanci, že operace bude dokončena v konečném čase pouze v případě, že žádné jiné vlákno nezasahuje do provádění operace
   - Slabší záruky než lock-free a wait-free algoritmy, ale stále zabraňují uváznutí

Výhody neblokujících algoritmů:

- Vysoký výkon a škálovatelnost v paralelním prostředí
- Zabraňují uváznutí a vyhladovění, které mohou nastat při použití tradičních zámků a synchronizačních mechanismů
- Zvyšují robustnost a spolehlivost paralelního kódu díky snížení možnosti uváznutí a vyhladovění

## Wait-free algoritmy:

- Speciální třída neblokujících algoritmů, které poskytují nejlepší záruky konvergence pro současně běžící vlákna
- Zajišťují, že každé vlákno dokončí svou operaci v konečném čase bez ohledu na chování ostatních vláken
- Zabraňují problémům, jako je uváznutí (deadlock), vyhladovění (starvation) a zbytečné čekání na dokončení jiných vláken

Vlastnosti wait-free algoritmů:
1. Konečná konvergence: Každé vlákno dokončí svou operaci v konečném čase, bez ohledu na ostatní vlákna
2. Robustnost: Odpovědnost za dokončení operace leží na provádějícím vlákně, což zabraňuje závislosti na chování jiných vláken
3. Spravedlivost: Žádné vlákno nemůže být trvale blokováno jiným vláknem, což zabraňuje vyhladovění

Výhody wait-free algoritmů:
- Vysoká škálovatelnost a výkon v paralelním prostředí
- Zlepšení spolehlivosti a robustnosti paralelního kódu díky odstranění závislosti na chování jiných vláken
- Poskytují nejlepší záruky konvergence ze všech typů neblokujících algoritmů

Příklady wait-free algoritmů:
- Wait-free fronty, zásobníky nebo počítadla, které zajišťují spravedlivý přístup ke sdíleným datovým strukturám
- Wait-free implementace atomických proměnných nebo operací, jako jsou compare-and-set nebo fetch-and-add

Použití wait-free algoritmů může být složitější než použití lock-free nebo obstruction-free algoritmů, ale poskytuje nejlepší záruky pro paralelní výpočty.

## Neblokující zásobník (LIFO) - Non-blocking Stack:

- Zásobník implementovaný jako neblokující datová struktura, která umožňuje současný přístup více vláken bez nutnosti použití zámků nebo synchronizačních mechanismů
- Používá atomické operace, jako jsou compare-and-set (CAS), pro zajištění konzistence a bezpečnosti dat při současném přístupu více vláken
- Zabraňuje problémům, jako je uváznutí (deadlock) a vyhladovění (starvation), které mohou nastat při použití tradičních zámků a synchronizačních mechanismů

Základní operace nebokujícího zásobníku (LIFO):

1. Push: Přidání prvku na vrchol zásobníku
2. Pop: Odebrání prvku z vrcholu zásobníku

Implementace nebokujícího zásobníku (LIFO):

- Základem implementace je spojový seznam s hlavou (head), která ukazuje na vrchol zásobníku
- Pro operaci Push a Pop se používá compare-and-set (CAS) operace, která zajišťuje atomičnost a konzistenci dat při přístupu více vláken
- V případě, že CAS operace selže, vlákno opakuje operaci, dokud není úspěšná

Výhody nebokujícího zásobníku (LIFO):

- Vysoký výkon a škálovatelnost v paralelním prostředí díky snížení režijního zatížení spojeného se zámky a synchronizací
- Zabraňuje uváznutí (deadlock) a vyhladovění (starvation), které mohou nastat při použití tradičních zámků a synchronizačních mechanismů
- Zvyšuje robustnost a spolehlivost paralelního kódu díky odstranění možnosti uváznutí a vyhladovění

## Statická a dynamická analýza paměti:

Statická analýza paměti:

- Provádí kontrolu zdrojového kódu bez jeho spuštění
- Identifikuje potenciální problémy s pamětí, jako jsou úniky paměti (memory leaks), neinicializované proměnné nebo nesprávné uvolňování paměti
- Zahrnuje kontrolu správnosti kódu, hledání nebezpečných funkcí nebo analýzu toku dat
- Pomáhá odhalit chyby a zlepšit kvalitu kódu před jeho spuštěním

Dynamická analýza paměti:

- Provádí kontrolu během provádění programu, monitoruje jeho chování a alokaci paměti
- Identifikuje problémy s pamětí v reálném čase, jako jsou úniky paměti, přístupy mimo rozsah pole nebo nesprávné uvolňování paměti
- Vyžaduje spuštění programu a sledování jeho chování, což může způsobit zpomalení běhu
- Umožňuje zjistit chyby, které nebyly odhaleny statickou analýzou, a poskytuje detailnější informace o problémech s pamětí

Výhody statické a dynamické analýzy paměti:

- Odhalení chyb, úniků paměti a problémů s pamětí, které mohou vést k nestabilitě nebo zranitelnostem v aplikaci
- Zlepšení kvality kódu a výkonu programu díky efektivnímu řešení problémů s pamětí
- Umožňuje vývojářům zaměřit se na kritické problémy a snížit riziko chyb ve výsledné aplikaci

## Mělká velikost (Shallow size) a zadržená velikost (Retained size):

Mělká velikost (Shallow size):
- Velikost paměti, kterou přímo zabírá objekt, bez zahrnutí paměti zabírané objekty, na které odkazuje
- Zahrnuje pouze velikost objektu a jeho přímých atributů, nikoli objektů, které jsou dostupné prostřednictvím referencí
- Mělká velikost objektu je konstantní pro objekty stejného typu, protože závisí pouze na počtu atributů a jejich typu

Zadržená velikost (Retained size):
- Celková velikost paměti, kterou zabírá objekt a všechny objekty, které jsou dostupné pouze prostřednictvím tohoto objektu
- Zahrnuje velikost objektu a všechny jeho tranzitivně dostupné objekty prostřednictvím referencí
- Pokud by byl tento objekt uvolněn, zadržená velikost ukazuje, kolik paměti by bylo uvolněno

Význam mělké a zadržené velikosti při analýze paměti:
- Pomáhají identifikovat úniky paměti (memory leaks) a nadměrné využití paměti v aplikacích
- Umožňují vývojářům zjistit, které objekty nebo části kódu nejvíce přispívají k celkovému využití paměti
- Poskytují informace, které mohou vést k optimalizaci kódu a efektivnějšímu využití paměti

## Únik paměti (Memory leak):

- Problém, když program nepřestává alokovat paměť, aniž by ji následně správně uvolnil, což vede ke zvýšenému využití paměti
- Může vést k degradaci výkonu, nestabilitě nebo selhání aplikace
- Často způsoben chybami v kódu, kdy programátor zapomene uvolnit alokovanou paměť nebo se objeví cyklické reference, které brání automatickému uvolňování paměti (např. v jazyce Java s garbage collectorem)

Příčiny úniků paměti:
1. Nesprávné uvolňování paměti: Programátor alokuje paměť, ale zapomene ji uvolnit
2. Cyklické reference: Dva nebo více objektů si navzájem udržují reference, což brání jejich automatickému uvolnění
3. Statické proměnné: Proměnné, které zůstávají v paměti po celou dobu běhu programu, a které mohou neúmyslně udržovat reference na objekty

Detekce a řešení úniků paměti:

- Použití nástrojů pro statickou a dynamickou analýzu paměti k identifikaci potenciálních úniků paměti a zlepšení kvality kódu
- Revize kódu, aby se zajistilo správné uvolňování paměti a předešlo se cyklickým referencím
- V případě jazyků s garbage collectorem je důležité porozumět jeho chování a mechanismům uvolňování paměti, aby se předešlo neúmyslným únikům paměti

## Datové struktury

- Způsob organizace, správy a ukládání dat, který umožňuje efektivní přístup a modifikaci dat
- Každá datová struktura má své vlastnosti a využití, které ji činí vhodnou pro konkrétní typ úlohy
- Základní datové struktury zahrnují pole, spojové seznamy, zásobníky, fronty, stromy a grafy

1. Pole (Array):
   - Statická datová struktura s pevnou velikostí
   - Umožňuje rychlý přístup k prvku na základě indexu
   - Nevýhoda: neměnná velikost, která může vést k neefektivnímu využití paměti

2. Spojový seznam (Linked list):
   - Dynamická datová struktura, která se skládá z uzlů obsahujících data a odkaz na další uzel v seznamu
   - Umožňuje snadné vkládání a mazání prvků bez nutnosti přesunu ostatních prvků
   - Nevýhoda: pomalejší přístup k prvkům, protože je nutné projít seznam od začátku

3. Zásobník (Stack):
   - Lineární datová struktura, která pracuje na principu LIFO (Last In, First Out)
   - Umožňuje přidávání a odebírání prvků pouze z vrcholu zásobníku
   - Vhodné pro úlohy, které vyžadují rekurzi nebo zpětné sledování (backtracking)

4. Fronta (Queue):
   - Lineární datová struktura, která pracuje na principu FIFO (First In, First Out)
   - Umožňuje přidávání prvků na konec fronty a odebírání z jejího začátku
   - Vhodné pro úlohy, které vyžadují sekvenční zpracování dat

5. Strom (Tree):
   - Hierarchická datová struktura, která se skládá z uzlů propojených hranami
   - Umožňuje efektivní vyhledávání, vkládání a mazání prvků v závislosti na konkrétním typu stromu (binární strom, AVL strom, B-strom, atd.)
   - Vhodné pro úlohy, které vyžadují hierarchickou organizaci dat

6. Graf (Graph):
   - Datová struktura, která se skládá z uzlů (vrcholů) a hran mezi nimi
   - Umožňuje reprezentovat složité vztahy mezi objekty
   - Vhodné pro

## Java primitivní typy a objekty:

Primitivní typy:

- Základní datové typy přímo zabudované do jazyka Java
- Zahrnují celá čísla, desetinná čísla, znaky a logické hodnoty
- Ukládány na zásobníku (stack) a předávány hodnotou
- Primitivní typy v Javě zahrnují: `byte`, `short`, `int`, `long`, `float`, `double`, `char`, `boolean`

Objekty:

- Instance tříd definovaných v Javě nebo vlastních tříd vytvořených programátorem
- Ukládány na haldě (heap) a předávány referencí
- Objekty zahrnují všechny neprimitivní datové typy, jako jsou třídy, pole, kolekce a také tzv. "wrapper" třídy pro primitivní typy (např. `Integer`, `Double`, `Character`, `Boolean`)
- Každý objekt je implicitně odvozen od třídy `Object`, která poskytuje základní metody pro všechny objekty

Rozdíly mezi primitivními typy a objekty:
1. Ukládání: Primitivní typy jsou ukládány na zásobníku, zatímco objekty na haldě
2. Předávání: Primitivní typy jsou předávány hodnotou, objekty referencí
3. Výchozí hodnoty: Primitivní typy mají výchozí hodnoty (např. 0 pro `int`, `false` pro `boolean`), zatímco objekty mají výchozí hodnotu `null`
4. Metody: Objekty mohou mít metody a být součástí dědičnosti, primitivní typy nemají metody ani dědičnost
5. Wrapper třídy: Pro každý primitivní typ existuje "wrapper" třída, která umožňuje pracovat s primitivním typem jako s objektem (např. `Integer` pro `int`, `Double` pro `double`)

## Auto-boxing a unboxing:

Auto-boxing:

- Automatický proces převodu primitivního typu na jeho odpovídající "wrapper" třídu (objektový typ)
- Java kompilátor provádí auto-boxing implicitně, když je to nutné
- Příklad: Přiřazení primitivního typu `int` do objektového typu `Integer`

Unboxing:

- Automatický proces převodu "wrapper" třídy (objektového typu) na její odpovídající primitivní typ
- Java kompilátor provádí unboxing implicitně, když je to nutné
- Příklad: Přiřazení objektového typu `Integer` do primitivního typu `int`

## Efektivita paměti složitých datových struktur:

Efektivita paměti datových struktur závisí na:

1. Režii paměti: Každá datová struktura vyžaduje určité množství paměti pro uložení dodatečných informací, jako jsou odkazy, ukazatele nebo metadata.
2. Pevnosti velikosti: Některé datové struktury mají pevnou velikost, zatímco jiné mohou být dynamicky zvětšovány nebo zmenšovány podle potřeby.
3. Vnitřní fragmentace: Vnitřní fragmentace nastává, když datová struktura má nevyužité části paměti, které nelze přiřadit jiným objektům.

Příklady efektivity paměti některých složitých datových struktur:

1. Binární vyhledávací strom (Binary Search Tree):
   - Efektivní v případě, že je strom vyvážený
   - Má režii paměti z důvodu ukládání odkazů na levý a pravý potomek pro každý uzel
   - Může mít neefektivní využití paměti, pokud je strom silně nevyvážený

2. Hash tabulka (Hash Table):
   - Má režii paměti pro ukládání ukazatelů na prvky a pro správu kolizí
   - Při správně nastavené velikosti tabulky a vhodné hashovací funkci může být efektivní z hlediska paměti
   - Vnitřní fragmentace nastává, když je velikost tabulky příliš velká nebo malá vzhledem k počtu prvků

3. Grafová reprezentace (Graph Representation):
   - Matice sousednosti: Má režii paměti kvůli ukládání celé matice, i když je graf řídký (má málo hran)
   - Seznam sousednosti: Má menší režii paměti než matice sousednosti, ale vyžaduje ukládání odkazů na seznamy sousedů pro každý vrchol
   - Efektivita paměti závisí na hustotě grafu a způsobu reprezentace

Optimalizace efektivity paměti:

- Výběr vhodné datové struktury pro konkrétní problém, která minimalizuje režii paměti a vnitřní fragmentaci
- V případě dynamických datových struktur správně nastavit velikost a strategii zvětšování/zmenšování, aby se minimalizovala fragmentace a režie paměti
- Použití kompresních technik pro snížení paměťových nároků, pokud je to vhodné (např. komprese trie stromu)
- Využití cache a paměťových návrhových vzorů pro zlepšení výkonu a efektivity paměti (např. LRU cache)
- Provést analýzu paměti a ladění, aby se identifikovaly a odstranily úniky paměti nebo neefektivní využití paměti
- Použití slabých referencí, soft referencí nebo phantom referencí pro zlepšení správy paměti a zamezení úniků paměti v Javě
- V případě, že je to možné, sdílet části dat mezi různými datovými strukturami nebo instancemi, aby se snížila režie paměti (např. internování řetězců v Javě)


Při návrhu a implementaci složitých datových struktur je důležité najít rovnováhu mezi efektivitou paměti, výkonem a čitelností kódu. Vybraná datová struktura by měla být vhodná pro konkrétní problém, snadno použitelná a rozšiřitelná a současně co nejméně náročná na paměť.

## Kolekce pro výkon:

Výběr správné kolekce pro výkon závisí na požadavcích na časovou složitost a paměťovou efektivitu konkrétního problému. Některé běžné kolekce v Javě a jejich výkonnostní charakteristiky:

1. ArrayList:
   - Rychlý přístup k prvkům pomocí indexu (O(1))
   - Pomalejší přidávání a odebírání prvků uprostřed seznamu (O(n))
   - Dynamicky se zvětšuje, když je kapacita překročena

2. LinkedList:
   - Rychlé přidávání a odebírání prvků na začátku a konci seznamu (O(1))
   - Pomalejší přístup k prvkům pomocí indexu (O(n))
   - Vyšší režie paměti kvůli ukládání odkazů na předchozí a následující prvky

3. HashSet:
   - Rychlé přidávání, odebírání a vyhledávání prvků (průměrně O(1))
   - Nepodporuje žádné pořadí prvků
   - Vyšší režie paměti než ArrayList, ale nižší než LinkedList

4. TreeSet:
   - Rychlé přidávání, odebírání a vyhledávání prvků (O(log n))
   - Udržuje prvky seřazené podle jejich přirozeného řazení nebo podle komparátoru
   - Vyšší režie paměti než HashSet

5. HashMap:
   - Rychlý přístup, přidávání a odebírání klíč-hodnota párů (průměrně O(1))
   - Nepodporuje žádné pořadí klíčů ani hodnot
   - Vyšší režie paměti než ArrayList, ale nižší než LinkedList

6. TreeMap:
   - Rychlý přístup, přidávání a odebírání klíč-hodnota párů (O(log n))
   - Udržuje klíče seřazené podle jejich přirozeného řazení nebo podle komparátoru
   - Vyšší režie paměti než HashMap

Při výběru kolekce pro výkon zvažte následující faktory:

1. Požadovaná časová složitost operací (přístup, přidávání, odebírání, vyhledávání)
2. Pořadí prvků (potřeba udržovat prvky seřazené nebo ne)
3. Paměťová efektivita (režie paměti a dynamické zvětšování/zmenšování)
4. Podpora pro konkurenci a synchronizaci (např. ConcurrentHashMap pro bezpečné použití ve vícevláknovém prostředí)

## Typově specifické kolekce:

Typově specifické kolekce jsou kolekce, které jsou navrženy pro ukládání primitivních datových typů nebo konkrétních tříd. Použití těchto kolekcí může zlepšit výkon a snížit režii paměti, protože se eliminuje potřeba autoboxingu a unboxingu.

Některé příklady typově specifických kolekcí:

1. Trove knihovna (Java):
   - Poskytuje kolekce pro primitivní typy, jako jsou TIntArrayList, TDoubleHashSet, TObjectIntHashMap atd.
   - Nabízí nižší režii paměti a rychlejší operace než standardní Java kolekce

2. FastUtil knihovna (Java):
   - Poskytuje kolekce pro primitivní typy, jako jsou LongArrayList, Int2ObjectOpenHashMap, DoubleLinkedOpenHashSet atd.
   - Nabízí nízkoúrovňové kolekce pro rychlý přístup a manipulaci s daty
   - Rychlejší než standardní Java kolekce a podporuje vysokou kompresi dat

3. Apache Commons Primitives (Java):
   - Poskytuje kolekce pro primitivní typy, jako jsou IntList, DoubleStack, ObjectIntMap atd.
   - Snadné použití a integrace se standardními Java kolekcemi

4. Eclipse Collections (Java):
   - Poskytuje kolekce pro primitivní typy i objekty, jako jsou IntArrayList, LongHashSet, MutableObjectIntMap atd.
   - Bohatá API pro práci s daty a pokročilé funkce, jako jsou paralelní zpracování, lazy evaluace, atd.

5. C++ Standard Template Library (STL):
   - Poskytuje kolekce pro primitivní typy i třídy, jako jsou vector, list, set, map, atd.
   - Přizpůsobitelné a rozšiřitelné pomocí šablon a vlastních komparátorů nebo alokátorů

Při výběru typově specifických kolekcí zvažte následující faktory:

1. Výkon: Typově specifické kolekce mohou poskytnout rychlejší operace a nižší režii paměti než obecné kolekce
2. Integrace: Zkontrolujte, jak snadno lze typově specifickou kolekci integrovat do vaší aplikace a jak dobře spolupracuje se standardními kolekcemi nebo knihovnami
3. Kompatibilita: Ujistěte se, že typově specifická kolekce je kompatibilní s vaší verzí jazyka a platformy
4. Podpora a údržba: Zvažte úroveň podpory a údržby pos

## Otevřené adresování hashování:

Otevřené adresování hashování je metoda řešení kolizí v hash tabulkách, která nevyžaduje použití externích datových struktur (např. seznamů) pro ukládání prvků s kolizí. Místo toho jsou všechny prvky uloženy přímo v hash tabulce. 

Klíčové vlastnosti otevřeného adresování hashování:

1. Kolize řešeny prostřednictvím sekvenčního hledání volného místa v hash tabulce
2. Různé metody pro hledání volného místa:
   - Lineární sondování: Při kolizi se postupně prochází následující pozice, dokud není nalezeno volné místo
   - Kvadratické sondování: Při kolizi se skáče na pozice s rostoucími kvadratickými intervaly, dokud není nalezeno volné místo
   - Dvojité hashování: Při kolizi se použije druhá hashovací funkce pro určení intervalu skoků, dokud není nalezeno volné místo
3. Prostorová efektivita: Otevřené adresování hashování může mít nižší režii paměti než hashování s řetězci, protože nevyžaduje externí datové struktury
4. Výkon: Otevřené adresování hashování může být rychlejší než hashování s řetězci, pokud je kolizí málo a tabulka má dostatečnou kapacitu
5. Nutnost udržovat nízký faktor zatížení (počet prvků vůči kapacitě tabulky) pro udržení dobrého výkonu

Při použití otevřeného adresování hashování je důležité zajistit, že hash tabulka má dostatečnou kapacitu a je pravidelně zvětšována nebo zmenšována podle počtu prvků. To pomáhá minimalizovat počet kolizí a udržet dobrou efektivitu vyhledávání, přidávání a odebírání prvků.

## Schémata řešení kolizí

Schémata řešení kolizí jsou metody, které se používají k řešení kolizí v hash tabulkách. Kolize nastávají, když dva různé prvky mají stejnou hash hodnotu nebo jsou mapovány na stejnou pozici v tabulce. Zde jsou některá základní schémata řešení kolizí:

1. Řetězení (Chaining):
   - Každá pozice v hash tabulce obsahuje ukazatel na externí datovou strukturu (např. spojový seznam nebo strom)
   - Při kolizi se nový prvek přidá do datové struktury spojené s danou pozicí
   - Výhody: Jednoduché řešení, které umožňuje vysoký faktor zatížení
   - Nevýhody: Vyžaduje více paměti pro externí datové struktury a může způsobit zpomalení při mnoha kolizích

2. Otevřené adresování (Open Addressing):
   - Všechny prvky jsou uloženy přímo v hash tabulce
   - Při kolizi se hledá volné místo v tabulce pomocí různých metod (např. lineární sondování, kvadratické sondování, dvojité hashování)
   - Výhody: Nižší režie paměti a může být rychlejší než řetězení, pokud je kolizí málo
   - Nevýhody: Nutnost udržovat nízký faktor zatížení a složitější řešení

3. Koalescentní hashování (Coalesced Hashing):
   - Kombinuje vlastnosti řetězení a otevřeného adresování
   - Při kolizi se nový prvek přidá na volné místo v tabulce a spojí se s předchozím prvkem v kolizním řetězci
   - Výhody: Lepší využití paměti než řetězení a může být rychlejší než otevřené adresování
   - Nevýhody: Složitější implementace a může být pomalejší než otevřené adresování při nízkém faktoru zatížení

4. Perfect hashing (Perfektní hashování):
   - Používá dvě úrovně hashovacích funkcí pro zajištění, že nebudou žádné kolize
   - První úroveň rozděluje prvky do skupin, druhá úroveň použije samostatnou hashovací funkci pro každou

## Bloom filters, complexity, false positives, Bloom filter extensions

Bloom filtry:

Bloom filtry jsou pravděpodobnostní datové struktury, které umožňují testování přítomnosti prvku v množině. Bloom filtry používají více hashovacích funkcí a bitové pole pro uložení informací o prvcích.

Složitost:

- Vkládání: O(k), kde k je počet hashovacích funkcí
- Hledání: O(k), kde k je počet hashovacích funkcí

Falešné pozitivy:

- Bloom filtry mohou vrátit falešné pozitivy (tvrdit, že prvek je v množině, i když tam není), ale nikdy nevracejí falešné negativy (tvrdit, že prvek není v množině, když tam je)
- Pravděpodobnost falešných pozitiv závisí na velikosti bitového pole, počtu hashovacích funkcí a počtu prvků v množině
- Pro zajištění nízké pravděpodobnosti falešných pozitiv je nutné správně naladit parametry Bloom filtru (velikost bitového pole a počet hashovacích funkcí)

Rozšíření Bloom filtrů:

1. Scalable Bloom Filters (Škálovatelné Bloom filtry):
   - Umožňují dynamicky přizpůsobovat velikost bitového pole a počet hashovacích funkcí podle počtu prvků v množině
   - Zajišťují konstantní pravděpodobnost falešných pozitiv při růstu množiny

2. Counting Bloom Filters (Počítací Bloom filtry):
   - Rozšiřují klasické Bloom filtry tím, že udržují počet výskytů prvku místo jednoduché přítomnosti
   - Umožňují přidávání i odebírání prvků, avšak za cenu vyšší režie paměti

3. Cuckoo Filters (Kukaččí filtry):
   - Vylepšení Bloom filtrů, které umožňují efektivnější práci s pamětí a poskytují lepší výkon pro testování přítomnosti prvku v množině
   - Používají kukaččí hashování pro řešení kolizí a udržují pouze část informací o prvku (např. fingerprint)

4. Invertible Bloom Lookup Tables (Invertibilní Bloom vyhledávací tabulky):
   - Rozšiřují Bloom filtry tím, že umožňují ukládat a získávat páry klíč-hodnota
   - Umožňují pokročilé operace, jako je sjednocení, průnik a rozdíl mezi množinami klíčů a hodnot
   - Využívají lineární sondování a kompresi dat pro efektivní využití paměti a rychlé vyhledávání 
  
5. Space-saving Bloom Filters (Úsporné Bloom filtry):
   - Optimalizují paměťovou náročnost Bloom filtrů tím, že dynamicky přizpůsobují velikost bitového pole a počet hashovacích funkcí
   - Využívají metody pro odhad pravděpodobnosti falešných pozitiv a minimalizují paměťovou režii při udržení požadované úrovně přesnosti

6. DLeft Counting Bloom Filters (DLeft Počítací Bloom filtry):
   - Kombinují vlastnosti DLeft hashování a počítacích Bloom filtrů pro efektivní ukládání a vyhledávání páry klíč-hodnota
   - Umožňují přidávání, odebírání a aktualizaci prvků s nízkou pravděpodobností falešných pozitiv a efektivním využitím paměti

7. Layered Bloom Filters (Vrstvené Bloom filtry):
   - Využívají více vrstev Bloom filtrů s různými parametry pro rychlé vyhledávání a eliminaci falešných pozitiv
   - Umožňují postupně zvyšovat přesnost vyhledávání při zachování rychlosti a efektivnosti paměti

Tyto rozšíření Bloom filtrů řeší různé úkoly a výzvy spojené s testováním přítomnosti prvku v množině, přičemž každé rozšíření se zaměřuje na konkrétní aspekt, jako je škálovatelnost, dynamické přidávání a odebírání prvků, efektivita paměti nebo podpora pro práci s páry klíč-hodnota.

## Reference types - weak, soft, phantom

1. Silné reference (Strong references):
   - Běžné reference, které používáme při práci s objekty
   - Pokud je objekt dosažitelný přes silnou referenci, nebude uvolněn garbage collectorem

2. Slabé reference (Weak references):
   - Vytváříme je pomocí třídy `java.lang.ref.WeakReference`
   - Pokud je objekt dosažitelný pouze přes slabé reference, může být kdykoliv uvolněn garbage collectorem
   - Často používány pro implementaci cache, která se automaticky uvolní při nedostatku paměti

3. Měkké reference (Soft references):
   - Vytváříme je pomocí třídy `java.lang.ref.SoftReference`
   - Pokud je objekt dosažitelný pouze přes měkké reference, může být uvolněn garbage collectorem, ale pouze pokud je potřeba uvolnit paměť
   - Užitečné pro implementaci cache, která se udržuje v paměti, dokud není potřeba uvolnit prostředky

4. Fantomové reference (Phantom references):
   - Vytváříme je pomocí třídy `java.lang.ref.PhantomReference`
   - Neslouží k přístupu k objektu, ale pouze k zaznamenání, že byl objekt uvolněn garbage collectorem
   - Užitečné pro sledování životního cyklu objektů a provádění úklidu po uvolnění objektu

Tyto různé typy referencí nám umožňují pracovat s objekty v Javě různými způsoby a ovlivňovat chování garbage collectoru při uvolňování paměti. Slabé, měkké a fantomové reference nám umožňují vytvářet pokročilé datové struktury a algoritmy, které pracují efektivně s omezenými zdroji a reagují na potřeby aplikace.

## Alokace objektů v JVM:

1. Mladá generace (Young Generation):
   - Většina objektů je alokována v mladé generaci
   - Mladá generace se dělí na tři části:
     - Eden: místo, kde jsou všechny nové objekty alokovány
     - Survivor 1 (S0) a Survivor 2 (S1): slouží k ukládání objektů, které přežily garbage collection v Eden prostoru

2. Alokace objektu:
   - Objekt je nejprve alokován v Eden prostoru
   - Pokud Eden prostor dosáhne kapacity, spustí se garbage collection (tzv. minor GC) pro mladou generaci
   - Objekty, které přežijí minor GC, jsou přesunuty do jednoho z Survivor prostorů (S0 nebo S1)

3. Promoci objektu do staré generace:
   - Pokud objekt přežije určitý počet minor GC (záleží na nastavení JVM), je promován do staré generace
   - Stará generace obsahuje objekty, které přežily více garbage collection a jsou pravděpodobněji dlouhodobě používány

4. Alokace velkých objektů:
   - Velké objekty, které nemohou být alokovány v mladé generace, jsou přímo alokovány v staré generaci

5. Garbage collection pro starou generaci:
   - Pokud stará generace dosáhne kapacity, spustí se garbage collection (tzv. major GC nebo full GC) pro celou heap
   - Major GC je náročnější na výkon a trvá déle než minor GC

Alokace objektů v JVM je optimalizována pro efektivní správu paměti a rychlé uvolňování krátkodobě žijících objektů. Garbage collector a generace paměti pomáhají minimalizovat dopad na výkon při uvolňování paměti.

## Thread-Local Allocation Buffers (TLAB)

1. Co je TLAB?
   - TLAB je část paměti Eden prostoru v mladé generaci, která je vyhrazena pro alokaci objektů jednoho konkrétního vlákna
   - Každé vlákno má svůj vlastní TLAB, což umožňuje alokovat objekty rychleji bez nutnosti synchronizace mezi vlákny

2. Výhody TLAB:
   - Snížení režie spojené s synchronizací vláken při alokaci objektů
   - Rychlejší alokace objektů, protože každé vlákno může alokovat objekty ve svém TLAB bez čekání na ostatní vlákna
   - Zlepšení výkonu aplikací s vysokou mírou paralelismu a vytvářením objektů

3. Jak TLAB funguje?
   - Při inicializaci JVM se pro každé vlákno vytvoří TLAB v Eden prostoru
   - Každé vlákno alokuje objekty pouze ve svém TLAB
   - Pokud je TLAB jednoho vlákna plný, může být přidělena nová část paměti z Eden prostoru, nebo se může spustit garbage collection

4. Nastavení a ladění TLAB:
   - Velikost TLAB může být nastavena pomocí JVM parametrů, např. `-XX:TLABSize=<velikost>`
   - Pro ladění TLAB lze použít JVM parametry, např. `-XX:+PrintTLAB` pro výpis informací o TLAB do logu

TLAB zvyšuje výkon JVM tím, že minimalizuje režii spojenou s alokací objektů v paralelním prostředí. Tím se zlepšuje celková efektivita paměti a výkon aplikací s vysokou mírou vytváření objektů.

## Analýza úniku objektů (Object Escape Analysis):

1. Co je analýza úniku objektů?
   - Optimalizační technika používaná JVM pro identifikaci objektů, které neuniknou z aktuálního kontextu metody nebo vlákna
   - Pokud objekt neunikne, může JVM optimalizovat jeho alokaci a synchronizaci, což zlepšuje výkon aplikace

2. Výhody analýzy úniku objektů:
   - Snížení režie spojené s alokací objektů na haldě
   - Odstranění zbytečných synchronizací, které nejsou potřeba pro objekty, které neuniknou z aktuálního kontextu
   - Možnost alokovat objekty na zásobníku místo na haldě, což zlepšuje výkon a zjednodušuje práci garbage collectoru

3. Jak analýza úniku objektů funguje?
   - JVM analyzuje kód aplikace za běhu nebo při kompilaci a identifikuje objekty, které neuniknou z aktuálního kontextu metody nebo vlákna
   - Pokud objekt neunikne, JVM může provést následující optimalizace:
     - Alokace objektu na zásobníku místo na haldě
     - Odstranění zbytečných synchronizací na objektu
     - Optimalizace práce garbage collectoru

4. Nastavení a ladění analýzy úniku objektů:
   - Analýza úniku objektů je ve většině JVM aktivována automaticky
   - Pro ladění analýzy úniku objektů lze použít JVM parametry, např. `-XX:+DoEscapeAnalysis` pro zapnutí analýzy úniku objektů

Analýza úniku objektů je důležitá optimalizační technika, která zlepšuje výkon a efektivitu paměti aplikací. Pomáhá JVM identifikovat objekty, které neuniknou z aktuálního kontextu, a provádět optimalizace, které snižují režii spojenou s alokací objektů a synchronizací.


## Lokalita dat (Data Locality):

1. Co je lokalita dat?
   - Lokalita dat se týká organizace dat v paměti tak, aby byla přístupná rychle a efektivně
   - Zaměřuje se na způsob, jakým jsou data uložena a uspořádána v paměti, aby byla minimalizována doba přístupu a režie
   - Existují dva druhy lokality dat: lokalita v čase a lokalita v prostoru

2. Lokalita v čase (Temporal Locality):
   - Pokud je prvek použit, je pravděpodobné, že bude opět použit v blízké budoucnosti
   - Optimalizace: ukládání často používaných dat v rychlých cache pamětech

3. Lokalita v prostoru (Spatial Locality):
   - Pokud je prvek použit, je pravděpodobné, že budou použity i jeho sousední prvky v blízké budoucnosti
   - Optimalizace: načítání bloků dat do cache paměti, které obsahují i sousední prvky

4. Výhody lokality dat:
   - Zlepšení výkonu aplikace díky rychlejšímu přístupu k datům
   - Efektivnější využití cache paměti a minimalizace cache miss
   - Menší režie spojená s načítáním a ukládáním dat

5. Aplikace lokality dat v programování:
   - Použití kontiguálních datových struktur (např. pole) místo spojových datových struktur (např. spojový seznam)
   - Uspořádání dat v paměti podle přístupových vzorů (např. skupinování souvisejících dat dohromady)
   - Optimalizace smyček a algoritmů pro využití lokality dat (např. procházení pole po řádcích nebo sloupcích)

Lokalita dat je klíčovým aspektem optimalizace výkonu aplikací. Správné uspořádání a organizace dat v paměti může významně zlepšit výkon aplikace a minimalizovat režii spojenou s načítáním a ukládáním dat.

## Nerovnoměrná alokace paměti (Non-Uniform Memory Allocation, NUMA):

1. Co je nerovnoměrná alokace paměti (NUMA)?
   - NUMA je architektura paměti, která se používá v multiprocesorových systémech, kde je přístup k paměti různě rychlý v závislosti na vzdálenosti mezi procesorem a pamětí
   - Cílem NUMA je zlepšit výkon a škálovatelnost systému tím, že se sníží režie spojená s přístupem k paměti

2. Jak NUMA funguje?
   - V NUMA architektuře je paměť rozdělena do několika menších paměťových uzlů, které jsou připojeny k procesorům
   - Každý procesor má rychlejší přístup k paměti ve svém vlastním uzlu a pomalejší přístup k paměti v ostatních uzlech
   - Při alokaci paměti se pokouší NUMA alokovat paměť v uzlu, který je nejblíže procesoru, který bude paměť používat

3. Výhody NUMA:
   - Zlepšení výkonu a škálovatelnosti multiprocesorových systémů díky rychlejšímu přístupu k lokální paměti
   - Menší režie spojená s přístupem k paměti, protože paměťová komunikace probíhá většinou uvnitř uzlů
   - Možnost efektivnějšího využití cache paměti

4. Nevýhody NUMA:
   - Složitější správa paměti a plánování procesů
   - Potenciální problémy s latencí a propustností při přístupu k vzdálené paměti
   - Vyšší nároky na hardware a softwarovou podporu

5. Jak optimalizovat aplikace pro NUMA?
   - Správné rozdělení práce mezi procesory a jejich lokálními paměťovými uzly
   - Využití NUMA-optimálních knihoven a funkcí pro správu paměti
   - Monitorování a ladění výkonu aplikace v NUMA systémech

Nerovnoměrná alokace paměti (NUMA) je architektura paměti používaná v multiprocesorových systémech pro zlepšení výkonu a škálovatelnosti. Správné využití NUMA může významně zlepšit výkon aplikace v multiprocesorových prostředích.

## OSI model (Open Systems Interconnection):

1. Co je OSI model?
   - OSI model je konceptuální rámec, který popisuje, jak různé vrstvy komunikačního systému spolupracují při přenosu dat mezi síťovými zařízeními
   - Model se skládá ze 7 vrstev, které definují různé úrovně abstrakce a funkcí komunikačního procesu

2. Seznam vrstev OSI modelu:
   1. Fyzická vrstva (Physical Layer)
   2. Linková vrstva (Data Link Layer)
   3. Síťová vrstva (Network Layer)
   4. Transportní vrstva (Transport Layer)
   5. Relační vrstva (Session Layer)
   6. Prezentační vrstva (Presentation Layer)
   7. Aplikační vrstva (Application Layer)

3. Popis vrstev OSI modelu:
   1. Fyzická vrstva:
      - Zajišťuje přenos a přijímání bitů přes fyzické médium (např. kabel, rádiové vlny)
      - Definuje fyzické charakteristiky konektorů, kabelů a signálů

   2. Linková vrstva:
      - Řeší přenos datových rámců mezi sousedními uzly v síti
      - Zajišťuje kontrolu chyb a řízení toku dat

   3. Síťová vrstva:
      - Zajišťuje směrování a přeposílání datových paketů mezi různými sítěmi
      - Spravuje adresování a segmentaci dat

   4. Transportní vrstva:
      - Zajišťuje spolehlivý přenos dat mezi koncovými uzly
      - Řídí tok dat, kontrolu chyb a obnovu ztracených dat

   5. Relační vrstva:
      - Řídí spojení mezi aplikacemi a zajišťuje jejich správnou funkci
      - Udržuje a ukončuje komunikační relace

   6. Prezentační vrstva:
      - Zajišťuje převod dat mezi aplikacemi a síťovým formátem
      - Řídí kódování, kompresi a šifrování dat

   7. Aplikační vrstva:
      - Poskytuje rozhraní mezi aplikacemi a komunikačními službami
      - Zajišťuje přístup k síťovým službám, jako jsou e-mail, webové stránky a databáze

OSI model je důležitým konceptem v oblasti počítačových sítí, který pomáhá porozumět základním principům komunikace mezi síťovými zař

## Problém C10K

1. Co je problém C10K?
   - Problém C10K je výkonový problém spojený se schopností serveru zvládat více než 10 000 současných síťových spojení
   - Tento problém byl poprvé popsán v roce 1999 a odráží výzvy spojené s růstem počtu uživatelů a potřeby serverů zvládat více spojení

2. Příčiny problému C10K:
   - Omezení výkonu způsobená tradičními síťovými modely (jako je model jeden proces/jeden vlákno na jedno spojení)
   - Vysoká režie spojená s vytvářením a zrušením vláken nebo procesů pro každé spojení
   - Nedostatek operačního systému a hardwarové podpory pro vysoký počet současných spojení

3. Řešení problému C10K:
   - Použití vícevláknových nebo asynchronních modelů serverů, které mohou zpracovávat více spojení pomocí méně zdrojů
   - Využití funkce epoll (Linux) nebo kqueue (BSD, macOS) pro efektivní sledování stavu více síťových spojení
   - Použití non-blocking I/O operací, které umožňují serveru pokračovat v práci, zatímco čeká na dokončení I/O operace
   - Optimalizace operačního systému a hardwaru pro zvýšení propustnosti a snížení režie spojené s přenosem dat

4. Význam řešení problému C10K:
   - Zlepšení výkonu serverů a schopnosti zvládat vyšší zátěž
   - Zajištění škálovatelnosti serverů, které mohou růst spolu s počtem uživatelů a potřebami aplikací
   - Umožnění efektivnějšího využití zdrojů serverů, což vede ke snížení nákladů na provoz a správu

Problém C10K odráží výzvy spojené se zvládáním velkého počtu současných síťových spojení na serverech. Řešení tohoto problému zahrnuje použití vícevláknových, asynchronních nebo non-blocking modelů serverů, optimalizaci operačního systému a hardwaru a využití pokročilých technologií pro sledování a správu síťových spojení.


## Blocking a non-blocking I/O (vstup/výstup):

1. Co je blocking I/O?
   - Blocking I/O je metoda vstupu/výstupu, při které se vykonávání programu zastaví, dokud nebude dokončena I/O operace
   - Během čekání na dokončení I/O operace je proces nebo vlákno blokováno a nemůže vykonávat žádné další úkoly

2. Co je non-blocking I/O?
   - Non-blocking I/O je metoda vstupu/výstupu, při které se vykonávání programu nepozastavuje, dokud nebude dokončena I/O operace
   - Místo čekání na dokončení I/O operace může proces nebo vlákno pokračovat v jiných úkolech a zpět ke zpracování I/O operace se vrátí, až bude hotova

3. Porovnání blocking a non-blocking I/O:
   - Výkon: Non-blocking I/O může zlepšit výkon aplikací tím, že minimalizuje čas strávený čekáním na dokončení I/O operací
   - Složitost: Blocking I/O je jednodušší na implementaci a pochopení, zatímco non-blocking I/O vyžaduje více pozornosti k správě asynchronních operací
   - Vhodnost: Blocking I/O je vhodný pro aplikace, kde je čekání na I/O operace přijatelné nebo očekávané, zatímco non-blocking I/O je vhodný pro aplikace, které vyžadují vysokou propustnost a odezvu

4. Příklady použití blocking a non-blocking I/O:
   - Blocking I/O: Jednoduché servery, které obsluhují malý počet klientů nebo aplikace, které nevyžadují vysokou propustnost
   - Non-blocking I/O: Webové servery, databázové servery nebo aplikace, které obsluhují velké množství současných spojení nebo vyžadují rychlou odezvu

Blocking a non-blocking I/O představují dva různé přístupy k vstupu/výstupu v aplikacích. Blocking I/O je jednodušší na implementaci, ale může vést k nižšímu výkonu. Non-blocking I/O poskytuje lepší výkon, ale vyžaduje více pozornosti k správě asynchronních operací.

## Vícevláknový server (Threading server):

1. Co je vícevláknový server?
   - Vícevláknový server je typ serveru, který používá více vláken pro obsluhu více klientů nebo požadavků současně
   - Každé vlákno zpracovává jeden nebo více klientů nezávisle na ostatních vláknech

2. Výhody vícevláknového serveru:
   - Lepší využití zdrojů: Vícevláknový server může efektivněji využívat zdroje procesoru a paměti, což zlepšuje výkon a propustnost
   - Rychlejší odezva: Vícevláknový server může poskytovat rychlejší odezvu na požadavky klientů, protože jednotlivá vlákna mohou pracovat paralelně a zpracovávat více požadavků současně
   - Škálovatelnost: Vícevláknový server může lépe zvládat zvýšenou zátěž, protože může vytvářet a zrušit vlákna podle potřeby

3. Nevýhody vícevláknového serveru:
   - Složitost: Vícevláknový server může být složitější na implementaci a správu, protože vyžaduje koordinaci a synchronizaci mezi vlákny
   - Režie: Vytváření a zrušení vláken může způsobit režii, která může snížit výkon serveru
   - Sdílené prostředky: Vlákna musí sdílet prostředky, jako je paměť a procesor, což může vést k problémům s výkonem a synchronizací

4. Použití vícevláknového serveru:
   - Vícevláknový server je vhodný pro aplikace, které vyžadují vysokou propustnost a rychlou odezvu, jako jsou webové servery, databázové servery nebo aplikace pro zpracování videa

Vícevláknový server představuje přístup k zpracování požadavků klientů, který umožňuje lepší využití zdrojů a rychlejší odezvu. Je vhodný pro aplikace, které vyžadují vysokou propustnost a rychlou odezvu, ale může být složitější na implementaci a správu než jednovláknové servery.

## Událostmi řízený server (Event-driven server):

1. Co je událostmi řízený server?
   - Událostmi řízený server je typ serveru, který zpracovává požadavky klientů na základě událostí, jako jsou příchozí data nebo změny stavu spojení
   - Server reaguje na události pomocí asynchronních I/O operací a zpracovává požadavky klientů bez potřeby vytvářet samostatná vlákna nebo procesy pro každé spojení

2. Výhody událostmi řízeného serveru:
   - Nižší režie: Událostmi řízený server má nižší režii než vícevláknový server, protože nepotřebuje vytvářet a zrušit vlákna pro každé spojení
   - Škálovatelnost: Událostmi řízený server může zvládat velký počet současných spojení s menšími nároky na systémové zdroje
   - Jednodušší koordinace: Událostmi řízený server může být jednodušší na koordinaci a správu než vícevláknový server, protože většina operací je asynchronní a nemusí být koordinována s ostatními vlákny

3. Nevýhody událostmi řízeného serveru:
   - Složitost: Událostmi řízený server může být složitější na implementaci, protože vyžaduje správu asynchronních událostí a I/O operací
   - Výkon: Událostmi řízený server může mít nižší výkon než vícevláknový server, pokud je zátěž serveru nevyvážená nebo pokud server musí provádět náročné výpočetní úkoly

4. Použití událostmi řízeného serveru:
   - Událostmi řízený server je vhodný pro aplikace, které potřebují zvládat velké množství současných spojení s nízkou režií, jako jsou webové servery, proxy servery nebo aplikace pro zpracování zpráv

Událostmi řízený server představuje přístup k zpracování požadavků klientů, který se zaměřuje na asynchronní I/O operace a reaguje na události, jako jsou příchozí data nebo změny stavu spojení. Je vhodný pro aplikace, které potřebují zvládat velké množství současných spo

## Event-based input/output approaches

Přístupy k událostmi řízenému vstupu/výstupu (Event-based input/output):

1. Co je událostmi řízený vstup/výstup (event-based I/O)?
   - Událostmi řízený vstup/výstup je asynchronní způsob zpracování I/O operací, který reaguje na události, jako jsou příchozí data nebo změny stavu spojení
   - Tento přístup umožňuje efektivně zpracovávat velké množství současných spojení s nízkou režií a vysokou propustností

2. Přístupy k událostmi řízenému vstupu/výstupu:

   a) Reactor pattern (Reaktor vzor):
      - Reaktor vzor je návrhový vzor, který řídí událostmi řízený vstup/výstup pomocí jednoho nebo více demultiplexorů událostí
      - Demultiplexor událostí sleduje události na více I/O zdrojích a spouští příslušné obslužné rutiny, které zpracovávají události
      - Reaktor vzor je vhodný pro aplikace s malým počtem současných spojení, které vyžadují rychlou odezvu na události

   b) Proactor pattern (Proaktor vzor):
      - Proaktor vzor je návrhový vzor, který řídí událostmi řízený vstup/výstup pomocí asynchronních I/O operací a plánovače událostí
      - Plánovač událostí zodpovídá za řízení a spouštění asynchronních I/O operací a obslužných rutin, které zpracovávají události
      - Proaktor vzor je vhodný pro aplikace s velkým počtem současných spojení, které vyžadují vysokou propustnost a efektivní využití systémových zdrojů

3. Porovnání událostmi řízených přístupů k vstupu/výstupu:
   - Reactor pattern:
      - Výhody: Jednodušší na implementaci, rychlá odezva na události
      - Nevýhody: Nižší propustnost při velkém počtu současných spojení, vyšší režie při demultiplexingu událostí
   - Proactor pattern:
      - Výhody: Vysoká propustnost, efektivní využití systémových zdrojů, snížená režie při zpracování událostí
      - Nevýhody: Složitější na implementaci, může vyžadovat specifickou podporu asynchronních I/O operací ze strany operačního systému

4. Použití událostmi řízených přístupů k vstupu/výstupu:
   - Událostmi řízené přístupy k vstupu/výstupu se používají v širokém spektru aplikací, které vyžadují efektivní zpracování velkého počtu současných spojení, jako jsou webové servery, proxy servery, aplikace pro zpracování zpráv nebo databázové servery

Událostmi řízené přístupy k vstupu/výstupu, jako jsou Reactor a Proactor vzory, umožňují efektivně zpracovávat velké množství současných spojení s nízkou režií a vysokou propustností. Tyto přístupy se používají v širokém spektru aplikací, které vyžadují efektivní zpracování velkého počtu současných spojení, jako jsou webové servery, proxy servery, aplikace pro zpracování zpráv nebo databázové servery.

## Nativní buffery v JVM (Java Virtual Machine):

1. Co jsou nativní buffery?
   - Nativní buffery jsou oblasti paměti mimo Java heap, které slouží k ukládání a manipulaci s daty v rámci JVM
   - Tyto buffery mohou být přímo přístupné pro nativní kód a operační systém, což umožňuje rychlejší a efektivnější zpracování dat než při použití běžných Java objektů

2. Výhody nativních bufferů v JVM:
   - Rychlost: Nativní buffery umožňují rychlejší zpracování dat, protože nejsou omezeny Java garbage collector a nemusí být kopírovány mezi Java heap a nativní pamětí
   - Efektivita: Nativní buffery umožňují efektivnější využití systémových zdrojů, jako je paměť a I/O, protože mohou být přímo přístupné pro nativní kód a operační systém
   - Kompatibilita: Nativní buffery usnadňují interakci mezi Java kódem a nativními knihovnami nebo operačním systémem, což umožňuje vytvářet výkonnější a škálovatelnější aplikace

3. Použití nativních bufferů v JVM:
   - Nativní buffery se často používají v JVM pro zlepšení výkonu a efektivity aplikací, které pracují s velkým množstvím dat nebo potřebují přímý přístup k nativním knihovnám a operačnímu systému
   - Typické příklady zahrnují síťové I/O operace, grafické a multimediální aplikace, databázové servery nebo výkonnostně náročné výpočty

Nativní buffery v JVM umožňují rychlejší a efektivnější zpracování dat než při použití běžných Java objektů, protože nejsou omezeny Java garbage collector a mohou být přímo přístupné pro nativní kód a operační systém. Tyto buffery se často používají pro zlepšení výkonu a efektivity aplikací, které pracují s velkým množstvím dat nebo potřebují přímý přístup k nativním knihovnám a operačnímu systému.

## Kanály a selektory:

1. Co jsou kanály a selektory?
   - Kanály (Channels) jsou abstrakce, které umožňují efektivní a asynchronní komunikaci mezi Java kódem a I/O zdroji, jako jsou soubory, síťové sockety nebo datové proudy
   - Selektory (Selectors) jsou komponenty, které sledují a řídí události na více kanálech současně, což umožňuje efektivní zpracování událostí a multiplexing I/O operací

2. Výhody kanálů a selektorů:
   - Efektivita: Kanály a selektory umožňují efektivní využití systémových zdrojů, jako je paměť a I/O, protože umožňují asynchronní a událostmi řízený přístup k I/O zdrojům
   - Flexibilita: Kanály a selektory poskytují jednotné rozhraní pro různé typy I/O zdrojů, což usnadňuje vývoj a údržbu aplikací, které pracují s různými typy dat a komunikací
   - Škálovatelnost: Kanály a selektory umožňují efektivní zpracování velkého počtu současných spojení, což je užitečné pro aplikace, které vyžadují vysokou propustnost a nízkou latenci

3. Použití kanálů a selektorů v JVM:
   - Kanály a selektory se používají v širokém spektru aplikací, které vyžadují efektivní zpracování I/O operací a komunikace, jako jsou webové servery, proxy servery, aplikace pro zpracování zpráv nebo databázové servery
   - Kanály a selektory jsou součástí Java NIO (New Input/Output) knihovny, která poskytuje rozšířené a výkonné I/O funkce pro Java aplikace

Kanály a selektory jsou klíčovými komponentami Java NIO knihovny, které umožňují efektivní a asynchronní komunikaci mezi Java kódem a I/O zdroji. Tyto komponenty se používají v širokém spektru aplikací, které vyžadují efektivní zpracování I/O operací a komunikace, jako jsou webové servery, proxy servery, aplikace pro zpracování zpráv nebo databázové servery.

## Synchronizace v multithreadových programech (atomické operace, mutex, semafor, rw-lock, spinlock, RCU). Kdy použít který mechanismus? Výkonnostní úzká místa zmíněných mechanismů:

1. Atomické operace:
   - Použití: Malé, jednoduché a rychlé operace, které mají garantovat konzistenci mezi vlákny
   - Výkonnostní úzká místa: Omezená na jednoduché operace, může způsobit zpoždění v případě častých aktualizací dat

2. Mutex:
   - Použití: Vzájemné vyloučení přístupu k sdíleným zdrojům, vhodné pro krátké kritické sekce
   - Výkonnostní úzká místa: Může způsobit zpoždění, pokud je přístup k sdíleným zdrojům často blokován

3. Semafor:
   - Použití: Omezení počtu současně prováděných operací, například při omezení počtu současných spojení
   - Výkonnostní úzká místa: Může způsobit zpoždění v případě velkého počtu vláken čekajících na uvolnění semaforu

4. Rw-lock:
   - Použití: Oddělení čtecích a zapisovacích operací pro sdílené zdroje, vhodné pro situace s častými čtecími operacemi a méně častými zapisovacími operacemi
   - Výkonnostní úzká místa: Může způsobit zpoždění, pokud zapisovací operace často blokují čtecí operace

5. Spinlock:
   - Použití: Vzájemné vyloučení přístupu k sdíleným zdrojům, vhodné pro velmi krátké kritické sekce, kde je očekávání na uvolnění zámku krátké
   - Výkonnostní úzká místa: Může způsobit zvýšení vytížení procesoru, pokud vlákna čekají na uvolnění zámku po delší dobu

6. RCU (Read-Copy-Update):
   - Použití: Synchronizace čtecích a zapisovacích operací pro sdílené zdroje bez použití zámků, vhodné pro situace s častými čtecími operacemi a méně častými zapisovacími operacemi
   - Výkonnostní úzká místa: Může způsobit zpoždění v případě častých zapisovacích operací nebo velkého množství vláken, kvůli nutnosti provádět čištění paměti a koordinaci mezi vlákny

Při výběru synchronizačního mechanismu je důležité zvážit následující faktory:

- Četnost a typ operací (čtení, zápis) prováděných na sdílených zdrojích
- Počet vláken, které přistupují k sdíleným zdrojům
- Očekávané doby čekání na zámky nebo jiné synchronizační mechanismy
- Důležitost výkonu a škálovatelnosti aplikace

Výběr vhodného synchronizačního mechanismu může mít významný dopad na výkon a škálovatelnost aplikace. Je důležité provádět testy a analýzu výkonu, aby bylo zajištěno, že zvolený mechanismus splňuje požadavky aplikace a nepředstavuje výkonnostní úzká místa.

## Synchronizace v "read-mostly workloads" (práce s převážně čtecími operacemi), výhody a nevýhody různých synchronizačních mechanismů:

1. Atomické operace:
   - Výhody: Rychlé, jednoduché a bez zámku
   - Nevýhody: Omezené na jednoduché operace, méně vhodné pro složitější sdílené struktury

2. Mutex:
   - Výhody: Zajišťuje vzájemné vyloučení přístupu k sdíleným zdrojům
   - Nevýhody: Může způsobit zpoždění, pokud je přístup k sdíleným zdrojům často blokován

3. Read-write lock (rw-lock):
   - Výhody: Umožňuje paralelní čtení, odděluje čtecí a zapisovací operace
   - Nevýhody: Může způsobit zpoždění, pokud zapisovací operace často blokují čtecí operace

4. RCU (Read-Copy-Update):
   - Výhody: Bez zámku, umožňuje efektivní čtení bez blokování
   - Nevýhody: Může způsobit zpoždění v případě častých zapisovacích operací, kvůli nutnosti provádět čištění paměti a koordinaci mezi vlákny

5. StampedLock:
   - Výhody: Podpora pro optimalizované čtení bez zámku, oddělení čtecích a zapisovacích operací
   - Nevýhody: Složitější použití, může způsobit zpoždění, pokud zapisovací operace často blokují čtecí operace

Pro read-mostly workloads, kde je většina operací čtecích a zapisovací operace jsou méně časté, jsou vhodné mechanismy, které minimalizují dopad zapisovacích operací na čtecí operace a umožňují efektivní paralelní čtení. Mezi takové mechanismy patří rw-lock, RCU a StampedLock.

Výběr vhodného synchronizačního mechanismu závisí na konkrétních požadavcích aplikace a na potřebě optimalizace výkonu a škálovatelnosti. Je důležité provádět testy a analýzu výkonu, aby bylo zajištěno, že zvolený mechanismus splňuje požadavky aplikace a nepředstavuje výkonnostní úzká místa.

## Cache-efektivní datové struktury a algoritmy (např. násobení matic):

Cache-efektivní datové struktury a algoritmy jsou navrženy tak, aby minimalizovaly přístupy k paměti a využily cache CPU co nejlépe. Příklady cache-efektivních datových struktur a algoritmů:

1. Cache-oblivious algoritmy:
   - Navrženy tak, aby efektivně využily cache bez znalosti velikosti cache nebo cache line
   - Příklad: Cache-oblivious násobení matic, které rozdělí matice na menší bloky a provádí násobení bloků s efektivním využitím cache

2. Cache-aware algoritmy:
   - Navrženy s vědomím velikosti cache a cache line, což umožňuje maximalizovat využití cache
   - Příklad: Cache-aware násobení matic, které rozdělí matice na bloky velikosti, která odpovídá velikosti cache, a násobí bloky efektivně

3. B-stromy:
   - Cache-efektivní stromová datová struktura, která má větší větve než binární stromy, což umožňuje efektivnější využití cache
   - Příklad: B-stromy se používají v databázových systémech a souborových systémech pro efektivní vyhledávání a manipulaci s daty

4. Bloom filtry:
   - Cache-efektivní datová struktura, která umožňuje rychlé a efektivní testování přítomnosti prvku v množině s malou paměťovou náročností
   - Příklad: Bloom filtry se používají pro rychlé vyhledávání v cache nebo pro detekci duplicitních dat

5. Compact hash tabulky:
   - Cache-efektivní varianta hash tabulek, která minimalizuje paměťovou náročnost a zlepšuje využití cache
   - Příklad: Compact hash tabulky se používají pro rychlé vyhledávání a ukládání dat s malou paměťovou náročností

Pro dosažení cache-efektivity je důležité brát v úvahu vlastnosti paměti cache, jako je velikost cache, cache line, asociativita a politika nahrazování. Cache-efektivní algoritmy a datové struktury mohou výrazně zlepšit výkon aplikace tím, že minimalizují přístupy k pomalejší hlavní paměti a maximalizují využití rychlé cache paměti.

## Zásady cache pamětí a různé druhy cache chyb:

Cache paměť je rychlá a menší paměť mezi CPU a hlavní pamětí (RAM), která zlepšuje výkon tím, že udržuje kopie často používaných dat z hlavní paměti. Cache paměť využívá vlastnosti prostorové a časové lokalitě přístupu k datům.

Různé druhy cache chyb (misses):

1. Compulsory miss (nevyhnutelná chyba):
   - Způsobena prvním přístupem k datům, která nejsou v cache
   - Nelze zcela eliminovat, může být minimalizováno efektivním přednačítáním dat do cache

2. Capacity miss (kapacitní chyba):
   - Způsobena omezenou kapacitou cache paměti, když je počet potřebných dat větší než velikost cache
   - Může být zlepšeno zvětšením cache nebo využitím cache-efektivních algoritmů a datových struktur

3. Conflict miss (konfliktní chyba):
   - Způsobena kolizemi v cache záznamech, kdy různá data mapují na stejnou pozici v cache
   - Může být zlepšeno zvýšením asociativity cache, použitím cache-oblivious nebo cache-aware algoritmů

4. Coherence miss (koherenční chyba):
   - Způsobena nekonzistencí mezi cache pamětí různých procesorů v multiprocesorovém systému
   - Může být zlepšeno použitím koherentních protokolů a správných synchronizačních mechanismů

Pro efektivní využití cache pamětí je důležité minimalizovat počet cache chyb a zohlednit vlastnosti cache, jako je velikost cache, cache line, asociativita a politika nahrazování. Cache-efektivní algoritmy a datové struktury mohou výrazně zlepšit výkon aplikace tím, že minimalizují přístupy k pomalejší hlavní paměti a maximalizují využití rychlé cache paměti.

## Self-evicting kód:

Self-evicting kód je kód, který je napsán tak, aby se záměrně vyhýbal využití cache paměti nebo z ní byl rychle vytlačen. Tento typ kódu může být užitečný v některých případech, například:

1. Pro zabezpečení:
   - Když chcete minimalizovat dobu, po kterou citlivá data zůstávají v cache paměti, a snížit tak riziko útoku, který by zneužil přístup k těmto datům (např. cache side-channel útoky)

2. Pro účely vyvažování zátěže:
   - Když chcete zajistit, že kritické části kódu nebudou vytlačeny z cache paměti méně důležitými částmi kódu, které by mohly vést k výkonnostním problémům

Pro napsání self-evicting kódu je třeba použít techniky, které záměrně zhoršují vlastnosti prostorové a časové lokalitě přístupu k datům a zabraňují jejich uchování v cache paměti. Některé z těchto technik mohou zahrnovat:

1. Použití nestandardních přístupových vzorů k datům
2. Záměrné prokládání přístupu k různým datovým oblastem, aby byla zvýšena pravděpodobnost vytlačení dat z cache
3. Použití technik, které ztěžují předpovědi větví, což zabraňuje efektivnímu přednačítání dat do cache

Je důležité si uvědomit, že self-evicting kód může mít negativní dopad na výkon aplikace v důsledku zvýšených přístupů k pomalejší hlavní paměti. Použití self-evicting kódu by mělo být pečlivě zváženo a použito pouze tam, kde je to opravdu nezbytné.

## False sharing - co to je a jak se s tím vypořádat?

False sharing je situace, kdy více vláken v multiprocesorovém nebo multicore systému nezávisle přistupuje k různým datovým položkám, které jsou umístěny ve stejném bloku cache (cache line). Tento přístup může způsobit nežádoucí invalidaci cache line a zvýšení komunikace mezi procesory nebo jádry, což má za následek výkonnostní problémy.

Jak se vypořádat s false sharingem:

1. Zarovnání dat: 
   - Zarovnejte často používaná data na hranice cache line, aby byla oddělena a nezpůsobovala false sharing. V některých jazycích (např. C/C++) lze použít direktivy pro zarovnání dat, jako je `alignas()`.

2. Padding (vyplnění):
   - Přidejte padding mezi datovými položkami, které jsou přístupné různými vlákny, aby byly umístěny ve vlastních cache lines. Padding může zahrnovat nevyužité proměnné nebo pole.

3. Oddělení dat:
   - Oddělte data, která jsou přístupná různými vlákny, do různých datových struktur nebo objektů, aby byla minimalizována pravděpodobnost false sharingu.

4. Thread-local storage (úložiště pro vlákna):
   - Pokud je to možné, použijte thread-local storage pro data, která jsou specifická pro jednotlivá vlákna. Tím se sníží potřeba sdílet data mezi vlákny a zároveň se minimalizuje false sharing.

5. Použití optimalizací kompilátoru:
   - Některé kompilátory mohou poskytovat optimalizace pro snížení false sharingu. Prozkoumejte možnosti optimalizace vašeho kompilátoru a zvažte jejich použití.

6. Profiling a analýza:
   - Použijte nástroje pro profiling a analýzu k identifikaci false sharingu ve vaší aplikaci. Tím získáte informace o kritických oblastech kódu, které mohou být zdrojem false sharingu a mohou být optimalizovány.

Při práci s false sharingem je důležité najít rovnováhu mezi snižováním false sharingu a zachováním paměťové efektivity, protože některé z těchto technik mohou zvýšit paměťovou náročnost aplikace.

## Profiling a optimalizace programů v kompilovaných jazycích (např. C/C++):

1. Profiling:
   - Profiling je proces sběru dat o výkonu a chování programu za účelem identifikace oblastí, které lze optimalizovat. Nástroje pro profiling v C/C++ mohou zahrnovat:
     - `gprof`: GNU profiler pro měření času stráveného v jednotlivých funkcích
     - `perf`: Nástroj pro profiling na úrovni jádra Linuxu
     - `Valgrind`: Nástroj pro analýzu paměti a profiling výkonu

2. Optimalizace kompilátoru:
   - Kompilátory jako GCC nebo Clang poskytují různé úrovně optimalizace, které lze nastavit pomocí přepínačů:
     - `-O0`: Žádná optimalizace (výchozí)
     - `-O1`: Optimalizace pro rychlost a velikost kódu
     - `-O2`: Optimalizace pro rychlost (bez zvýšení velikosti kódu)
     - `-O3`: Agresivní optimalizace pro rychlost (může zvýšit velikost kódu)
     - `-Os`: Optimalizace pro velikost kódu
     - `-Ofast`: Optimalizace pro nejvyšší rychlost (ignoruje striktní standardy)

3. Optimalizace kódu:
   - Ruční optimalizace kódu může zahrnovat následující techniky:
     - Smyčkové optimalizace: unrolling, fusion, či blocking
     - Minimalizace režie volání funkcí: inlining, tail call optimalizace
     - Optimalizace paměťového přístupu: zarovnání dat, cache-friendly algoritmy
     - Využití paralelismu: SIMD instrukce, vícevláknové programování
     - Snížení režie synchronizace: atomické operace, lock-free algoritmy

4. Analýza a ladění:
   - Analyzujte a laděte svůj kód za účelem identifikace a řešení výkonnostních problémů, např. pomocí následujících nástrojů:
     - `gdb`: GNU Debugger pro ladění programů
     - `strace`: Nástroj pro sledování systémových volání a signálů
     - `ltrace`: Nástroj pro sledování volání knihoven
     - `vtune`: Profiler a ladící nástroj od Intelu

Při provádění optimalizací je důležité najít rovnováhu mezi výkonem, čitelností kódu a přenositelností.

## Hardwarové čítače výkonu:

Hardwarové čítače výkonu (Hardware Performance Counters, HPC) jsou speciální registry, které integrované do procesoru, umožňují sledovat různé aspekty výkonu a chování procesoru. Tyto čítače mohou poskytovat informace o:

1. Počet provedených instrukcí
2. Počet provedených cyklů
3. Počet cache hitů a missů
4. Počet branch (větvení) instrukcí a predikcí
5. Počet zápisů a čtení z paměti
6. Počet závislostí mezi instrukcemi
7. Počet událostí souvisejících s pipeliningem

Tyto informace lze použít k analýze výkonu programu a identifikaci úzkých míst nebo problémů, které lze optimalizovat. Některé nástroje pro práci s hardwarovými čítači výkonu zahrnují:

- `perf`: Nástroj pro profiling na úrovni jádra Linuxu, který podporuje hardwarové čítače výkonu.
- `PAPI`: Performance Application Programming Interface, multiplatformní knihovna pro práci s hardwarovými čítači výkonu.
- `Intel VTune`: Profiler a ladící nástroj od Intelu, který podporuje hardwarové čítače výkonu.

Při použití hardwarových čítačů výkonu je důležité mít na paměti, že jejich podpora a dostupnost se může lišit mezi různými procesory a architekturami.

## Optimalizace řízená profilem (Profile-Guided Optimization, PGO):

Optimalizace řízená profilem (PGO) je technika optimalizace kompilátoru, která používá data získaná z profilingu běhu programu za účelem informování kompilátoru o tom, jak nejlépe optimalizovat kód. PGO zahrnuje následující kroky:

1. Kompilace programu s přepínačem pro generování profilovacích informací (např. `-fprofile-generate` v GCC nebo Clang).
2. Spuštění programu na reprezentativní sadě vstupů, které zahrnují typické scénáře použití, aby byly vygenerovány profilovací data.
3. Opětovná kompilace programu s přepínačem pro využití profilovacích informací (např. `-fprofile-use` v GCC nebo Clang).

PGO může přinést následující výhody:

- Lepší optimalizace na úrovni zdrojového kódu: Kompilátor může zohlednit skutečné chování programu při volbě optimalizačních strategií.
- Optimalizace inliningu funkcí: Kompilátor může lépe rozhodnout, které funkce by měly být inlinovány na základě jejich skutečného použití.
- Optimalizace větvení: Kompilátor může předpovědět pravděpodobnost větvících instrukcí a generovat efektivnější kód.
- Optimalizace rozložení kódu: Kompilátor může rozhodnout, jakým způsobem uspořádat kód v paměti pro snížení cache missů.

Je důležité provést profiling na reprezentativní sadě vstupů, aby PGO mohla efektivně zlepšit výkon programu. PGO může mít významný dopad na výkon, ale jeho výsledky se mohou lišit v závislosti na konkrétním programu a jeho použití.

## Základy kompilátorů C/C++ - AST, intermediální reprezentace:

1. Abstract Syntax Tree (AST):
   - AST je stromová struktura, která reprezentuje zdrojový kód programu ve formě, která je snadno zpracovatelná pro další analýzy a transformace.
   - AST je vytvořen během syntaktické analýzy zdrojového kódu a zachycuje informace o struktuře kódu, např. deklarace, přiřazení, cykly a podmínky.
   - AST slouží jako vstup pro další fáze kompilace, jako je sémantická analýza, optimalizace a generování kódu.

2. Intermediální reprezentace (Intermediate Representation, IR):
   - IR je zjednodušená reprezentace programu, která slouží jako mezikrok mezi AST a výsledným strojovým kódem.
   - IR je navržen tak, aby byl snadno analyzovatelný a modifikovatelný pro optimalizace a transformace kódu.
   - Existují různé formy IR, například:
     - Three-Address Code (TAC): Lineární sekvence instrukcí, kde každá instrukce má nejvýše tři operandy.
     - Static Single Assignment (SSA): IR, ve kterém je každá proměnná přiřazena pouze jednou.

Kompilátory C/C++ jako GCC nebo Clang provádějí několik transformací a optimalizací na úrovni AST a IR před generováním výsledného strojového kódu. Tyto transformace a optimalizace mohou zahrnovat zjednodušení výrazů, inlining funkcí, eliminaci mrtvého kódu, propagaci konstant a mnoho dalších.

## Optimalizační průchody na vysoké a nízké úrovni:

1. Optimalizace na vysoké úrovni (High-Level Optimization):
   - Tyto optimalizace se provádějí na úrovni zdrojového kódu nebo abstraktního syntaktického stromu (AST).
   - Cílem je zlepšit výkon programu pomocí transformací, které využívají znalosti o struktuře a sémantice zdrojového kódu.
   - Příklady optimalizací na vysoké úrovni:
     - Zjednodušení výrazů
     - Eliminace mrtvého kódu
     - Zabalení (wrapping) a rozbalení (unwrapping) cyklů
     - Rozdělení proměnných
     - Odstraňování společných podvýrazů

2. Optimalizace na nízké úrovni (Low-Level Optimization):
   - Tyto optimalizace se provádějí na úrovni intermediální reprezentace (IR) nebo strojového kódu.
   - Cílem je zlepšit výkon programu pomocí transformací, které využívají znalosti o architektuře procesoru a paměti.
   - Příklady optimalizací na nízké úrovni:
     - Alokační optimalizace registrů
     - Inlining funkcí
     - Sdílení registrů mezi proměnnými
     - Optimalizace pipeliningu
     - Optimalizace větvení

Kompilátory C/C++ jako GCC nebo Clang provádějí řadu optimalizačních průchodů na vysoké i nízké úrovni před generováním výsledného strojového kódu. Tyto průchody mohou být řízeny pomocí přepínačů kompilátoru, které umožňují nastavit různé úrovně optimalizace, například `-O1`, `-O2`, `-O3` a `-Os`.
