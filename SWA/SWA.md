# SWA

## Topics
Software architectures, their parameters and qualitative metrics. Architectural patterns,
styles and standards. BE4M36SWA (Course web pages)

## Questions
### Describe Krutchen's 4+1 View Model of a software architecture. Explain how it captures the complete behavior of a developed software from multiple perspectives of the system. How is this model aligned with the UML models?

#### Popis Krutchenova 4+1 View Modelu softwarové architektury:

   - Pohled logický (Logical View):
     - Zobrazuje třídy, objekty, rozhraní a jejich vztahy
     - Zaměřuje se na funkcionalitu systému
   - Pohled procesní (Process View):
     - Popisuje procesy a konkurenci v systému
     - Zaměřuje se na výkonnost, škálovatelnost a stabilitu
   - Pohled fyzický (Physical View):
     - Popisuje mapování softwarových komponent na hardware
     - Zaměřuje se na nasazení a distribuci systému
   - Pohled vývojový (Development View):
     - Zobrazuje organizaci zdrojového kódu, knihoven a komponent
     - Zaměřuje se na správu kódu a modulární strukturu
   - Scénáře (Scenarios):
     - Uplatňuje se pro ověření a validaci návrhu architektury
     - Pomáhá provést průřez všemi čtyřmi pohledy

#### Jak 4+1 View Model zachycuje chování softwaru z různých perspektiv:

   - A. Logický pohled (Logical View):
      - Poskytuje abstraktní pohled na systém z hlediska funkčnosti
      - Umožňuje analyzovat a navrhovat statickou strukturu systému
      - Pomáhá identifikovat třídy, rozhraní a jejich vztahy
      - Slouží k pochopení domény a funkcí, které systém poskytuje

   - B. Procesní pohled (Process View):
      - Zkoumá chování systému z hlediska běhových procesů a vláken
      - Umožňuje identifikovat synchronizační a komunikační aspekty mezi jednotlivými procesy
      - Pomáhá zajišťovat škálovatelnost, výkonnost a stabilitu systému
      - Slouží k analýze a řešení problémů týkajících se konkurence a distribuce

   - C. Fyzický pohled (Physical View):
      - Popisuje, jak jsou softwarové komponenty nasazeny na hardwarové prostředky
      - Umožňuje řešit otázky týkající se komunikace a propojení mezi hardwarovými jednotkami
      - Pomáhá identifikovat potenciální omezení a problémy v hardwarové konfiguraci
      - Slouží k optimalizaci nasazení a distribuce systému

   - D. Vývojový pohled (Development View):
      - Zkoumá strukturu zdrojového kódu, knihoven a modulů
      - Umožňuje identifikovat závislosti a propojení mezi jednotlivými částmi kódu
      - Pomáhá zlepšovat čitelnost, udržitelnost a modularitu kódu
      - Slouží k usnadnění práce vývojářů a podpoře týmové spolupráce

   - E. Scénáře (Scenarios):
      - Představují konkrétní příklady použití systému (use cases)
      - Umožňují ověřit a validovat návrh architektury
      - Pomáhají identifikovat problémy a nedostatky v návrhu
      - Slouží k provádění průřezů mezi všemi čtyřmi pohledy a k integraci různých aspektů systému

#### Souvislost mezi 4+1 View Model a UML modely:

UML diagramy pro 4+1 View Model:

1. Logický pohled (Logical View):
    - Třídní diagram (Class Diagram)
    - Objektový diagram (Object Diagram)
    - Kompoziční struktura (Composite Structure Diagram)
    - Balíčkový diagram (Package Diagram)

2. Procesní pohled (Process View):
    - Diagram činností (Activity Diagram)
    - Sekvenční diagram (Sequence Diagram)
    - Diagram spolupráce (Collaboration Diagram)
    - Stavový diagram (State Diagram)

3. Fyzický pohled (Physical View):
    - Diagram nasazení (Deployment Diagram)
    - Diagram komponent (Component Diagram)
    - Komunikační diagram (Communication Diagram)

