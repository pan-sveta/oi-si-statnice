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
       - Rozdělen na:
         - **New Generation**:
           - Mladší generace, kde se ukládají nově vytvořené objekty
           - Dále rozdělen na:
             - Eden Space: místo pro vytváření nových objektů
             - Survivor Spaces (S0 a S1): oblasti pro přeživší objekty z Eden Space
         - **Old Generation**:
           - Starší generace, kam se přesouvají objekty, které přežily několik cyklů Garbage Collection
           - Slouží pro dlouhodobě žijící objekty
    3. Java stacks
    4. PC (Program Counter) registry
    5. Nativní (Native) metoda stacks
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

## Volatile variable
## Synchronization - thin fat and biased locking
## Reentrant locks
## Atomic operations based on compare-and-set instructions
## Atomic field updaters
## Non-blocking algorithms
## Wait free algorithms
## Non-blocking stack (LIFO)
## Static and dynamic memory analysis
## Shallow and retained size
## Memory leak
## Data Structures
## Java primitives and objects
## Auto-boxing and unboxing
## Memory efficiency of complex data structures
## Collection for performance
## Type specific collections
## Open addressing hashing
## Collision resolution schemes
## Bloom filters, complexity, false positives, Bloom filter extensions
## Reference types - weak, soft phantom
## JVM object allocation
## Thread-local allocation buffers
## Object escape analysis
## Data locality
## Non-uniform memory allocation
## Networking
## OSI model
## C10K problem
## Blocking and non-blocking input/output
## Threading server
## Event-driven server
## Event-based input/output approaches
## Native buffers in JVM
## Channels and selectors
## Synchronization in multi-threaded programs (atomic operations, mutex, semaphore,rw-lock,spinlock,RCU). When to use which mechanism? Performance bottlenecks of the mentioned mechanisms
## Synchronization in “read-mostly workloads”, advantages and disadvantages of different synchronization mechanisms
## Cache-efficient data structures and algorithms (e.g. matrix multiplication)
## Principles of cache memories different kinds of cache misses
## Self-evicting code
## false sharing – what is it and how deal with it?
## Profiling and optimizations of programs in compiled languages (e.g.C/C++)
## Hardware performance counters
## Profile-guided optimization
## Basics of C/C++ compilers - AST, intermediate representation
## high-level and low-level optimization passes