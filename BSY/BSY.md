# BSY

## Topics
Security analysis of operating systems, development of secure software and web applications security. Analysis of cyberattacks and malware. Security of mobile devices.
BE4M36BSY (Course web pages)

## Questions
- Managing a software project with a security as an objective, advantages and disadvantages of waterfall and ellipse model for this use-case, systematic identification of potential vulnerabilities, STRIDE, attack modelling (attack trees), ranking of vulnerabilities (ideal, DREAD).
- Timing and storage covert channels, Side channel attacks, Steganography.
- Discretionary access control(Access control list, Capabilities), Mandatory access control, Multi-level security, Biba model, Multi-lateral security, Role-based access control.
- Privilege escalation, security of operating systems, trusted computer base, reference monitor, complete mediation, needed mechanism for securing current OS, memory management, rings.
- Virtualization, virtual machine monitor, micro-kernels, general-purpose sandboxing, danger, Kernel namespaces, seccomp, Linux kernel capabilities.
- Access control model of web ecosystem, single-origin policy, preservations of integrity of data and code, sandboxing in web, content security policy.
- Network protocols, TCP, DNS, BGP, security of HTTPs, mechanism of certificates, security of certificate infrastructure.
- Firewalls, network intrusion detection, network intrusion prevention, thin client, intrusion deflection.
- Denial of service attack, reflection attacks, syn-cookies, detection and protection against DOS.

## Bezpečnostní řízení projektů softwaru

Bezpečnost je klíčovou součástí každého softwarového projektu. Správné řízení projektu s důrazem na bezpečnost může pomoci snížit rizika a minimalizovat náklady na opravy bezpečnostních nedostatků v pozdějších fázích projektu.

Existují různé modely řízení projektů softwaru, ale v této souvislosti se zaměříme na Waterfall a Elipsa model.

## Waterfall model

Waterfall model je lineární proces řízení projektů, který se skládá z jednotlivých fází, které se následují: 

* **Definice požadavků:** V této fázi jsou stanoveny všechny požadavky na projekt.
* **Návrh:** V této fázi se navrhuje architektura projektu a připravuje se plán realizace.
* **Implementace:** Tato fáze zahrnuje samotnou implementaci projektu.
* **Testování:** V této fázi se testují jednotlivé části projektu a ověřuje se, zda splňují stanovené požadavky.
* **Dodávka:** V této fázi se projekt dokončuje a dodává se zákazníkovi.

Výhodou Waterfall modelu je jeho jednoduchost a přehlednost, která usnadňuje řízení projektu. Nevýhodou je však jeho nedostatečná flexibilita, což může být problematické v případě, že se objeví nějaké neočekávané problémy během realizace projektu.

## Elipsa model

Elipsa model je iterativní proces řízení projektů, který se skládá z opakujících se fází:

* **Plánování:** V této fázi se stanovují cíle a požadavky na projekt.
* **Návrh:** V této fázi se navrhuje architektura projektu.
* **Implementace:** Tato fáze zahrnuje samotnou implementaci projektu.
* **Testování:** V této fázi se testují jednotlivé části projektu a ověřuje se, zda splňují stanovené požadavky.
* **Hodnocení:** V této fázi se hodnotí výsledky projektu a plánuje se další iterace.

Výhodou Elipsa modelu je jeho flexibilita, což umožňuje rychlé reakce na změny v průběhu projektu. Nevýhodou může být větší náročnost na řízení projektu, jelikož každá iter


## Systematic identification of potential vulnerabilities

Systémová identifikace potenciálních zranitelností

- Systémová identifikace potenciálních zranitelností je důležitým krokem pro zajištění bezpečnosti systému.
- Proces zahrnuje systematickou analýzu všech aspektů systému.
- Identifikuje se potenciální zranitelnosti, posuzuje se jejich pravděpodobnost a potenciální dopad a stanovuje se jejich prioritizace pro odstranění.
- Existují různé metody, jako je manuální analýza, automatické skenování a penetrační testování, které mohou být použity samostatně nebo v kombinaci pro poskytnutí komplexního hodnocení zranitelností systému.
- Manuální analýza zahrnuje důkladný přezkum architektury, návrhu a implementace systému zkušenými bezpečnostními odborníky.
- Automatické skenování identifikuje známé zranitelnosti v systému rychleji, ale vyžaduje manuální ověření a posouzení, zda jsou zranitelnosti skutečné.
- Penetrační testování simuluje útok na systém, aby se zjistilo, zda existují skryté zranitelnosti.
- Identifikace potenciálních zranitelností chrání citlivé informace před útoky a pomáhá minimalizovat rizika.

## STRIDE

`STRIDE` je zkratka pro sedm nejčastějších hrozeb v kybernetické bezpečnosti: 

- **S**poofing (falešné identifikace) - útočník se vydává za jiného uživatele nebo za systém
- **T**ampering (pozměňování) - útočník mění data nebo kód v systému
- **R**epudiation (popírání) - útočník popírá svou účast v útoku nebo transakci
- **I**nformation disclosure (odhalení informací) - útočník získává nebo odhaluje citlivé informace
- **D**enial of Service (odmítnutí služby) - útočník přetíží systém nebo službu, aby byla nedostupná pro ostatní uživatele
- **E**levation of privilege (zvýšení oprávnění) - útočník získává vyšší oprávnění, než které mu bylo původně přiděleno
- **A**uthorization bypass (obcházení autorizace) - útočník se dostává do systému bez nutnosti platného ověření identity nebo oprávnění

Použití této metodiky může pomoci při analýze bezpečnostních hrozeb a návrhu ochranných opatření.

## Attack modelling (attack trees)

Útokové modelování (stromy útoků) je metoda, která se používá k identifikaci možných zranitelností v systému a kategorizaci útoků, které by mohly být na systém provedeny. Tato metoda umožňuje analyzovat potenciální hrozby a navrhnout zabezpečení systému proti nim.

Attack trees jsou grafické nástroje, které reprezentují útoky na systém pomocí stromové struktury. Kořen stromu představuje cíl útoku, zatímco listy stromu představují konkrétní způsoby, jak útok na cíl dosáhnout. Každý uzel stromu reprezentuje jednu zranitelnost nebo krok v útoku.

