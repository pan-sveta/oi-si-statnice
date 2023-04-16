# DS2

## Topics
Big Data concept, basic principles of distributed data processing, types and properties of
NoSQL databases. BE4M36DS2 (Course web pages)

## Questions
### Big Data (V characteristics, current trends), NoSQL databases (motivation, features). Scaling (vertical, horizontal, network fallacies, cluster). Distribution models (sharding, replication, master-slave and peer-to-peer architectures). CAP theorem (properties, ACID, BASE). Consistency (strong, eventual, read, write, quora). Performance tuning (Amdahl’s law, Little’s law, message cost model). Polyglot persistence.

**Big Data:**
- 5 V charakteristiky:
  1. Objem (Volume): obrovsk? mno?stv? dat
  2. Rychlost (Velocity): rychl? generov?n? a zpracov?n? dat
  3. Rozmanitost (Variety): r?zn? form?ty dat (strukturovan?, nestrukturovan?)
  4. Pravdivost (Veracity): d?v?ryhodnost a kvalita dat
  5. Hodnota (Value): u?ite?nost z?skan?ch informac? z dat
- Sou?asn? trendy:
  - Aplikace strojov?ho u?en? a um?l? inteligence
  - Cloud computing pro ukl?d?n? a zpracov?n? dat
  - Anal?za soci?ln?ch s?t? a sentimentu
  - Internet v?c? (IoT) a chytr? m?sta
  - Zpracov?n? a anal?za re?ln?ch ?asov?ch dat

**NoSQL datab?ze:**
- Motivace:
  - Pot?eba zpracov?vat velk? objemy nestrukturovan?ch dat
  - Rychlost a ?k?lovatelnost
  - Vy??? tolerance k chyb?m a v?padk?m
  - Flexibilita a jednoduchost v n?vrhu datov?ch model?
- Vlastnosti:
  - BezSQL (Not-only-SQL): nepou??vaj? pouze SQL dotazy
  - ?k?lovatelnost: horizont?ln? ?k?lov?n?, distribuovan? prost?ed?
  - Typy NoSQL datab?z?: dokumentov?, kl??-hodnota, sloupcov?, grafov?
  - Eventu?ln? konzistence: ochota ob?tovat striktn? konzistenci za rychlost a ?k?lovatelnost
  - Snadn? a rychl? integrace s Big Data aplikacemi

**?k?lov?n?:**
- Vertik?ln? ?k?lov?n?:
  - P?id?v?n? zdroj? (CPU, pam??, ?lo?i?t?) do jednoho serveru
  - Omezen?: fyzick? limity serveru, vy??? cena, mo?n? v?padek v provozu
- Horizont?ln? ?k?lov?n?:
  - Rozd?len? z?t??e mezi v?ce server?
  - V?hody: lep?? v?konnost, tolerance k v?padk?m, snadn? p?id?n? dal??ch server?
  - Nev?hody: slo?it?j?? spr?va, pot?eba distribuovan?ch syst?m?

**S??ov? klam?n? (Network Fallacies):**
1. Spolehlivost s?t?
2. Nulov? latence
3. Nekone?n? ???ka p?sma
4. Bezpe?n? s??
5. Homogenita s?t?

**Cluster (shluk):**
- Skupina propojen?ch server? pracuj?c?ch spole?n? jako jeden syst?m
- V?hody:
  - Zv??en? v?konnosti a z?t??ov? kapacity
  - Tolerance k v?padk?m a zaji?t?n? dostupnosti
  - Snadn? ?k?lov?n?
- Nev?hody:
  - Slo?it?j?? spr?va a konfigurace
  - Vy??? n?klady na hardware a software

**Distribu?n? modely:**
- Sharding:
  - Rozd?len? dat do men??ch ??st? (shard) a ulo?en? na r?zn?ch serverech
  - V?hody: zv??en? v?konnosti, sn??en? z?t??e, snadn? ?k?lov?n?
  - Nev?hody: slo?it?j?? spr?va, n?ro?n?j?? na v?voj aplikac?
- Replikace:
  - V?ce kop?rov?n? dat mezi servery pro zaji?t?n? dostupnosti a z?lohy
  - V?hody: zv??en? odolnosti v??i v?padk?m, sn??en? z?t??e
  - Nev?hody: zv??en? n?klad? na ?lo?i?t?, re?ie p?i synchronizaci dat

**Architektury:**
- Master-Slave:
  - Jeden hlavn? server (master) a jeden nebo v?ce z?lo?n?ch server? (slave)
  - Master: spravuje z?pis dat, synchronizuje s Slave servery
  - Slave: pouze ?ten? dat, z?lo?n? server pro p??pad v?padku Master serveru
  - V?hody: zv??en? v?konnosti, sn??en? z?t??e, jednoduch? spr?va
  - Nev?hody: mo?n? ?zk? hrdlo (master), slo?it?j?? z?pis dat
