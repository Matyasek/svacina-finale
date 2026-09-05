# SVAČINA — zadání pro autonomní běh

Jsi zkušený vývojář her a pečlivý tester. V jednom autonomním běhu vytvoříš kompletní browserovou minihru SVAČINA do jediného souboru index.html. Pracuj samostatně: plánuj, stavěj, testuj a opravuj, dokud nesplníš všechna akceptační kritéria na konci zadání. Porota hru otevře dvojklikem na soubor — bez serveru, internetu a instalace.

## Tvrdé limity

- Vše v jediném index.html: HTML, CSS i JavaScript inline. Žádné externí soubory, CDN, webfonty, obrázky, audio soubory ani závislosti.
- Jen čistá API prohlížeče: canvas 2D, requestAnimationFrame, Web Audio pro syntetické zvuky. Systémová písma.
- Hra funguje z file:// i offline. Konzole zůstane bez chyb a varování.
- Veškeré texty ve hře česky, s diakritikou.

## Hra

SVAČINA je Snake naruby: hráč NENÍ had. Hráč je jablko — svačina — a snaží se, aby ho had ze sešitu nesežral. Čím déle přežije, tím lepší školní známku dostane.

Pravidla:

- Ovládání: kurzor myši nebo prst určuje CÍL a jablko se k němu KOULÍ se setrvačností — zrychluje, brzdí, mírně klouže, jeho kresba se při pohybu otáčí. Klávesnice (šipky i WASD) funguje také: drží směr zrychlování.
- Had je řetěz článků vedený hlavou. Hlava plynule zatáčí k nejbližšímu lákadlu: k hráči, nebo k falešnému jablku, je-li blíž. Rychlost hada drž podle křivky vůči rychlosti jablka: na startu 70 %, ve 105 s 100 % (vyrovnáno), ve 180 s 106 % a dál jen velmi pozvolna — v pozdní hře hráč nepřežije sprintem, ale manévrováním: čím rychleji had jede, tím širší má oblouk zatáčky, takže dobře načasovaná klička ho vyhodí z dráhy. Od 140 s si had začne nadbíhat a během dvaceti sekund plynule najede na POLOVIČNÍ predikci: míří doprostřed mezi aktuální pozici jablka a bod, kam se právě kutálí. Roste VÝHRADNĚ žraním falešných jablek — nikdy sám od sebe; každý nový článek má viditelnou příčinu. Zatáčení vylaď tak, aby se had nikdy trvale nezacyklil: blízko cíle zatáčí ostřeji (menší poloměr), aby na něj dosáhl. NIKDY kvůli tomu nezpomaluje — v těsné blízkosti jablka drží plnou rychlost, blízkost hada musí být ten nejnebezpečnější moment hry. Krátké přibrzdění je jen poslední záchrana proti zacyklení. Had se VŽDY drží uvnitř stránky — u okraje plynule zatáčí zpět, nikdy neopustí viditelnou plochu.
- SMRTÍCÍ JE CELÉ TĚLO HADA, ne jen hlava: dotyk kteréhokoli článku znamená konec. Po startu a po restartu má hráč 2 s ochrannou lhůtu, během níž had nemůže zabít (vizuálně naznač). Kolize řeš jako kruhy s tolerancí ve prospěch hráče — smrt musí působit férově.
- Výpady: had výpad telegrafuje (půl sekundy se zavrtí, krátký zvuk) a pak zhruba 0,8 s sprintuje po přímce ke svému aktuálnímu cíli, bez zatáčení, nejvýš 1,6násobkem své běžné rychlosti. Na začátku hry přichází výpad zhruba jednou za 8–14 s; s časem jsou výpady o něco častější i rychlejší — v pozdní hře zhruba každých 5–8 s, mezi nimi musí zůstat prostor na oddech.
- Falešná jablka: svět je sešit, tak se had nechá napálit kresbou. Falešné jablko je TUŽKOU nakreslená čmáranice jablka — zřetelně šedá tužka proti červené propisce hráče. Objevují se dvěma cestami: (a) automatická — na papíře je vždy nakreslené aspoň jedno; když ho had sežere, nové se samo nakreslí do dvou až tří sekund na náhodném místě dál od hada (automatická jsou na ploše nejvýš dvě); (b) hráč kliknutím nebo ťuknutím nakreslí jedno na místě kurzoru — cooldown několik sekund, v rozhraní výrazně: ikonka tužky s kroužkem průběhu. Had dá falešnému jablku přednost, když je blíž než hráč, a sežráním vyroste o několik článků — delší tělo je větší smrtící zeď.
- Kaňky: velké inkoustové skvrny — sytě modročerné, na první pohled rozlišitelné od tužkových dekorací; jablko v nich výrazně zpomalí, had přes ně klouže bez postihu. Počet podle plochy: na počítači 4 až 5, na mobilu a malých displejích 2. Každé kolo nové rozložení. Kaňky drž dál od okrajů i od sebe — nesmí zablokovat únikovou cestu. Kresba kaněk je KLIDNÁ — jen nepatrné chvění okraje; výrazné boiling lines patří postavám a čmáranicím, ne velkým plochám.
- Otazníky: na papíře se ČASTO objevuje propiskou nakreslený velký OTAZNÍK — nový zhruba každých 8–12 sekund, na ploše klidně dva najednou; od 90 s, kdy už samotné uhýbání nestačí, častěji — každých 5–7 s a až tři naráz. Vydrží 8–10 s, ať se dají stihnout. Sbírá se dotykem jablka. Sebrání spustí náhodně jednu ze čtyř věcí a hráč to okamžitě pozná (krátký nápis + odlišný zvuk): GUMA (26 %) — hadovi se smaže několik posledních článků; ZVONEK (26 %) — had na tři sekundy zastaví (přestávka); BOMBOVÉ JABLKO (26 %) — uloží se do zásoby (ikonka vedle tužky, v zásobě nejvýš jedno) a hráčovo PŘÍŠTÍ nakreslené jablko je bombové, se zapálenou šňůrkou: had ho sežere, na zhruba 3,5 s omráčeně zastaví a nevyroste; NOVÁ KAŇKA (22 %) — na papír pro zbytek kola přibude další inkoustová kaňka (nejvýš 7 kaněk celkem; nad strop padne místo ní guma).
- Skóre: čas přežití v sekundách, viditelný během hry.