Použití attack trees umožňuje identifikovat nejpravděpodobnější útoky a navrhnout opatření pro zvýšení bezpečnosti systému. Tato metoda také umožňuje určit, které zabezpečovací opatření jsou nejúčinnější a které jsou méně účinné.

Attack modelling (attack trees) jsou užitečným nástrojem pro každého, kdo se zabývá kybernetickou bezpečností. Tato metoda umožňuje identifikovat a analyzovat potenciální hrozby a navrhnout opatření pro ochranu systému proti nim.

## Ranking of vulnerabilities (ideal, DREAD)

### Ideální

Ideální ranking zranitelností se skládá z pěti kritérií:

1. Vliv (Impact) - jak moc by zranitelnost mohla poškodit organizaci
2. Pravděpodobnost (Likelihood) - jak pravděpodobné je, že se zranitelnost vyskytne
3. Využitelnost (Ease of Exploitation) - jak snadné je zranitelnost využít
4. Zjištění (Discoverability) - jak snadné je zranitelnost najít
5. Důležitost (Importance) - jak důležitá je pro organizaci ohrožená oblast

### DREAD

DREAD ranking zranitelností se skládá z pěti kritérií:

1. Vliv (Damage) - jak moc by zranitelnost mohla poškodit organizaci
2. Reprodukovatelnost (Reproducibility) - jak snadné je zranitelnost reprodukovat
3. Exploitabilita (Exploitability) - jak snadné je zranitelnost využít
4. Postižení uživatelů (Affected Users) - kolik uživatelů by mohlo být zasaženo zranitelností
5. Rozšíření (Discoverability) - jak snadné je zranitelnost najít

## Timing and storage covert channels

**Časování a ukládání skrytých kanálů**

### **Popis**
Skryté kanály jsou metody, které umožňují komunikaci mezi útočníkem a obětí bez detekce ze strany bezpečnostních opatření. Časování a ukládání skrytých kanálů jsou dva způsoby, jak mohou být skryté kanály implementovány.

**Časování skrytých kanálů:** Tento typ skrytého kanálu využívá různých časových prodlev mezi různými akcemi, jako jsou například požadavky na server nebo odesílání dat. Tyto prodlevy jsou použity jako kódování pro přenos informací.

**Ukládání skrytých kanálů:** Tento typ skrytého kanálu využívá různých možností ukládání dat, jako jsou například metadata souborů nebo skryté sektory na pevném disku. Tyto metody jsou použity k ukládání informací, které jsou později získány útočníkem.

### **Příklad využití**

Útočník může využít časování skrytého kanálu k přenosu informací mezi svým počítačem a obětí. Například může použít prodlevu mezi požadavky na server k přenosu informací v kódované formě.

Další možností je využití ukládání skrytého kanálu k ukládání informací na pevný disk oběti. Útočník může využít skrytých sektorů na disku k ukládání informací, které jsou později získány pomocí speciálního softwaru.

### **Prevence**

Prevence skrytých kanálů zahrnuje monitorování časových prodlev a ukládání dat na počítači. Bezpečnostní opatření by měla být navržena tak, aby minimalizovala možnosti využití skrytých kanálů útočníky. Například by měla být omezena možnost ukládání dat na pevný disk a monitorovány časové prodlevy.

## Side channel attacks

Side channel attacks are a type of cyber attack that exploits weaknesses in a system's physical or electromagnetic characteristics, such as power consumption, electromagnetic radiation, or sound, to extract sensitive information. These attacks are often used to bypass encryption or other security measures and can be difficult to detect.

### **Types of Side Channel Attacks**

1. **Power Analysis Attack**: This attack involves analyzing the power consumption of a device to determine the secret key used in encryption. 

2. **Electromagnetic Attack**: This attack involves analyzing the electromagnetic radiation emitted by a device to determine the secret key used in encryption.

3. **Acoustic Attack**: This attack involves analyzing the sound produced by a device to determine the secret key used in encryption.

### **Prevention of Side Channel Attacks**

1. **Implementing Countermeasures**: Implementing countermeasures such as noise reduction techniques, shielding, and filtering can help prevent side channel attacks.

2. **Using Advanced Encryption**: Using advanced encryption algorithms that are resistant to side channel attacks can also help prevent these attacks.

3. **Regular Security Audits**: Regular security audits can help identify and address any vulnerabilities that may be exploited by side channel attacks.
   
## Steganography

Steganografie je technika skrytí dat uvnitř jiných dat, aby se skryla existence samotného zprávy. Tato technika se často používá k ukrývání škodlivého kódu nebo citlivých informací. Steganografie může být detekována pomocí specializovaných nástrojů, které jsou navrženy k odhalení skrytých dat. Je důležité mít vědomosti o této technice, aby se zabránilo útokům, které využívají steganografii.

## Discretionary access control(Access control list, Capabilities)


Discretionary access control (DAC) - řízení přístupu na základě diskrece uživatele

**Co to je?**
DAC je typ řízení přístupu, který umožňuje uživatelům kontrolovat přístup k objektům, jako jsou soubory a složky, na základě své diskrece. To znamená, že uživatelé mohou rozhodnout, kteří další uživatelé nebo skupiny mají přístup k jejich objektům.

**Jak to funguje?**
DAC využívá dvou metod řízení přístupu: Access control list (ACL) a Capabilities. ACL umožňuje uživatelům určit, kdo má přístup k jejich objektům a jaký typ přístupu mají. Capabilities na druhé straně umožňují uživatelům určit, ke kterým objektům mají ostatní uživatelé přístup a jaký typ přístupu mají.

**Proč je to důležité v kybernetické bezpečnosti?**
DAC je důležitým nástrojem v kybernetické bezpečnosti, protože umožňuje uživatelům kontrolovat přístup k důležitým datům a informacím. Pokud jsou tyto objekty špatně chráněny, mohou být snadno ohroženy útokem hackerů. DAC umožňuje uživatelům chránit své objekty a informace před neoprávněným přístupem. 


