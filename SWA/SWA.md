# SWA

## Topics
Software architectures, their parameters and qualitative metrics. Architectural patterns,
styles and standards. BE4M36SWA (Course web pages)

## Questions
### Describe Krutchen's 4+1 View Model of a software architecture. Explain how it captures the complete behavior of a developed software from multiple perspectives of the system. How is this model aligned with the UML models?

#### Popis Krutchenova 4+1 View Modelu softwarov? architektury:

   - Pohled logick? (Logical View):
     - Zobrazuje t??dy, objekty, rozhran? a jejich vztahy
     - Zam??uje se na funkcionalitu syst?mu
   - Pohled procesn? (Process View):
     - Popisuje procesy a konkurenci v syst?mu
     - Zam??uje se na v?konnost, ?k?lovatelnost a stabilitu
   - Pohled fyzick? (Physical View):
     - Popisuje mapov?n? softwarov?ch komponent na hardware
     - Zam??uje se na nasazen? a distribuci syst?mu
   - Pohled v?vojov? (Development View):
     - Zobrazuje organizaci zdrojov?ho k?du, knihoven a komponent
     - Zam??uje se na spr?vu k?du a modul?rn? strukturu
   - Sc?n??e (Scenarios):
     - Uplat?uje se pro ov??en? a validaci n?vrhu architektury
     - Pom?h? prov?st pr??ez v?emi ?ty?mi pohledy

#### Jak 4+1 View Model zachycuje chov?n? softwaru z r?zn?ch perspektiv:

   - A. Logick? pohled (Logical View):
      - Poskytuje abstraktn? pohled na syst?m z hlediska funk?nosti
      - Umo??uje analyzovat a navrhovat statickou strukturu syst?mu
      - Pom?h? identifikovat t??dy, rozhran? a jejich vztahy
      - Slou?? k pochopen? dom?ny a funkc?, kter? syst?m poskytuje

   - B. Procesn? pohled (Process View):
      - Zkoum? chov?n? syst?mu z hlediska b?hov?ch proces? a vl?ken
      - Umo??uje identifikovat synchroniza?n? a komunika?n? aspekty mezi jednotliv?mi procesy
      - Pom?h? zaji??ovat ?k?lovatelnost, v?konnost a stabilitu syst?mu
      - Slou?? k anal?ze a ?e?en? probl?m? t?kaj?c?ch se konkurence a distribuce

   - C. Fyzick? pohled (Physical View):
      - Popisuje, jak jsou softwarov? komponenty nasazeny na hardwarov? prost?edky
      - Umo??uje ?e?it ot?zky t?kaj?c? se komunikace a propojen? mezi hardwarov?mi jednotkami
      - Pom?h? identifikovat potenci?ln? omezen? a probl?my v hardwarov? konfiguraci
      - Slou?? k optimalizaci nasazen? a distribuce syst?mu

   - D. V?vojov? pohled (Development View):
      - Zkoum? strukturu zdrojov?ho k?du, knihoven a modul?
      - Umo??uje identifikovat z?vislosti a propojen? mezi jednotliv?mi ??stmi k?du
      - Pom?h? zlep?ovat ?itelnost, udr?itelnost a modularitu k?du
      - Slou?? k usnadn?n? pr?ce v?voj??? a podpo?e t?mov? spolupr?ce

   - E. Sc?n??e (Scenarios):
      - P?edstavuj? konkr?tn? p??klady pou?it? syst?mu (use cases)
      - Umo??uj? ov??it a validovat n?vrh architektury
      - Pom?haj? identifikovat probl?my a nedostatky v n?vrhu
      - Slou?? k prov?d?n? pr??ez? mezi v?emi ?ty?mi pohledy a k integraci r?zn?ch aspekt? syst?mu

#### Souvislost mezi 4+1 View Model a UML modely:

UML diagramy pro 4+1 View Model:

1. Logick? pohled (Logical View):
    - T??dn? diagram (Class Diagram)
    - Objektov? diagram (Object Diagram)
    - Kompozi?n? struktura (Composite Structure Diagram)
    - Bal??kov? diagram (Package Diagram)