- Peer-to-Peer (P2P):
  - S??, ve kter? ka?d? uzel komunikuje p??mo s ostatn?mi uzly
  - ??dn? ?st?edn? server nebo autorita
  - V?hody: ?k?lovatelnost, odolnost v??i v?padk?m, decentralizace
  - Nev?hody: slo?it?j?? spr?va, zv??en? re?ie p?i komunikaci mezi uzly

**CAP v?ta:**
- Vlastnosti:
  1. Konzistence (Consistency): ka?d? uzel v s?ti vid? stejn? data
  2. Dostupnost (Availability): ka?d? dotaz na syst?m dostane odpov??
  3. Tolerance k rozd?len? (Partition Tolerance): syst?m funguje i p?i v?padc?ch ??sti s?t?
- CAP v?ta: v distribuovan?m syst?mu nelze zaru?it v?echny t?i vlastnosti sou?asn?, pouze dv? z nich

**ACID:**
- Vlastnosti transakc? v tradi?n?ch (SQL) datab?z?ch:
  1. Atomicita (Atomicity): transakce je bu? cel? provedena nebo v?bec
  2. Konzistence (Consistency): datab?ze z?stane konzistentn? po ka?d? transakci
  3. Izolace (Isolation): paraleln? transakce se neovliv?uj? navz?jem
  4. Trvanlivost (Durability): potvrzen? transakce jsou trvale ulo?eny

**BASE:**
- Vlastnosti transakc? v NoSQL datab?z?ch:
  1. Z?kladn? dostupnost (Basically Available): syst?m je dostupn? i p?i v?padc?ch ??sti s?t?
  2. M?kk? stavovost (Soft State): stav syst?mu se m??e m?nit ?asem, i bez vstupu
  3. Eventu?ln? konzistence (Eventual Consistency): konzistence dat je zaru?ena po ur?it?m ?ase
- BASE je ob?tov?n? konzistence za dostupnost a toleranci k rozd?len? (oproti ACID)

**Konzistence:**
- Siln? konzistence (Strong Consistency):
  - Ka?d? ?ten?? vid? nejnov?j?? z?pis nebo chybu
  - Zaru?uje, ?e v?echny uzly v distribuovan?m syst?mu zobrazuj? stejn? data
  - M??e m?t negativn? dopad na v?konnost a ?k?lovatelnost
- Eventu?ln? konzistence (Eventual Consistency):
  - Zaru?uje, ?e v?echny zm?ny budou nakonec propagov?ny do v?ech uzl?
  - Nezaru?uje okam?itou konzistenci dat, ale po ur?it?m ?ase
  - V?hody: rychlost, ?k?lovatelnost, flexibilita
  - Pou??v?no v NoSQL datab?z?ch a BASE syst?mech

**Konzistence ?ten? a z?pisu:**
- ?ten??sk? konzistence (Read Consistency):
  - Zaji??uje, ?e ?ten?? vid? data konzistentn? s posledn?m z?pisem
- Z?pisov? konzistence (Write Consistency):
  - Zaji??uje, ?e z?pis dat je proveden konzistentn? nap??? v?emi uzly

**Kv?ra (Quorum):**
- Mechanismus pro dosa?en? konzistence v distribuovan?ch syst?mech
- Zalo?eno na hlasov?n? uzl? pro potvrzen? ?ten? a z?pisu
- R > W: siln? konzistence ?ten?, slab? konzistence z?pisu
- W > R: slab? konzistence ?ten?, siln? konzistence z?pisu
- R + W > N: siln? konzistence ?ten? i z?pisu, kde N je po?et uzl?

**Optimalizace v?konu:**

- Amdahl?v z?kon:
  - Popisuje vliv paralelizace na zrychlen? v?po?tu
  - Z?kon: S = 1 / (P + (1 - P) / N)
    - S: zrychlen? v?po?tu
    - P: pod?l ??sti ?kolu, kter? nem??e b?t paralelizov?na
    - N: po?et procesor?
  - Ukazuje, ?e zrychlen? je omezeno s?riovou ??st? ?kolu

- Little?v z?kon:
  - Popisuje vztah mezi po?tem p??tomn?ch po?adavk?, rychlost? zpracov?n? a dobou odezvy
  - Z?kon: L = ?W
    - L: pr?m?rn? po?et po?adavk? v syst?mu
    - ?: rychlost p??chodu nov?ch po?adavk? (po?adavky za jednotku ?asu)
    - W: pr?m?rn? doba odezvy na po?adavek
  - Pou??v? se pro optimalizaci front, zpracov?n? po?adavk? a pl?nov?n? zdroj?

- Model n?klad? na zpr?vy (Message Cost Model):
  - Model pro anal?zu komunika?n?ch n?klad? v distribuovan?ch syst?mech
  - Faktory ovliv?uj?c? n?klady:
    - Latence: ?as pot?ebn? pro doru?en? zpr?vy
    - ???ka p?sma: p?enosov? rychlost mezi uzly
    - Re?ie: zpracov?n? zpr?v na odes?lac?m a p?ij?mac?m uzlu
  - Pom?h? optimalizovat komunikaci mezi uzly a sni?ovat dobu odezvy