Poznámka: V českém jazyce se používá termín řízení přístupu na základě diskrece uživatele pro Discretionary access control.

## Mandatory access control

**Mandatory Access Control (MAC)** je bezpečnostní mechanismus v kybernetické bezpečnosti, který řídí přístup k datům a zdrojům na základě předem definovaných pravidel. Tyto pravidla jsou vytvořeny administrátorem systému a aplikovány na uživatele a procesy. 

MAC je účinným způsobem, jak minimalizovat rizika způsobená útoky na systém. Umožňuje správci systému přesně definovat, kdo má přístup k určitým datům a zdrojům a co s nimi může dělat. Tím se snižuje riziko, že neoprávněný uživatel získá přístup k citlivým informacím nebo je poškodí.

MAC je často používán v prostředí s vysokou úrovní bezpečnosti, jako jsou vládní organizace, finanční instituce a průmyslové podniky. Je to důležitý nástroj v boji proti kybernetickým hrozbám a je nezbytný pro ochranu citlivých dat a informací.

Povinná kontrola přístupu (MAC) je bezpečnostní mechanismus, který řídí přístup k datům a zdrojům na základě předem definovaných pravidel. Tento mechanismus minimalizuje riziko útoků na systém a snižuje riziko získání přístupu k citlivým informacím nebo jejich poškození. MAC je často používán v prostředí s vysokou úrovní bezpečnosti, jako jsou vládní organizace, finanční instituce a průmyslové podniky.

## Multi-level security

Multi-level security (MLS) je koncept zabezpečení, který se používá v oblasti kybernetické bezpečnosti. Tento koncept zahrnuje použití různých úrovní zabezpečení pro různé části systému. Každá úroveň zabezpečení má své vlastní pravidla a omezení, které pomáhají chránit systém před útoky.

MLS se používá v mnoha různých oblastech, včetně vládních a vojenských systémů, finančních institucí a podobně. Většina systémů MLS používá tři nebo více úrovní zabezpečení, ale některé mohou mít i více než deset úrovní.

Každá úroveň zabezpečení má své vlastní názvy a čísla, například Top Secret (nejvyšší tajné), Secret (tajné), Confidential (důvěrné) a Unclassified (neutajené). Každá úroveň má také své vlastní pravidla pro přístup a zpracování informací.

Použití MLS může pomoci minimalizovat riziko útoku na systém a chránit citlivé informace. Nicméně, implementace MLS může být nákladná a složitá, a může vyžadovat specializované znalosti a technologie.

## Biba model

Biba model je bezpečnostní model, který se používá k ochraně informací a dat. Tento model se zaměřuje na zachování integrity dat a předcházení neautorizovanému přístupu k nim. 

Model je pojmenován po svém tvůrci, americkém matematikovi Kennethu Bibovi. Biba model se skládá ze tří základních úrovní: 

1. **Integrita dat** - Tato úroveň se zaměřuje na zachování integrity dat a zabraňuje jakémukoli neoprávněnému zásahu do dat. Zabezpečuje se tak, aby data nebyla poškozena, ztracena nebo změněna.

2. **Dostupnost dat** - Tato úroveň se zaměřuje na zajištění dostupnosti dat pro autorizované uživatele. Zabezpečuje se tak, aby data byla k dispozici v době, kdy jsou potřebná.

3. **Důvěrnost dat** - Tato úroveň se zaměřuje na zajištění důvěrnosti dat a zabraňuje neoprávněnému přístupu k nim. Zabezpečuje se tak, aby data byla přístupná pouze autorizovaným uživatelům.

Biba model je velmi užitečný pro organizace, které se zabývají citlivými informacemi a daty. Tento model pomáhá chránit informace a data před útoky a zabezpečuje, že jsou k dispozici pouze pro autorizované osoby.

## Multi-lateral security

Multi-laterální bezpečnost znamená spolupráci a koordinaci mezi více stranami v oblasti kybernetické bezpečnosti. To zahrnuje vládní organizace, soukromé společnosti, akademické instituce a další subjekty. Cílem multi-laterální bezpečnosti je zlepšit ochranu proti kybernetickým hrozbám a zvýšit schopnost reagovat na ně.

V rámci multi-laterální bezpečnosti se mohou provádět různé aktivity, jako jsou společné cvičení, výměna informací o hrozbách a zranitelnostech, spolupráce na vývoji bezpečnostních technologií a standardů a další. Tato spolupráce může být regionální, mezinárodní nebo dokonce globální.

V České republice se multi-laterální bezpečnost v kybernetické bezpečnosti provádí prostřednictvím různých iniciativ a organizací, jako jsou Národní centrum kybernetické bezpečnosti, Česká asociace pro kybernetickou bezpečnost a další. Tyto organizace spolupracují s různými subjekty, včetně vládních úřadů, soukromých společností a akademických institucí, aby zlepšily kybernetickou bezpečnost v České republice.

## Role-based access control

Role-based access control (RBAC) je metoda řízení přístupu k informacím a systémům založená na přidělování oprávnění uživatelům na základě jejich rolí v organizaci. Tento systém umožňuje správci přidělit uživatelům práva k určitým činnostem na základě jejich pracovních funkcí a odpovědností, což snižuje riziko zneužití oprávnění. RBAC je důležitým prvkem kybernetické bezpečnosti, protože pomáhá minimalizovat riziko útoků ze strany interních a externích hrozeb a zajišťuje ochranu citlivých informací.

## Privilege escalation

Privilege escalation představuje zvýšení úrovně oprávnění uživatele v systému. To znamená, že uživatel, který nemá původně dostatečné oprávnění, získává vyšší úroveň oprávnění, aby mohl provádět určité akce, ke kterým by jinak neměl přístup.

Tento proces může být zneužitý útočníky, kteří se snaží získat neoprávněný přístup k systému. Pokud útočník dokáže získat omezené oprávnění, může použít různé techniky, aby získal vyšší úroveň oprávnění a získal tak plný přístup k systému.

Existuje několik způsobů, jak útočníci mohou provést privilege escalation, včetně zneužití chyb v softwaru, zneužití chyb v konfiguraci systému a využití slabých hesel.