2. Procesn? pohled (Process View):
    - Diagram ?innost? (Activity Diagram)
    - Sekven?n? diagram (Sequence Diagram)
    - Diagram spolupr?ce (Collaboration Diagram)
    - Stavov? diagram (State Diagram)

3. Fyzick? pohled (Physical View):
    - Diagram nasazen? (Deployment Diagram)
    - Diagram komponent (Component Diagram)
    - Komunika?n? diagram (Communication Diagram)

4. V?vojov? pohled (Development View):
    - Bal??kov? diagram (Package Diagram)
    - Diagram komponent (Component Diagram)

Integrace UML s 4+1 View Model:
    - UML diagramy poskytuj? vizu?ln? reprezentaci pro ka?d? pohled v 4+1 View Modelu
    - Umo??uj? efektivn? komunikaci mezi architekty, v?voj??i, testery a dal??mi ?leny t?mu
    - Podporuj? anal?zu, n?vrh, implementaci a ?dr?bu syst?mu
    - Usnad?uj? kontrolu a ??zen? kvality architektury

### What is a software architecture? Describe the importance of software architecture when developing a system. What are the software architecture design guidelines? What are the architectural styles? Give an example of an architectural style and describe it in detail.

**Co je softwarov? architektura?**

- Softwarov? architektura je **struktura** a **organizace** softwarov?ho syst?mu.
- Zahrnuje **komponenty**, jejich **vlastnosti** a **vztahy** mezi nimi.
- Definuje **z?sady**, **sm?rnice** a **omezen?** pro v?voj syst?mu.

**D?le?itost softwarov? architektury p?i v?voji syst?mu:**

1. **Zaji?t?n? kvality**:
   - Architektura zaji??uje, ?e syst?m spl?uje **funk?n?** a **nefunk?n?** po?adavky.
2. **Usnadn?n? komunikace**:
   - Architektura slou?? jako **spole?n? jazyk** pro v?voj??e, z?kazn?ky a dal?? z??astn?n? strany.
3. **Podpora znovupou?itelnosti**:
   - Spr?vn? navr?en? architektura umo??uje **znovupou?it?** k?du a komponent.
4. **Zjednodu?en? rozhodov?n?**:
   - Architektura poskytuje **r?mcov? rozhodnut?** pro v?voj??e, kter? usnad?uje v?voj a ?dr?bu.
5. **??zen? rizik**:
   - Architektura pom?h? identifikovat a ?e?it **rizika** spojen? s v?vojem syst?mu.
6. **Zlep?en? v?konnosti**:
   - Architektura optimalizuje **v?konnost**, **?k?lovatelnost** a **stabilitu** syst?mu.

**Sm?rnice pro n?vrh softwarov? architektury:**

1. **Rozd?lit a vl?dnout**:
   - Syst?m rozd?lit na men??, snadno ?iditeln? komponenty.
2. **Abstrakce**:
   - Pou??t abstrakce pro zjednodu?en? slo?it?ch probl?m?.
3. **Modularita**:
   - Navrhnout nez?visl? a snadno zam?niteln? moduly.
4. **Zachov?n? informac?**:
   - Minimalizovat z?vislosti mezi komponentami.
5. **?k?lovatelnost**:
   - Umo?nit snadn? roz???en? syst?mu.
6. **Znovupou?itelnost**:
   - Navrhovat komponenty tak, aby byly znovupou?iteln?.
7. **Flexibilita**:
   - Umo?nit snadnou ?dr?bu a p?izp?soben? zm?n?m po?adavk?.

**Architektonick? styly:**

- Architektonick? styly jsou **vzory** nebo **paradigmata** pro n?vrh softwarov? architektury.

**P??klad architektonick?ho stylu: MVC (Model-View-Controller)**

1. **Model**:
   - Reprezentuje **data** a **byznysovou logiku** aplikace.
   - Nez?visl? na prezenta?n? vrstv? a u?ivatelsk?m rozhran?.