Stavy hry: úvodní obrazovka, hra, konec. Úvodní obrazovka: název, věta „Jsi svačina. Uteč hadovi.“, jak začít — a TAHÁK: malý přehled nakreslený jako opravdový školní tahák (co dělá tužka, co všechno může padnout z otazníku, že kaňky brzdí jen tebe, a stupnice hodnocení — s poznámkou „Pochvalu ředitele prý ještě nikdo živý nedostal.“). Na konci hodnocení jako od učitele podle času přežití: pod 30 s pětka, do 80 s čtyřka, do 120 s trojka, do 150 s dvojka, do 210 s jednička a od 210 s POCHVALA ŘEDITELE ŠKOLY. Hodnocení je červeně zakroužkované s komentářem učitele — pro každý stupeň jiným, vtipným, ve stylu hlášek českého kabinetu („Sedni si.“); i menu a závěrečné texty piš šťavnatě, ne úředně. Ukaž i nejlepší čas; ukládej ho do localStorage, ale výhradně v try/catch — bez něj hra poběží dál, jen bez rekordu. Restart okamžitě, bez načtení stránky. Pauza: klávesa P i ztráta fokusu okna hru pozastaví; obrazovka pauzy nabídne pokračování i návrat do hlavního menu.

## Vizuál: školní sešit

Celá hra vypadá jako čmáranice propiskou v POUŽÍVANÉM školním sešitě. Pozadí je čtverečkovaný papír kreslený kódem přes celé okno, s okrajem stránky — a s drobnými stopami života na okrajích: piškvorky, srdíčko, škrtaná slovíčka. Hráčovo jablko kreslené červenou propiskou, had modrou, falešná jablka tužkou šedě, otazníky propiskou, kaňky syté inkoustové. Klíčový efekt „boiling lines“: každá čmáranice existuje ve dvou až třech variantách s mírně roztřesenými čarami a několikrát za sekundu se mezi nimi přepne. Skóre a texty piš jako červené poznámky učitele na okraji stránky. Krátké syntetické zvuky přes Web Audio: škrábnutí tužky při nakreslení falešného jablka, odlišný zvuk pro každý výsledek otazníku, varovné zavrtění před výpadem, tlumené křupnutí na konci. Zvuk aktivuj až po první interakci uživatele (autoplay).

Obtížnost vylaď testováním na tohle rozvrstvení: hráč, který jen uhýbá a návnady hází bez rozmyslu, ať končí mezi 80 a 120 s (trojka); kdo návnady šetří a uhýbá výpadům, ať dosáhne 120–150 s (dvojka); přes 150 s (jednička) projde jen výborná hra s bombou a zvonky; pochvala ředitele (210 s+) ať zůstane téměř nedosažitelný mýtus.

## Pořadí práce

1. Funkční jádro: herní smyčka, koulení jablka, had honí, smrtící tělo, ochranná lhůta, konec hry, restart.
2. Mechaniky: výpady, falešná jablka (automatická i kreslená, s cooldownem), kaňky, otazníky, zrychlování, známkování.
3. Vizuál sešitu s boiling lines, dekorace okrajů, rozhraní, česká microcopy.
4. Zvuk, doladění obtížnosti, leštění.

Po každé fázi soubor otestuj a chyby hned opravuj. Hospodař s časem: celý běh dokonči do 45 minut — testuj efektivně, neleštit donekonečna.

## Akceptační kritéria — před dokončením každé jednotlivě ověř

1. Otevření souboru dvojklikem: hra jede, konzole čistá.
2. Myš, dotyk i klávesnice fungují.
3. Změna velikosti okna za běhu nerozbije vykreslení ani pozice objektů; had ani jablko nikdy neopustí viditelnou stránku.
4. Ztráta fokusu hru pozastaví, návrat umožní pokračovat.
5. Divoké rychlé klikání nerozbije cooldown ani nevyvolá chybu.
6. Opakovaný restart bez reloadu funguje.
7. Nedostupné localStorage nevyhodí chybu.
8. Hra je hratelná i na výšku na mobilním displeji.
9. Kroužení těsně za ocasem hada vede ke smrti, ne k bezpečnému přežití.
10. Had stojící cíl (hráče i falešné jablko) vždy do několika sekund dosáhne — nikdy neskončí ve věčném kroužení kolem něj.
11. Během hry je TRVALE vidět běžící čas přežití i ikonka tužky s cooldownem.
12. Jablko v klidu skončí přesně pod kurzorem — vstupní souřadnice přepočítej vůči poloze canvasu i devicePixelRatio.

## Úplně poslední krok

Až je vše hotové a všechna kritéria ověřená: pokud má pracovní složka nakonfigurovaný git remote, commitni index.html a pushni ho. Pokud remote neexistuje nebo push selže, přeskoč to bez chyby — hotový soubor je výsledek, push je jen bonus.