4. Vývojový pohled (Development View):
    - Balíčkový diagram (Package Diagram)
    - Diagram komponent (Component Diagram)

Integrace UML s 4+1 View Model:
    - UML diagramy poskytují vizuální reprezentaci pro každý pohled v 4+1 View Modelu
    - Umožňují efektivní komunikaci mezi architekty, vývojáři, testery a dalšími členy týmu
    - Podporují analýzu, návrh, implementaci a údržbu systému
    - Usnadňují kontrolu a řízení kvality architektury

### What is a software architecture? Describe the importance of software architecture when developing a system. What are the software architecture design guidelines? What are the architectural styles? Give an example of an architectural style and describe it in detail.

**Co je softwarová architektura?**

- Softwarová architektura je **struktura** a **organizace** softwarového systému.
- Zahrnuje **komponenty**, jejich **vlastnosti** a **vztahy** mezi nimi.
- Definuje **zásady**, **směrnice** a **omezení** pro vývoj systému.

**Důležitost softwarové architektury při vývoji systému:**

1. **Zajištění kvality**:
   - Architektura zajišťuje, že systém splňuje **funkční** a **nefunkční** požadavky.
2. **Usnadnění komunikace**:
   - Architektura slouží jako **společný jazyk** pro vývojáře, zákazníky a další zúčastněné strany.
3. **Podpora znovupoužitelnosti**:
   - Správně navržená architektura umožňuje **znovupoužití** kódu a komponent.
4. **Zjednodušení rozhodování**:
   - Architektura poskytuje **rámcové rozhodnutí** pro vývojáře, které usnadňuje vývoj a údržbu.
5. **Řízení rizik**:
   - Architektura pomáhá identifikovat a řešit **rizika** spojená s vývojem systému.
6. **Zlepšení výkonnosti**:
   - Architektura optimalizuje **výkonnost**, **škálovatelnost** a **stabilitu** systému.

**Směrnice pro návrh softwarové architektury:**

1. **Rozdělit a vládnout**:
   - Systém rozdělit na menší, snadno řiditelné komponenty.
2. **Abstrakce**:
   - Použít abstrakce pro zjednodušení složitých problémů.
3. **Modularita**:
   - Navrhnout nezávislé a snadno zaměnitelné moduly.
4. **Zachování informací**:
   - Minimalizovat závislosti mezi komponentami.
5. **Škálovatelnost**:
   - Umožnit snadné rozšíření systému.
6. **Znovupoužitelnost**:
   - Navrhovat komponenty tak, aby byly znovupoužitelné.
7. **Flexibilita**:
   - Umožnit snadnou údržbu a přizpůsobení změnám požadavků.

**Architektonické styly:**

- Architektonické styly jsou **vzory** nebo **paradigmata** pro návrh softwarové architektury.

**Příklad architektonického stylu: MVC (Model-View-Controller)**

1. **Model**:
   - Reprezentuje **data** a **byznysovou logiku** aplikace.
   - Nezávislý na prezentační vrstvě a uživatelském rozhraní.
2. **View (Zobrazení)**:
   - Zodpovědný za **prezentaci** a **zobrazení** dat z modelu.
   - Aktualizuje se automaticky, když se změní data v modelu.
3. **Controller (Ovladač)**:
   - Zodpovědný za **řízení** interakce mezi modelem a zobrazením.
   - Zpracovává uživatelské vstupy a aktualizuje model nebo zobrazení.

**Detaily architektonického stylu MVC:**

- **Oddělení zájmů**: MVC odděluje zájmy aplikace do tří komponent, což usnadňuje údržbu a rozšíření.
- **Znovupoužitelnost**: Model a Controller mohou být znovu použity pro různá zobrazení.
- **Flexibilita**: Změny v jedné komponentě mají minimální dopad na ostatní komponenty.

#### What is a design pattern? What problem are design patterns solving? What types of design patterns exist? Why is it important to know the design patterns? Are there design antipatterns?

**Co je návrhový vzor (design pattern)?**

- Návrhový vzor je **opakovatelné řešení** pro často se vyskytující problémy v oblasti softwarového návrhu.
- Není to hotový návrh, ale **šablona** pro řešení problému, kterou lze přizpůsobit konkrétním situacím.