Proti privilege escalation útokům mohou být použity různé bezpečnostní opatření, jako jsou aktualizace softwaru, konfigurační změny a zlepšení správy hesel.

## Security of operating systems

Bezpečnost operačních systémů je klíčovou součástí kybernetické bezpečnosti. Operační systémy jsou základem pro všechny aplikace a procesy běžící na počítači, a proto je důležité zajistit jejich bezpečnost. Některé z důležitých opatření pro zajištění bezpečnosti operačních systémů jsou:

### 1. Aktualizace

Aktualizace operačního systému jsou důležité, protože obsahují opravy chyb a zranitelností. Je důležité pravidelně aktualizovat operační systém a všechny nainstalované aplikace, aby se minimalizovala rizika útoku.

### 2. Antivirový software

Antivirový software je důležitým nástrojem pro ochranu operačního systému. Antivirový software dokáže odhalit a zablokovat škodlivý software, který by mohl poškodit operační systém.

### 3. Firewall

Firewall je dalším důležitým nástrojem pro zajištění bezpečnosti operačního systému. Firewall dokáže blokovat nežádoucí přístup k počítači a chránit ho před útoky z internetu.

### 4. Silné heslo

Silné heslo je důležité pro ochranu operačního systému. Heslo by mělo být dostatečně dlouhé a obsahovat kombinaci písmen, číslic a speciálních znaků.

Bezpečnost operačních systémů je důležitá pro ochranu počítače a dat před útoky. Pravidelná aktualizace, antivirový software, firewall a silné heslo jsou důležitými nástroji pro zajištění bezpečnosti operačního systému.

## Trusted computer base

Trusted computer base je termín používaný v kybernetické bezpečnosti pro označení části systému, která je považována za důvěryhodnou a zabezpečenou. Tato část systému je obvykle oddělena od zbytku systému a obsahuje kritické funkce, jako jsou autentizace uživatelů, řízení přístupu a záznamy o událostech. Cílem trusted computer base je minimalizovat rizika spojená s útoky na systém a zajistit, aby důvěryhodné informace zůstaly v bezpečí.

## Reference monitor

Reference Monitor (Referenční monitor) je základním bezpečnostním mechanismem v oblasti kybernetické bezpečnosti. Je to softwarový mechanismus, který řídí přístup k systému a zajišťuje, že pouze oprávněné osoby mají přístup k citlivým datům a aplikacím.

Referenční monitor funguje jako středník mezi uživateli a systémem. Každý požadavek na přístup k systému musí projít referenčním monitorem, který vyhodnotí, zda je uživatel oprávněn přistupovat k daným datům a aplikacím. Pokud je uživatel oprávněn, referenční monitor povolí přístup. Pokud ne, přístup je zamítnut.

Referenční monitor je klíčovým prvkem v rámci bezpečnostní architektury a je používán v mnoha systémech, včetně operačních systémů, firewalů a antivirových programů. Jeho účelem je minimalizovat rizika spojená s neoprávněným přístupem k citlivým datům a aplikacím a chránit tak uživatele a organizace před kybernetickými hrozbami.

## Complete mediation, needed mechanism for securing current OS, memory management, rings.

Kompletní mediací je mechanismus, který zajišťuje, že každá interakce mezi subjekty v systému je řízena a kontrolována. Tento mechanismus zahrnuje kontrolu přístupu, autentizaci, autorizaci a auditování.

### Mechanismus pro zabezpečení současného operačního systému

Pro zabezpečení současného operačního systému je třeba použít několik mechanismů, jako jsou firewally, antivirové programy, aktualizace operačního systému a aplikací, zabezpečené připojení k internetu a další.

### Správa paměti

Správa paměti je proces, který zajišťuje, že každý proces v systému má přístup pouze k paměti, kterou mu byla přidělena. Tento mechanismus zahrnuje virtualizaci paměti, oddělení procesů a kontrolu přístupu k paměti.

### Kruhy

Kruhy jsou mechanismem pro oddělení procesů v systému. Existují čtyři kruhy, přičemž každý kruh má svou úroveň oprávnění. Kruh 0 je nejvyšší úroveň a používá se pro jádro operačního systému. Kruhy 1 a 2 jsou určeny pro ovladače a systémové služby. Kruh 3 je určen pro uživatelské procesy. Tento mechanismus zajišťuje, že procesy v nižších kruzích nemohou ovlivnit procesy v kruzích vyšších. 


## Virtualization

Virtualizace je proces vytváření virtuálních verzí hardwaru, softwaru nebo síťových prostředků. Tento proces umožňuje oddělit jednotlivé části systému od sebe a simulovat jejich chování. To může být užitečné v oblasti kybernetické bezpečnosti, protože umožňuje izolovat potenciálně nebezpečné aplikace nebo procesy od zbytku systému.

Existují různé typy virtualizace, včetně virtualizace operačního systému, virtualizace aplikace a virtualizace síťových prostředků. Každý typ má své vlastní výhody a nevýhody, a také různé použití v oblasti kybernetické bezpečnosti.

Virtualizace může být použita k izolaci potenciálně nebezpečných aplikací od zbytku systému, což může pomoci chránit systém před útoky malware. Také umožňuje vytvoření testovacího prostředí, ve kterém je možné testovat nové aplikace nebo aktualizace bez rizika poškození systému.

Nicméně, virtualizace také přináší svá vlastní rizika. Pokud není řádně zabezpečena, může být virtuální prostředí cílem útoků. Také může být použita k útoku na jiné systémy, pokud je virtuální prostředí propojeno s jinými sítěmi.

Proto je důležité, aby byla virtualizace správně konfigurována a zabezpečena. To zahrnuje použití silných hesel a šifrování dat v rámci virtuálního prostředí. Také je důležité pravidelně aktualizovat virtuální prostředí a provádět pravidelné kontroly zabezpečení.

## Virtual machine monitor