2. **View (Zobrazen?)**:
   - Zodpov?dn? za **prezentaci** a **zobrazen?** dat z modelu.
   - Aktualizuje se automaticky, kdy? se zm?n? data v modelu.
3. **Controller (Ovlada?)**:
   - Zodpov?dn? za **??zen?** interakce mezi modelem a zobrazen?m.
   - Zpracov?v? u?ivatelsk? vstupy a aktualizuje model nebo zobrazen?.

**Detaily architektonick?ho stylu MVC:**

- **Odd?len? z?jm?**: MVC odd?luje z?jmy aplikace do t?? komponent, co? usnad?uje ?dr?bu a roz???en?.
- **Znovupou?itelnost**: Model a Controller mohou b?t znovu pou?ity pro r?zn? zobrazen?.
- **Flexibilita**: Zm?ny v jedn? komponent? maj? minim?ln? dopad na ostatn? komponenty.

#### What is a design pattern? What problem are design patterns solving? What types of design patterns exist? Why is it important to know the design patterns? Are there design antipatterns?

**Co je n?vrhov? vzor (design pattern)?**

- N?vrhov? vzor je **opakovateln? ?e?en?** pro ?asto se vyskytuj?c? probl?my v oblasti softwarov?ho n?vrhu.
- Nen? to hotov? n?vrh, ale **?ablona** pro ?e?en? probl?mu, kterou lze p?izp?sobit konkr?tn?m situac?m.

**Jak? probl?m ?e?? n?vrhov? vzory?**

- N?vrhov? vzory ?e?? probl?my, kter? se vyskytuj? opakovan? p?i n?vrhu softwarov?ch syst?m?.
- Pom?haj? **zlep?it kvalitu** k?du, **usnadnit komunikaci** mezi v?voj??i a **urychlit v?voj**.

**Typy n?vrhov?ch vzor?:**

1. **Vzory pro tvorbu objekt? (Creational Patterns)**:
   - ?e?? probl?my spojen? s procesem vytv??en? objekt?.
   - P??klady: Singleton, Factory Method, Abstract Factory, Builder, Prototype.
2. **Struktur?ln? vzory (Structural Patterns)**:
   - ?e?? probl?my t?kaj?c? se kompozice t??d a objekt?.
   - P??klady: Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy.
3. **Vzory chov?n? (Behavioral Patterns)**:
   - ?e?? probl?my interakce mezi objekty a zp?soby, jak?mi spolupracuj?.
   - P??klady: Chain of Responsibility, Command, Interpreter, Iterator, Mediator, Memento, Observer, State, Strategy, Template Method, Visitor.

**D?le?itost znalosti n?vrhov?ch vzor?:**

1. **Zlep?en? kvality k?du**:
   - N?vrhov? vzory poskytuj? osv?d?en? ?e?en?, kter? zvy?uj? kvalitu k?du.
2. **Zv??en? efektivity v?voje**:
   - Pou?it?m n?vrhov?ch vzor? lze urychlit v?voj a sn??it chybovost.
3. **Usnadn?n? komunikace mezi v?voj??i**:
   - N?vrhov? vzory slou?? jako spole?n? jazyk, kter? usnad?uje komunikaci a porozum?n? mezi v?voj??i.
4. **Zjednodu?en? ?dr?by**:
   - N?vrhov? vzory usnad?uj? ?dr?bu a roz?i?ov?n? k?du d?ky jejich zn?m? struktu?e a princip?m.
5. **Podpora znovupou?itelnosti**:
   - N?vrhov? vzory podporuj? znovupou?itelnost k?du t?m, ?e umo??uj? snadn?j?? integraci a adaptaci k?du.

**Existuj? n?vrhov? antivzory (design antipatterns)?**

- Ano, n?vrhov? antivzory existuj?.
- Jsou to **?patn? ?e?en?** nebo **protip??klady** dobr?ch n?vrhov?ch vzor?.
- N?vrhov? antivzory mohou v?st ke **?patn? navr?en?mu**, **t??ko udr?iteln?mu** a **neefektivn?mu** k?du.
- Je d?le?it? rozpoznat a vyh?bat se n?vrhov?m antivzor?m, aby byla zaji?t?na dobr? kvalita k?du a efektivn? v?voj.