**Jaký problém řeší návrhové vzory?**

- Návrhové vzory řeší problémy, které se vyskytují opakovaně při návrhu softwarových systémů.
- Pomáhají **zlepšit kvalitu** kódu, **usnadnit komunikaci** mezi vývojáři a **urychlit vývoj**.

**Typy návrhových vzorů:**

1. **Vzory pro tvorbu objektů (Creational Patterns)**:
   - Řeší problémy spojené s procesem vytváření objektů.
   - Příklady: Singleton, Factory Method, Abstract Factory, Builder, Prototype.
2. **Strukturální vzory (Structural Patterns)**:
   - Řeší problémy týkající se kompozice tříd a objektů.
   - Příklady: Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy.
3. **Vzory chování (Behavioral Patterns)**:
   - Řeší problémy interakce mezi objekty a způsoby, jakými spolupracují.
   - Příklady: Chain of Responsibility, Command, Interpreter, Iterator, Mediator, Memento, Observer, State, Strategy, Template Method, Visitor.

**Důležitost znalosti návrhových vzorů:**

1. **Zlepšení kvality kódu**:
   - Návrhové vzory poskytují osvědčené řešení, která zvyšují kvalitu kódu.
2. **Zvýšení efektivity vývoje**:
   - Použitím návrhových vzorů lze urychlit vývoj a snížit chybovost.
3. **Usnadnění komunikace mezi vývojáři**:
   - Návrhové vzory slouží jako společný jazyk, který usnadňuje komunikaci a porozumění mezi vývojáři.
4. **Zjednodušení údržby**:
   - Návrhové vzory usnadňují údržbu a rozšiřování kódu díky jejich známé struktuře a principům.
5. **Podpora znovupoužitelnosti**:
   - Návrhové vzory podporují znovupoužitelnost kódu tím, že umožňují snadnější integraci a adaptaci kódu.

**Existují návrhové antivzory (design antipatterns)?**

- Ano, návrhové antivzory existují.
- Jsou to **špatné řešení** nebo **protipříklady** dobrých návrhových vzorů.
- Návrhové antivzory mohou vést ke **špatně navrženému**, **těžko udržitelnému** a **neefektivnímu** kódu.
- Je důležité rozpoznat a vyhýbat se návrhovým antivzorům, aby byla zajištěna dobrá kvalita kódu a efektivní vývoj.

#### What is a microservice architecture? What are its advantages and disadvantages compared to a monolithic architecture. How is microservices development different from developing a monolithic application? Are there any methodologies or guidelines or best practices to follow when developing microservices? Obviously, there are patterns that can be applied in this area, are there any antipatterns that should be avoided?

**Co je mikroservisní architektura?**

- Mikroservisní architektura je **přístup k vývoji softwaru**, který rozděluje aplikaci na **malé, nezávislé služby**.
- Tyto služby komunikují pomocí **lehkých protokolů** (např. REST nebo gRPC) a mají vlastní **databáze** a **konfigurace**.

**Výhody a nevýhody mikroservisní architektury oproti monolitické architektuře:**

**Výhody:**

1. **Lehká škálovatelnost**:
   - Mikroservisy lze škálovat nezávisle na ostatních službách.
2. **Snadnější údržba**:
   - Menší a jednodušší kódová základna usnadňuje údržbu a rozšiřování.
3. **Rychlejší nasazení**:
   - Mikroservisy lze nasazovat nezávisle, což urychluje vývojový cyklus.
4. **Technologická agilita**:
   - Každá služba může používat jiné technologie, což umožňuje snadnější inovace.
5. **Odolnost vůči chybám**:
   - Selhání jedné služby má menší dopad na celý systém.

**Nevýhody:**

1. **Složitost**:
   - Větší počet komponent a interakcí mezi nimi zvyšuje složitost systému.
2. **Výkon**:
   - Komunikace mezi službami může být pomalejší než u monolitické architektury.