Virtual Machine Monitor (VMM) nebo také hypervisor je softwarová vrstva, která umožňuje běh více virtuálních strojů na jednom fyzickém počítači. VMM zajišťuje izolaci mezi jednotlivými virtuálními stroji a hostitelským operačním systémem, což zvyšuje bezpečnost celého systému. Využití VMM je často doporučováno v oblasti kybernetické bezpečnosti, protože umožňuje izolovat potenciálně nebezpečné aplikace a procesy na jednom virtuálním stroji, což minimalizuje riziko šíření škodlivého kódu na ostatní části systému.

V českém jazyce se Virtual Machine Monitor často označuje jako hypervisor.


## Micro-kernels

V oblasti kybernetické bezpečnosti se termín *micro-kernels* používá pro označení jádra operačního systému, které obsahuje pouze nezbytně nutné funkce a služby. Tento přístup přináší výhody v oblasti bezpečnosti, neboť útočník má méně možností, jak zneužít zranitelnosti v jádře systému. 

Kromě toho mohou být funkce operačního systému, které nejsou nezbytné pro běh aplikací, implementovány jako samostatné procesy, které běží mimo jádro. Tím se zvyšuje bezpečnost systému, neboť chyby v těchto procesech nemají vliv na stabilitu jádra.

Celkově lze říci, že použití *micro-kernels* je jedním z přístupů, jak zvýšit bezpečnost operačního systému a minimalizovat riziko útoků.

## General-purpose sandboxing, 

Obecné sandboxování je metoda, která slouží k izolaci a omezení přístupu k určitým funkcím a zdrojům aplikace. Tato technologie umožňuje chránit systém před nebezpečným kódem a zabezpečit citlivá data. Sandboxování se používá v různých oblastech, jako je například virtualizace, testování aplikací nebo v oblasti kybernetické bezpečnosti. V oblasti kybernetické bezpečnosti se sandboxování používá k analýze neznámých souborů a programů, které mohou obsahovat malware. Sandboxování umožňuje analyzovat chování programu v izolovaném prostředí, což umožňuje identifikovat nebezpečné chování a přijmout potřebná opatření k ochraně systému.

## Kernel namespaces, seccomp, Linux kernel capabilities

### Kernelové jmenné prostory

Kernelové jmenné prostory jsou mechanismus, který umožňuje oddělit procesy a zdroje v operačním systému. Tento mechanismus může být využit pro izolaci procesů a snížení rizika útoků v kybernetickém prostředí.

### Seccomp

Seccomp je bezpečnostní mechanismus v operačním systému, který umožňuje omezit přístup procesů k systémovým voláním. Tento mechanismus může být využit pro snížení rizika útoků v kybernetickém prostředí.

### Linuxové jádrové schopnosti

Linuxové jádrové schopnosti jsou mechanismus, který umožňuje procesům získávat přístup k určitým zdrojům v operačním systému. Tyto schopnosti mohou být využity pro izolaci procesů a snížení rizika útoků v kybernetickém prostředí.

## Access control model of web ecosystem

Model přístupové kontroly ekosystému webu se používá k řízení přístupu k informacím a zdrojům na internetu. Tento model zahrnuje různé metody, jako jsou autentizace, autorizace a auditování, které pomáhají chránit citlivé informace a zdroje před neoprávněným přístupem.

Autentizace je proces ověřování identity uživatele. To může zahrnovat použití hesel, biometrických údajů nebo jiných metod pro ověření identity uživatele.

Autorizace je proces řízení přístupu k informacím a zdrojům na základě ověřené identity uživatele. To zahrnuje určování, kteří uživatelé mají přístup k určitým informacím a zdrojům a jakým způsobem mohou tyto zdroje používat.

Auditování je proces sledování a zaznamenávání aktivit uživatelů na internetu. To zahrnuje zaznamenávání přístupu k informacím a zdrojům, změn v datech a dalších aktivit, které mohou mít vliv na bezpečnost informací a zdrojů.

Správné použití modelu přístupové kontroly ekosystému webu může pomoci chránit citlivé informace a zdroje před neoprávněným přístupem a zneužitím. Je důležité, aby organizace měly správné politiky a postupy pro řízení přístupu k informacím a zdrojům na internetu a aby tyto politiky a postupy byly pravidelně aktualizovány a přizpůsobeny aktuálním hrozbám v kybernetické bezpečnosti.

## Single-origin policy

`Single-origin policy` (politika jednoho zdroje) je bezpečnostní mechanismus v prohlížečích webových stránek, který omezuje přístup JavaScriptu a dalším skriptovacím jazykům ke zdrojům z jiných domén. Tento mechanismus zabraňuje útočníkům využívat kódy na jedné stránce a aplikovat je na jinou stránku, což může vést k útokům typu cross-site scripting (XSS) a dalším bezpečnostním hrozbám. Jedná se o důležitý prvek v ochraně webových aplikací a uživatelských dat.

## Preservations of integrity of data and code

Jedním z hlavních cílů kybernetické bezpečnosti je zajistit ochranu integrity dat a kódu. Integrity dat znamená, že data zůstanou nedotčena a nezměněna během přenosu nebo ukládání. Integrity kódu znamená, že kód zůstane nedotčen a nezměněn během vývoje, testování a nasazení.

Existuje několik způsobů, jak zajistit ochranu integrity dat a kódu:

- Šifrování: šifrování dat a kódu může pomoci chránit je před neoprávněným přístupem a úpravami.
- Digitální podpisy: digitální podpisy mohou pomoci ověřit pravost kódu a dat a zajistit, že nebyly změněny.
- Kontrola přístupu: omezení přístupu k datům a kódu může pomoci zabránit neoprávněné úpravě.
- Zálohování: pravidelné zálohování dat a kódu může pomoci obnovit původní verzi v případě útoku.

Je důležité, aby organizace měly plán na ochranu integrity dat a kódu a aby tento plán pravidelně aktualizovaly a testovaly, aby byly připraveny na případné útoky.

## Sandboxing in web

`Sandboxing` je bezpečnostní opatření v kybernetické bezpečnosti, které umožňuje izolovat procesy a aplikace od ostatních částí systému. Tento koncept se nejčastěji používá v internetových prohlížečích, kde jsou webové stránky spouštěny v izolovaném prostředí, aby se minimalizovala možnost útoku na uživatelský systém. Sandbox umožňuje bezpečné testování nových aplikací a softwaru, aniž by se ohrozila bezpečnost celého systému.