#### What is a microservice architecture? What are its advantages and disadvantages compared to a monolithic architecture. How is microservices development different from developing a monolithic application? Are there any methodologies or guidelines or best practices to follow when developing microservices? Obviously, there are patterns that can be applied in this area, are there any antipatterns that should be avoided?

**Co je mikroservisn? architektura?**

- Mikroservisn? architektura je **p??stup k v?voji softwaru**, kter? rozd?luje aplikaci na **mal?, nez?visl? slu?by**.
- Tyto slu?by komunikuj? pomoc? **lehk?ch protokol?** (nap?. REST nebo gRPC) a maj? vlastn? **datab?ze** a **konfigurace**.

**V?hody a nev?hody mikroservisn? architektury oproti monolitick? architektu?e:**

**V?hody:**

1. **Lehk? ?k?lovatelnost**:
   - Mikroservisy lze ?k?lovat nez?visle na ostatn?ch slu?b?ch.
2. **Snadn?j?? ?dr?ba**:
   - Men?? a jednodu??? k?dov? z?kladna usnad?uje ?dr?bu a roz?i?ov?n?.
3. **Rychlej?? nasazen?**:
   - Mikroservisy lze nasazovat nez?visle, co? urychluje v?vojov? cyklus.
4. **Technologick? agilita**:
   - Ka?d? slu?ba m??e pou??vat jin? technologie, co? umo??uje snadn?j?? inovace.
5. **Odolnost v??i chyb?m**:
   - Selh?n? jedn? slu?by m? men?? dopad na cel? syst?m.

**Nev?hody:**

1. **Slo?itost**:
   - V?t?? po?et komponent a interakc? mezi nimi zvy?uje slo?itost syst?mu.
2. **V?kon**:
   - Komunikace mezi slu?bami m??e b?t pomalej?? ne? u monolitick? architektury.
3. **Spr?va a monitorov?n?**:
   - Spr?va a sledov?n? mnoha nez?visl?ch slu?eb m??e b?t n?ro?n?.
4. **Distribuovan? transakce**:
   - ?e?en? distribuovan?ch transakc? m??e b?t komplikovan?j?? ne? v monolitick?ch aplikac?ch.

**Jak se v?voj mikroservis? li?? od v?voje monolitick? aplikace?**

1. **Rozd?len? aplikace**:
   - Aplikace je rozd?lena na men??, nez?visl? slu?by.
2. **Komunikace mezi slu?bami**:
   - Mikroservisy komunikuj? pomoc? API a lehk?ch protokol?.
3. **Datab?ze a konfigurace**:
   - Ka?d? slu?ba m? vlastn? datab?zi a konfiguraci.
4. **Nez?visl? nasazen?**:
   - Mikroservisy mohou b?t nasazeny a ?k?lov?ny nez?visle.
5. **Technologick? diverzita**:
   - Ka?d? slu?ba m??e pou??vat jin? technologie, co? umo??uje snadn?j?? inovace.
6. **Spr?va a monitorov?n?**:
   - Vy?aduje n?stroje a postupy pro spr?vu a sledov?n? mnoha nez?visl?ch slu?eb.
7. **Distribuovan? transakce**:
   - ?e?en? distribuovan?ch transakc? m??e b?t komplikovan?j?? ne? v monolitick?ch aplikac?ch.

**Metodiky, sm?rnice a osv?d?en? postupy pro v?voj mikroservis?:**

1. **Rozd?lit a vl?dnout**:
   - Aplikaci rozd?lit na men??, nez?visl? a snadno ?iditeln? slu?by.
2. **Definice rozhran? (API)**:
   - Navrhnout jasn? a stabiln? API pro komunikaci mezi slu?bami.
3. **Odd?len? z?jm?**:
   - Ka?d? slu?ba by m?la m?t jednu zodpov?dnost a ?e?it jeden aspekt byznysu.