3. **Správa a monitorování**:
   - Správa a sledování mnoha nezávislých služeb může být náročné.
4. **Distribuované transakce**:
   - Řešení distribuovaných transakcí může být komplikovanější než v monolitických aplikacích.

**Jak se vývoj mikroservisů liší od vývoje monolitické aplikace?**

1. **Rozdělení aplikace**:
   - Aplikace je rozdělena na menší, nezávislé služby.
2. **Komunikace mezi službami**:
   - Mikroservisy komunikují pomocí API a lehkých protokolů.
3. **Databáze a konfigurace**:
   - Každá služba má vlastní databázi a konfiguraci.
4. **Nezávislé nasazení**:
   - Mikroservisy mohou být nasazeny a škálovány nezávisle.
5. **Technologická diverzita**:
   - Každá služba může používat jiné technologie, což umožňuje snadnější inovace.
6. **Správa a monitorování**:
   - Vyžaduje nástroje a postupy pro správu a sledování mnoha nezávislých služeb.
7. **Distribuované transakce**:
   - Řešení distribuovaných transakcí může být komplikovanější než v monolitických aplikacích.

**Metodiky, směrnice a osvědčené postupy pro vývoj mikroservisů:**

1. **Rozdělit a vládnout**:
   - Aplikaci rozdělit na menší, nezávislé a snadno řiditelné služby.
2. **Definice rozhraní (API)**:
   - Navrhnout jasná a stabilní API pro komunikaci mezi službami.
3. **Oddělení zájmů**:
   - Každá služba by měla mít jednu zodpovědnost a řešit jeden aspekt byznysu.
4. **Decentralizace správy dat**:
   - Každá služba by měla mít svou vlastní databázi a spravovat svá data nezávisle.
5. **Stavová nezávislost**:
   - Preferovat bezestavové služby, které neuchovávají stav mezi požadavky.
6. **Automatizace nasazení a škálování**:
   - Používat nástroje a postupy pro automatické nasazení a škálování služeb.
7. **Monitorování a sledování**:
   - Implementovat monitorování, sledování a protokolování pro snadnou detekci a řešení problémů.
8. **Resilience a tolerování selhání**:
   - Navrhnout služby tak, aby byly schopny zotavit se z chyb a pokračovat v provozu.
9. **Bezpečnost**:
   - Zabezpečit komunikaci mezi službami a chránit citlivá data.
10. **Kontejnerizace a orchestrace**:
    - Používat kontejnery (např. Docker) a orchestrátory (např. Kubernetes) pro snadnou správu a škálování.

**Antivzory, kterým by se mělo vyhnout při vývoji mikroservisů:**

1. **Nedostatečné rozdělení služeb**:
   - Příliš velké nebo příliš malé služby mohou vést k problémům se škálovatelností a údržbou.
2. **Nadbytečná komunikace mezi službami**:
   - Příliš mnoho vzájemné komunikace mezi službami může vést k problémům s výkonem a složitosti.
3. **Centrální správa dat**:
   - Spoléhání na jednu centrální databázi pro všechny služby může vést k problémům se škálovatelností a nezávislostí služeb.
4. **Synchronní komunikace**:
   - Nadměrné použití synchronní komunikace může způsobit výkonnostní problémy a závislost mezi službami.
5. **Nedostatečné monitorování a sledování**:
   - Absence monitorování a sledování může ztížit detekci a řešení problémů.
6. **Nedostatečná bezpečnost**:
   - Nedostatek zabezpečení mezi službami nebo nedbalost při ochraně dat může vést k zranitelnostem.
7. **Vývoj monolitu v mikroservisách**:
   - Přístup k vývoji mikroservisů, který zachovává špatné návyky z monolitického vývoje, může způsobit výkonnostní a údržbové problémy.
8. **Nedostatečná automatizace nasazení a škálování**:
   - Ruční nasazení a škálování služeb může vést k chybám a zpomalit vývoj.
9. **Zanedbávání kontejnerizace a orchestrace**:
   - Neužívání kontejnerů a orchestrátorů může ztížit správu a škálování mikroservisů.