## Content security policy.

Content Security Policy (CSP) je bezpečnostní mechanismus, který slouží k omezení rizik spojených s útoky typu Cross-Site Scripting (XSS), Clickjacking a dalšími útoky založenými na vkládání kódu do webových stránek.

CSP umožňuje definovat, jaké zdroje jsou povoleny pro načítání na stránce, jako jsou skripty, obrázky, styly a další. To znamená, že pokud je například na stránce použit skript z externího zdroje, který není definován v CSP, bude blokován a stránka se nezobrazí.

CSP lze definovat pomocí HTTP hlavičky nebo meta tagu v HTML kódu stránky. Správné nastavení CSP může výrazně snížit riziko útoků na webové stránky a zlepšit celkovou bezpečnost aplikace.

## Network protocols, TCP, DNS, BGP

Síťové protokoly jsou soubory pravidel a postupů, které umožňují komunikaci mezi počítači v síti. Tyto protokoly se používají pro přenos dat v rámci sítě a zajišťují bezpečnost a spolehlivost přenosu.

## TCP

TCP (Transmission Control Protocol) je jedním z nejpoužívanějších protokolů pro přenos dat v počítačových sítích. Tento protokol zajišťuje spolehlivý přenos dat mezi počítači a kontroluje, zda dorazila všechna data bez chyb.

## DNS

DNS (Domain Name System) je systém, který překládá doménová jména na IP adresy. Tento systém umožňuje počítačům v síti komunikovat s ostatními počítači pomocí doménových jmen, což je pro uživatele mnohem pohodlnější než používání IP adres.

## BGP

BGP (Border Gateway Protocol) je protokol, který se používá pro směrování dat mezi autonomními systémy (AS). Tento protokol zajišťuje, že data jsou směrována správným způsobem a že jsou doručena do cílové sítě.



V kontextu kybernetické bezpečnosti jsou tyto protokoly důležité pro zajištění bezpečnosti a spolehlivosti přenosu dat. Například útoky typu DDoS mohou být zaměřeny na síťové protokoly, jako je BGP, aby způsobily výpadek sítě. Útočníci mohou také využít chyby v TCP protokolu k útoku na počítačový systém. DNS pak může být cílem útoků typu DNS spoofing, kdy útočník změní odpověď DNS serveru tak, aby uživatel byl přesměrován na škodlivou stránku. Je tedy důležité zajistit bezpečnost těchto protokolů a sledovat jejich správnou funkci.

## Security of HTTPs

HTTPs je protokol pro zabezpečenou komunikaci mezi webovými servery a prohlížeči. Tento protokol zajišťuje šifrování dat, která jsou přenášena mezi serverem a prohlížečem, a tím chrání uživatele před útoky hackerů.

### **Jak funguje HTTPs?**

Když uživatel navštíví webovou stránku s protokolem HTTPs, jeho prohlížeč zašle požadavek na server, aby zahájil zabezpečenou komunikaci. Server poté odešle certifikát, který obsahuje veřejný klíč, který bude použit k šifrování dat. Prohlížeč ověří platnost certifikátu a poté zašifruje data pomocí veřejného klíče a odešle je zpět na server. Server poté dešifruje data pomocí svého soukromého klíče.

### **Výhody HTTPs**

- **Šifrování dat:** HTTPs zajišťuje šifrování dat, která jsou přenášena mezi serverem a prohlížečem, a tím chrání uživatele před útoky hackerů.

- **Důvěryhodnost:** HTTPs používá certifikáty, které jsou vydávány autorizovanými certifikačními autoritami, a tím zajišťuje důvěryhodnost webových stránek.

- **SEO výhody:** Google preferuje webové stránky s protokolem HTTPs a tyto stránky mají větší šanci na lepší pozice ve vyhledávačích.

### **Závěr**

HTTPs je důležitým nástrojem pro zabezpečení webových stránek a ochranu uživatelů před útoky hackerů. Použití HTTPs je dnes již standardem a každý majitel webové stránky by měl zajistit, aby jeho stránka byla chráněna touto technologií.

## Mechanism of certificates

Mechanismus certifikátů je klíčovým prvkem kybernetické bezpečnosti. Certifikáty jsou digitální identifikátory, které slouží k ověření totožnosti uživatele, serveru nebo aplikace. Certifikáty se vydávají certifikačními autoritami (CA) a obsahují informace o vlastníkovi, platnosti a veřejném klíči. 

Certifikáty umožňují šifrování komunikace mezi uživateli a serverem, což zajišťuje důvěrnost a integritu dat. Pokud uživatel obdrží certifikát od serveru, může se spolehnout na to, že komunikuje s legitimním serverem a že data jsou šifrována tak, aby nebyla čitelná pro neoprávněné osoby.

Pro správnou funkci certifikátů je důležité, aby byly správně vydávány, ověřovány a spravovány. Certifikační autority musí mít dostatečné zabezpečení a důvěryhodnost, aby se zabránilo podvržení certifikátů. Uživatelé musí být schopni ověřit platnost certifikátu a důvěryhodnost vydavatele.

Mechanismus certifikátů je klíčovým prvkem kybernetické bezpečnosti a je důležité, aby byl správně implementován a spravován, aby se minimalizovala rizika kybernetických útoků.

## Security of certificate infrastructure.

Certifikační infrastruktura (PKI) je systém, který umožňuje vydávat a ověřovat digitální certifikáty. Tyto certifikáty jsou klíčové pro zajištění bezpečného přenosu dat na internetu. Proto je důležité zajistit bezpečnost celé PKI.

### Hrozby pro certifikační infrastrukturu

Existuje několik způsobů, jak mohou být certifikační autority (CA) ohroženy:

- **Útoky na CA server**: Hackeři mohou zaútočit na server CA a ukrást privátní klíče, které jsou potřebné k vydávání certifikátů. Pokud útočník získá tyto klíče, může vydávat falešné certifikáty a provádět útoky typu man-in-the-middle.

- **Útoky na uživatele**: Útočníci mohou cílit na uživatele a získat jejich privátní klíče. Poté mohou vydávat falešné certifikáty a provádět útoky typu man-in-the-middle.