4. **Decentralizace spr?vy dat**:
   - Ka?d? slu?ba by m?la m?t svou vlastn? datab?zi a spravovat sv? data nez?visle.
5. **Stavov? nez?vislost**:
   - Preferovat bezestavov? slu?by, kter? neuchov?vaj? stav mezi po?adavky.
6. **Automatizace nasazen? a ?k?lov?n?**:
   - Pou??vat n?stroje a postupy pro automatick? nasazen? a ?k?lov?n? slu?eb.
7. **Monitorov?n? a sledov?n?**:
   - Implementovat monitorov?n?, sledov?n? a protokolov?n? pro snadnou detekci a ?e?en? probl?m?.
8. **Resilience a tolerov?n? selh?n?**:
   - Navrhnout slu?by tak, aby byly schopny zotavit se z chyb a pokra?ovat v provozu.
9. **Bezpe?nost**:
   - Zabezpe?it komunikaci mezi slu?bami a chr?nit citliv? data.
10. **Kontejnerizace a orchestrace**:
    - Pou??vat kontejnery (nap?. Docker) a orchestr?tory (nap?. Kubernetes) pro snadnou spr?vu a ?k?lov?n?.

**Antivzory, kter?m by se m?lo vyhnout p?i v?voji mikroservis?:**

1. **Nedostate?n? rozd?len? slu?eb**:
   - P??li? velk? nebo p??li? mal? slu?by mohou v?st k probl?m?m se ?k?lovatelnost? a ?dr?bou.
2. **Nadbyte?n? komunikace mezi slu?bami**:
   - P??li? mnoho vz?jemn? komunikace mezi slu?bami m??e v?st k probl?m?m s v?konem a slo?itosti.
3. **Centr?ln? spr?va dat**:
   - Spol?h?n? na jednu centr?ln? datab?zi pro v?echny slu?by m??e v?st k probl?m?m se ?k?lovatelnost? a nez?vislost? slu?eb.
4. **Synchronn? komunikace**:
   - Nadm?rn? pou?it? synchronn? komunikace m??e zp?sobit v?konnostn? probl?my a z?vislost mezi slu?bami.
5. **Nedostate?n? monitorov?n? a sledov?n?**:
   - Absence monitorov?n? a sledov?n? m??e zt??it detekci a ?e?en? probl?m?.
6. **Nedostate?n? bezpe?nost**:
   - Nedostatek zabezpe?en? mezi slu?bami nebo nedbalost p?i ochran? dat m??e v?st k zranitelnostem.
7. **V?voj monolitu v mikroservis?ch**:
   - P??stup k v?voji mikroservis?, kter? zachov?v? ?patn? n?vyky z monolitick?ho v?voje, m??e zp?sobit v?konnostn? a ?dr?bov? probl?my.
8. **Nedostate?n? automatizace nasazen? a ?k?lov?n?**:
   - Ru?n? nasazen? a ?k?lov?n? slu?eb m??e v?st k chyb?m a zpomalit v?voj.
9. **Zanedb?v?n? kontejnerizace a orchestrace**:
   - Neu??v?n? kontejner? a orchestr?tor? m??e zt??it spr?vu a ?k?lov?n? mikroservis?.
10. **Nedostate?n? dokumentace a komunikace**:
    - ?patn? zdokumentovan? nebo nekomunikovan? zm?ny mohou v?st k nedorozum?n?m a chyb?m mezi t?my.

#### Software architects can choose one architecture over another. The choice may affect the quality of the final product. Can you tell if one architecture is better than another or if one architecture is bad while the other is not? How can you measure the quality of an architecture? Can you measure the quality from different perspectives?

P?i v?b?ru softwarov? architektury je t??k? ??ci, ?e jedna architektura je obecn? lep?? ne? druh?, proto?e jejich vhodnost z?vis? na konkr?tn?ch po?adavc?ch a omezen?ch projektu. P?i v?b?ru architektury je d?le?it? zv??it n?sleduj?c? faktory:

1. **Po?adavky na v?kon**:
   - N?kter? architektury mohou l?pe podporovat vysok? v?kon ne? jin?, nap??klad distribuovan? syst?my pro ?k?lov?n?.