10. **Nedostatečná dokumentace a komunikace**:
    - Špatně zdokumentované nebo nekomunikované změny mohou vést k nedorozuměním a chybám mezi týmy.

#### Software architects can choose one architecture over another. The choice may affect the quality of the final product. Can you tell if one architecture is better than another or if one architecture is bad while the other is not? How can you measure the quality of an architecture? Can you measure the quality from different perspectives?

Při výběru softwarové architektury je těžké říci, že jedna architektura je obecně lepší než druhá, protože jejich vhodnost závisí na konkrétních požadavcích a omezeních projektu. Při výběru architektury je důležité zvážit následující faktory:

1. **Požadavky na výkon**:
   - Některé architektury mohou lépe podporovat vysoký výkon než jiné, například distribuované systémy pro škálování.

2. **Škálovatelnost**:
   - Zvolená architektura by měla umožňovat snadné škálování a rozšiřování aplikace, aby bylo možné lépe řešit růst zátěže.

3. **Flexibilita a rozšiřitelnost**:
   - Architektura by měla umožňovat snadné přidávání nových funkcí a integraci s dalšími systémy.

4. **Bezpečnost**:
   - Důležité je zvážit, jak dobře architektura řeší bezpečnostní hrozby a zabezpečuje citlivá data.

5. **Údržba a evoluce**:
   - Architektura by měla usnadňovat údržbu a umožňovat snadnou adaptaci na změny v požadavcích nebo technologiích.

6. **Náklady a zdroje**:
   - Je třeba zohlednit dostupné zdroje, jako je čas, rozpočet a lidské zdroje, a zvážit náklady na vývoj, provoz a údržbu.

7. **Kompatibilita s technologiemi**:
   - Zvolená architektura by měla být kompatibilní s technologiemi, které tým již používá, nebo které plánuje použít.

8. **Týmová zkušenost a dovednosti**:
   - Je důležité zvážit zkušenosti a dovednosti týmu a jak dobře se dokážou vyrovnat s nároky zvolené architektury.

Při výběru architektury je důležité zvážit všechny tyto faktory a zvolit takovou, která nejlépe vyhovuje konkrétním potřebám a omezením projektu. Není žádná univerzálně "špatná" nebo "lepší" architektura; místo toho je třeba posoudit, jaká architektura je nejvhodnější pro daný projekt.

**Měření kvality architektury:**

Kvalitu softwarové architektury lze měřit pomocí několika metrik a z různých perspektiv. Některé z těchto perspektiv zahrnují:

1. **Výkon**:
   - Měření, jak rychle a efektivně architektura zvládá požadavky, např. doba odezvy, průchodnost a latence.
   
2. **Škálovatelnost**:
   - Hodnocení, jak snadno může architektura růst, aby vyhověla rostoucím požadavkům, a jak dobře se přizpůsobuje změnám v zátěži.

3. **Flexibilita a rozšiřitelnost**:
   - Určení, jak snadno může být architektura rozšířena nebo upravena pro nové funkce nebo integraci s dalšími systémy.

4. **Bezpečnost**:
   - Hodnocení, jak dobře architektura zabezpečuje citlivá data a chrání před bezpečnostními hrozbami.

5. **Spolehlivost a odolnost**:
   - Měření, jak dobře architektura zvládá selhání a chyby, a jak rychle se dokáže zotavit.

6. **Údržba a evoluce**:
   - Hodnocení, jak snadno může být architektura udržována a aktualizována, aby vyhovovala změnám v požadavcích a technologiích.

7. **Modularita a oddělení zájmů**:
   - Určení, jak dobře je architektura rozdělena do samostatných, snadno spravovatelných a znovupoužitelných komponent.

8. **Testovatelnost**:
   - Hodnocení, jak snadno lze architekturu testovat a validovat pro zajištění kvality a spolehlivosti.

Každá z těchto perspektiv nabízí odlišné metriky a hodnocení kvality architektury. Pro měření kvality architektury je třeba zvážit všechny tyto aspekty a určit, jaké metriky jsou nejrelevantnější pro konkrétní projekt a jeho požadavky.