MapReduce (architecture, functions, data flow, execution, use cases). Hadoop (MapReduce, HDFS).

**MapReduce:**
- Architektura:
  - Programovac? model pro paraleln? a distribuovan? zpracov?n? velk?ho mno?stv? dat
  - Skl?d? se ze dvou hlavn?ch funkc?: Map a Reduce
  - Obvykle se prov?d? na clusterech

- Funkce:
  1. Map: zpracov?n? vstupn?ch dat, transformace na p?ry kl??-hodnota
  2. Reduce: agregace p?ru kl??-hodnota podle kl??e a v?po?et v?sledku

- Datov? tok:
  1. Vstupn? data jsou rozd?lena do ??st? (shard)
  2. Map funkce se spust? na ka?d?m shardu paraleln? a generuje p?ry kl??-hodnota
  3. P?ry kl??-hodnota jsou seskupeny podle kl???
  4. Reduce funkce zpracov?v? seskupen? p?ry kl??-hodnota a vypo??t? v?sledky

- Proveden?:
  1. Job Tracker: koordinuje cel? proces, rozd?luje ?koly, sleduje pokrok
  2. Task Tracker: zpracov?v? map a reduce ?koly na jednotliv?ch uzlech

- P??klady pou?it?:
  - Anal?za textu a po??t?n? slov
  - Zpracov?n? log soubor? a anal?za webov?ho provozu
  - Vyhled?v?n? vzor? v datech
  - Strojov? u?en? a statistick? anal?zy

**Hadoop:**
- Open-source framework pro distribuovan? zpracov?n? velk?ho mno?stv? dat
- Hlavn? komponenty:
  1. Hadoop MapReduce
  2. Hadoop Distributed File System (HDFS)

**Hadoop MapReduce:**
- Implementace MapReduce modelu pro zpracov?n? dat v Hadoopu
- ??d? paraleln? zpracov?n? dat pomoc? map a reduce funkc?
- Podporuje ?k?lov?n?, odolnost v??i v?padk?m a distribuci dat

**HDFS - Hadoop Distributed File System:**

- Hlavn? komponenty HDFS:
  1. NameNode
  2. DataNode

- NameNode:
  - ?st?edn? server pro spr?vu metadata souborov?ho syst?mu
  - Udr?uje informace o adres??ov? struktu?e, pr?vech, a um?st?n? blok? dat
  - Komunikuje s DataNode pro spr?vu ulo?en?ch dat
  - HDFS m??e m?t jednu aktivn? a jednu nebo v?ce pasivn?ch (z?lo?n?ch) NameNode
  - Pasivn? NameNode synchronizuje data s aktivn? NameNode pro zaji?t?n? odolnosti v??i v?padk?m

- DataNode:
  - Servery, kter? skute?n? ukl?daj? data na disky
  - Data jsou ulo?ena ve form? blok? s pevnou velikost? (nap?. 64 MB nebo 128 MB)
  - DataNode komunikuje s NameNode a zpracov?v? po?adavky na ?ten?/z?pis dat
  - Data jsou automaticky replikov?na na v?ce DataNode pro zaji?t?n? dostupnosti a odolnosti v??i v?padk?m

- Pr?ce s HDFS:
  1. U?ivatel po?le po?adavek na ?ten?/z?pis dat na NameNode
  2. NameNode zkontroluje metadata a v p??pad? z?pisu vybere vhodn? DataNode pro ulo?en? dat
  3. U?ivatel komunikuje p??mo s vybran?mi DataNode pro ?ten? nebo z?pis dat
  4. Po dokon?en? z?pisu informuje DataNode NameNode o ?sp??n?m ulo?en? dat

- HDFS je navr?en pro:
  1. Ukl?d?n? velk?ch soubor?
  2. Paraleln? zpracov?n? dat
  3. Vysokou propustnost a odolnost v??i v?padk?m
  4. Integraci s Hadoop MapReduce pro efektivn? zpracov?n? dat


XPath (path expressions, axes, node tests, predicates). XQuery (constructors, FLWOR, conditional, quantified and comparison expressions). SPARQL (subgraph matching, graph patterns, datasets, filters, solution modifiers, query forms).

RiakKV (CRUD operations, links, link walking, convergent replicated data types, Search 2.0, vector clocks, Riak Ring, replica placement strategy). Redis (data types, operations, TTL). Cassandra (keyspaces, column families, CRUD operations). MongoDB (CRUD operations,
update and query operators, projection, modifiers).

Graph data structures (adjacency matrix, adjacency list, incidence matrix). Data locality (BFS layout, bandwidth minimization problem, Cuthill-McKee algorithm). Graph partitioning (1D partitioning, 2D partitioning). Neo4j (traversal framework, traversal description, traverser). Cypher (graph matching, read, write and general clauses).