- **Útoky na certifikační řetězec**: Certifikační řetězec je řada certifikátů, které jsou použity k ověření identity webové stránky. Pokud útočník získá privátní klíč jedné z certifikačních autorit v řetězci, může vydávat falešné certifikáty a provádět útoky typu man-in-the-middle.

### Zabezpečení certifikační infrastruktury

Aby byla certifikační infrastruktura bezpečná, je nutné dodržovat několik zásad:

- **Bezpečné ukládání privátních klíčů**: Privátní klíče by měly být uchovávány v bezpečném prostředí, kde mají přístup pouze oprávněné osoby.

- **Bezpečné ověřování uživatelů**: Uživatelé by měli být ověřováni pomocí silných hesel a dvoufázové autentizace.

- **Kontrola certifikačního řetězce**: Certifikační řetězec by měl být pravidelně kontrolován a aktualizován, aby se minimalizovalo riziko útoků.

- **Šifrování přenosu dat**: Všechny přenosy dat by měly být šifrovány pomocí silného šifrovacího protokolu, jako je například TLS.

- **Pravidelné aktualizace a opravy**: Certifikační infrastruktura by měla být pravidelně aktualizována a opravována, aby se minimalizovalo riziko zneužití.

Dodržování těchto zásad je klíčové pro zajištění bezpečnosti certifikační infrastruktury a ochranu před útoky.

## Firewalls

Firewally jsou základním prvkem zabezpečení počítačových sítí. Jedná se o software nebo hardware, který slouží k ochraně sítě před neoprávněným přístupem. Firewall může blokovat nebo povolit přístup k určitým síťovým službám na základě definovaných pravidel.

### Typy firewalů

### Stavový firewall

Stavový firewall sleduje stav síťového spojení a umožňuje povolit přístup pouze k platným spojením. Tento typ firewallu je schopen rozpoznat, zda je spojení iniciováno z vnitřní nebo vnější sítě a podle toho povolit nebo blokovat přístup.

### Paketový firewall

Paketový firewall pracuje na úrovni síťového protokolu a umožňuje blokovat nebo povolit přenos jednotlivých paketů na základě definovaných pravidel. Tento typ firewallu je méně sofistikovaný než stavový firewall a může být snadno překonán pokročilejšími útoky.

### Aplikační firewall

Aplikační firewall pracuje na úrovni aplikace a umožňuje blokovat nebo povolit přístup k jednotlivým aplikacím nebo službám na základě definovaných pravidel. Tento typ firewallu je nejsofistikovanější a umožňuje detailní kontrolu nad síťovým provozem.

### Konfigurace firewallu

Správná konfigurace firewallu je klíčová pro úspěšné zabezpečení sítě. Firewall by měl být konfigurován tak, aby blokoval veškerý nevyžádaný síťový provoz a povoloval pouze provoz, který je nezbytný pro fungování sítě. Důležité je také pravidelně aktualizovat pravidla firewallu a sledovat jeho logy pro odhalení podezřelého síťového provozu.

## Network intrusion detection

Síťová detekce proniknutí (NID) je proces monitorování síťového provozu a hledání podezřelých aktivit, které by mohly naznačovat útok na síť. NID může být prováděno pomocí hardwarových zařízení nebo softwarových aplikací, které analyzují síťový provoz a hledají známky útoku.

Existuje několik typů NID, včetně detekce chování, detekce signatur a detekce anomálií. Detekce chování sleduje chování uživatelů a aplikací v síti a hledá podezřelé vzorce, jako jsou opakované pokusy o přihlášení nebo přístup k citlivým datům. Detekce signatur používá databázi známých útoků a hledá shodu mezi síťovým provozem a těmito známými útoky. Detekce anomálií sleduje neobvyklé vzorce v síťovém provozu a upozorňuje na podezřelé aktivity.

NID je důležitou součástí kybernetické bezpečnosti a pomáhá chránit organizace před útoky na síť. Správně nakonfigurovaný a spravovaný NID může identifikovat útoky včas a umožnit rychlou reakci na ně.

## Network intrusion prevention

Ochrana proti vniknutí do sítě (Network intrusion prevention) je důležitou součástí kybernetické bezpečnosti. Tato technologie slouží k detekci a prevenci neoprávněného přístupu do sítě. 

### Jak to funguje?

Systém ochrany proti vniknutí do sítě monitoruje provoz v síti a analyzuje ho na základě předem definovaných pravidel. Pokud je detekována podezřelá aktivita, systém aktivuje bezpečnostní opatření, jako je například blokování přístupu nebo varování správce sítě.

### Proč je to důležité?

Bez ochrany proti vniknutí do sítě mohou být počítače a další zařízení v síti ohroženy útoky, jako jsou například útoky typu Denial of Service (DoS) nebo ransomware. Tyto útoky mohou způsobit výpadek sítě, ztrátu dat a další škody.

### Závěr

Ochrana proti vniknutí do sítě je zásadní pro zajištění kybernetické bezpečnosti. Je důležité mít tuto technologii správně nakonfigurovanou a pravidelně aktualizovanou, aby byla schopna detekovat nové hrozby a bránit se jim.

Poznámka: V češtině se také často používá termín "prevence vniknutí do sítě".

## Thin client

Tenký klient je počítačový systém, který se používá pro přístup k centrálnímu serveru. Tento typ klienta nemá vlastní pevný disk ani většinu hardwarových komponentů, což znamená, že veškeré zpracování a ukládání dat se provádí na serveru. To znamená, že tenký klient je méně náchylný na útoky a viry, protože všechna data jsou uložena na centrálním serveru a ne na samotném klientovi.

V oblasti kybernetické bezpečnosti se tenký klient používá jako jedna z možností pro zabezpečení sítě. Protože všechna data jsou uložena na serveru, mohou být snadno monitorována a chráněna před neoprávněným přístupem. Tenké klienty také umožňují snadnou aktualizaci softwaru a zabezpečení, protože všechny změny se provádějí pouze na centrálním serveru.