2. **?k?lovatelnost**:
   - Zvolen? architektura by m?la umo??ovat snadn? ?k?lov?n? a roz?i?ov?n? aplikace, aby bylo mo?n? l?pe ?e?it r?st z?t??e.

3. **Flexibilita a roz?i?itelnost**:
   - Architektura by m?la umo??ovat snadn? p?id?v?n? nov?ch funkc? a integraci s dal??mi syst?my.

4. **Bezpe?nost**:
   - D?le?it? je zv??it, jak dob?e architektura ?e?? bezpe?nostn? hrozby a zabezpe?uje citliv? data.

5. **?dr?ba a evoluce**:
   - Architektura by m?la usnad?ovat ?dr?bu a umo??ovat snadnou adaptaci na zm?ny v po?adavc?ch nebo technologi?ch.

6. **N?klady a zdroje**:
   - Je t?eba zohlednit dostupn? zdroje, jako je ?as, rozpo?et a lidsk? zdroje, a zv??it n?klady na v?voj, provoz a ?dr?bu.

7. **Kompatibilita s technologiemi**:
   - Zvolen? architektura by m?la b?t kompatibiln? s technologiemi, kter? t?m ji? pou??v?, nebo kter? pl?nuje pou??t.

8. **T?mov? zku?enost a dovednosti**:
   - Je d?le?it? zv??it zku?enosti a dovednosti t?mu a jak dob?e se dok??ou vyrovnat s n?roky zvolen? architektury.

P?i v?b?ru architektury je d?le?it? zv??it v?echny tyto faktory a zvolit takovou, kter? nejl?pe vyhovuje konkr?tn?m pot?eb?m a omezen?m projektu. Nen? ??dn? univerz?ln? "?patn?" nebo "lep??" architektura; m?sto toho je t?eba posoudit, jak? architektura je nejvhodn?j?? pro dan? projekt.

**M??en? kvality architektury:**

Kvalitu softwarov? architektury lze m??it pomoc? n?kolika metrik a z r?zn?ch perspektiv. N?kter? z t?chto perspektiv zahrnuj?:

1. **V?kon**:
   - M??en?, jak rychle a efektivn? architektura zvl?d? po?adavky, nap?. doba odezvy, pr?chodnost a latence.
   
2. **?k?lovatelnost**:
   - Hodnocen?, jak snadno m??e architektura r?st, aby vyhov?la rostouc?m po?adavk?m, a jak dob?e se p?izp?sobuje zm?n?m v z?t??i.

3. **Flexibilita a roz?i?itelnost**:
   - Ur?en?, jak snadno m??e b?t architektura roz???ena nebo upravena pro nov? funkce nebo integraci s dal??mi syst?my.

4. **Bezpe?nost**:
   - Hodnocen?, jak dob?e architektura zabezpe?uje citliv? data a chr?n? p?ed bezpe?nostn?mi hrozbami.

5. **Spolehlivost a odolnost**:
   - M??en?, jak dob?e architektura zvl?d? selh?n? a chyby, a jak rychle se dok??e zotavit.

6. **?dr?ba a evoluce**:
   - Hodnocen?, jak snadno m??e b?t architektura udr?ov?na a aktualizov?na, aby vyhovovala zm?n?m v po?adavc?ch a technologi?ch.

7. **Modularita a odd?len? z?jm?**:
   - Ur?en?, jak dob?e je architektura rozd?lena do samostatn?ch, snadno spravovateln?ch a znovupou?iteln?ch komponent.

8. **Testovatelnost**:
   - Hodnocen?, jak snadno lze architekturu testovat a validovat pro zaji?t?n? kvality a spolehlivosti.

Ka?d? z t?chto perspektiv nab?z? odli?n? metriky a hodnocen? kvality architektury. Pro m??en? kvality architektury je t?eba zv??it v?echny tyto aspekty a ur?it, jak? metriky jsou nejrelevantn?j?? pro konkr?tn? projekt a jeho po?adavky.