Celkově lze říci, že tenký klient je užitečným nástrojem pro zabezpečení sítě a prevenci kybernetických útoků.

## Intrusion deflection

Odklon útoků (anglicky Intrusion deflection) je proces, při kterém se snažíme zabránit útokům na počítačové systémy. Tento proces se skládá z několika kroků:

1. Detekce útoku: Snažíme se identifikovat útoky, které jsou namířeny na naše systémy. K tomu můžeme použít různé nástroje, jako jsou například firewally, antiviry nebo systémy detekce anomálií.

2. Odpověď na útok: Jakmile identifikujeme útok, musíme na něj adekvátně reagovat. To může zahrnovat například blokování útočníka, uzavření bezpečnostních děr nebo obnovení dat ze zálohy.

3. Prevence budoucích útoků: Abychom minimalizovali riziko budoucích útoků, musíme zajistit, že jsou naše systémy dostatečně zabezpečené. To zahrnuje pravidelné aktualizace softwaru, silná hesla a další bezpečnostní opatření.

Odklon útoků je důležitou součástí kybernetické bezpečnosti a pomáhá chránit naše počítačové systémy před různými hrozbami, jako jsou například malware, phishing nebo DDoS útoky.


## Denial of service attack

Útok typu Denial of Service (DoS) je útok, kdy útočník záměrně přetíží cílový systém, aby byl nedostupný pro legitimní uživatele. Toho lze dosáhnout různými způsoby, například pomocí floodingu síťového provozu, útoků na protokoly nebo využitím zranitelností v softwaru.

### Druhy DoS útoků

- **Flooding útoky**: Útočník přetíží síťovou linku nebo server velkým množstvím nelegitimních datových paketů. To má za následek výpadek služeb a nedostupnost systému.

- **Spoofing útoky**: Útočník využívá zranitelností v síťových protokolech k tomu, aby posílal falešné nebo modifikované pakety, které vypadají jako legitimní. To může vést k výpadku služeb nebo k úniku citlivých informací.

- **Využití zranitelností**: Útočník využívá zranitelnosti v softwaru nebo hardware cílového systému k tomu, aby ho donutil spadnout nebo aby získal neoprávněný přístup.

### Ochrana proti DoS útokům

- **Monitorování sítě**: Monitorování síťového provozu může pomoci odhalit DoS útoky a umožnit rychlou reakci.

- **Firewally**: Firewally mohou být použity k blokování nelegitimního síťového provozu a ochraně proti DoS útokům.

- **Load balancing**: Load balancing může pomoci rozložit zátěž mezi více serverů a snížit tak riziko výpadku služeb.

- **Aktualizace softwaru**: Pravidelné aktualizace softwaru mohou pomoci snížit riziko využití zranitelností v softwaru.

- **Ochrana proti spoofingu**: Použití technologií, jako je například DNSSEC, může pomoci chránit proti spoofingu útokům.

- **Využití služeb DDoS ochrany**: Pokud je organizace vystavena vysokému riziku DoS útoků, může být využita služba DDoS ochrany, která poskytuje pokročilé nástroje pro detekci a obranu proti útokům.


## Reflection attacks

Reflection attacks or *reflected amplification attacks* are a type of DDoS attack where the attacker sends a request to a server with a spoofed IP address, and the server responds to the victim with a much larger response than the original request. This causes the victim to be overwhelmed with traffic, eventually leading to denial of service.

### **How does it work?**

1. The attacker sends a request to a server with a spoofed IP address.
2. The server responds to the request, but with a much larger response than the original request.
3. The victim receives the amplified response, overwhelming their system and causing denial of service.

### **Prevention**

1. Implement anti-spoofing measures to prevent attackers from using spoofed IP addresses.
2. Use traffic filtering to block traffic from known sources of reflection attacks.
3. Use rate limiting to limit the amount of traffic that can be sent to a server in a given time period.

## Syn-cookies
`Syn-cookies` jsou bezpečnostní opatření používaná v počítačových sítích k ochraně před útoky typu SYN flood. Tyto útoky jsou zaměřeny na přetížení sítě nebo serveru tím, že se zasílají velké množství SYN požadavků, které nejsou dokončeny, což vede ke ztrátě výkonu a výpadkům služeb.

`Syn-cookies` fungují tím, že místo ukládání SYN požadavků do paměti serveru, jsou informace o těchto požadavcích zakódovány do speciálního čísla, které je připojeno k odpovědi serveru na požadavek. Pokud je následující požadavek na server s tímto číslem, server rozpozná, že se jedná o platný požadavek a dokončí ho.

Tímto způsobem jsou `Syn-cookies` schopny odolat útokům typu SYN flood a zajistit, že server zůstane v provozu i při velkém množství požadavků.

## Detection and protection against DOS.

DOS (Denial of Service) útoky jsou útoky, které mají za cíl zahlcení služby nebo systému, což vede k nedostupnosti pro legitimní uživatele. Pro ochranu proti těmto útokům je důležité mít implementované následující opatření:

### Detekce DOS útoků

- Monitorování síťového provozu: Monitorování síťového provozu může odhalit anomálie v síťovém provozu, které mohou indikovat DOS útoky. Například velké množství paketů od jednoho zdroje nebo velké množství požadavků na konkrétní službu.
- Monitoring chování uživatelů: Monitorování chování uživatelů může odhalit neobvyklé chování, které může indikovat DOS útoky. Například uživatelé, kteří se snaží přistupovat ke službám, ke kterým nemají oprávnění.

### Ochrana proti DOS útokům

- Firewall: Firewall může blokovat síťový provoz, který je považován za DOS útok. Například může blokovat síťový provoz od konkrétního zdroje nebo síťový provoz s určitými charakteristikami.
- Load balancer: Load balancer může rovnoměrně rozdělovat síťový provoz mezi více serverů, což snižuje riziko DOS útoku, protože jeden server nemůže být zahlcen.
- Cloud-based security services: Cloud-based security services mohou poskytovat ochranu proti DOS útokům tím, že poskytují škálovatelnou infrastrukturu, která může odolat vysokému objemu síťového provozu.

Poznámka: V češtině se používá termín DoS útok (Denial of Service).