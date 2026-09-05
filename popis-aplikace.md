# SVAČINA — popis aplikace

**SVAČINA je Snake naruby: nejste had — jste svačina.** Hráč ovládá jablko
nakreslené červenou propiskou ve školním sešitě a snaží se, aby ho nesežral
had, který roste jen tím, co sežere. Čím déle přežijete, tím lepší známku
od učitele dostanete — od pětky („Sedni si.") přes jedničku až po legendární
POCHVALU ŘEDITELE ŠKOLY, kterou prý ještě nikdo živý nedostal.

## Jak se hraje

**Tip: nejlépe se hraje myší** — touchpad zvládá jen hrubší kličky.

- **Myš / prst:** jablko se koulí za kurzorem — se setrvačností; zvládnout
  koulení je součást dovednosti. Funguje i klávesnice (šipky, WASD).
- **Kliknutí / ťuknutí:** nakreslíte tužkou falešné jablko — had se nechá
  napálit kresbou a odběhne si pro ni. Jenže sežráním vyroste a jeho tělo
  je smrtící celé, ne jen hlava. Každá návnada je riziko i záchrana.
- **Otazníky:** na papíře se objevují nakreslené otazníky — náhodně z nich
  padne guma (smaže hadovi ocas), zvonek (přestávka — had 3 s stojí),
  bombové jablko (příští nakreslené jablko hada omráčí) nebo nová kaňka.
- **Kaňky** brzdí jen vás, had přes ně klouže. Výpady had férově ohlašuje
  zavrtěním — a v pozdní hře vám začne nadbíhat.

## Co je uvnitř (jeden soubor, žádné závislosti)

Celá hra je jediný `index.html` — vanilla JavaScript + canvas 2D, zvuky
syntetizované ve Web Audio (žádné soubory, žádná CDN). Vizuál školního
sešitu je kreslený kódem včetně „boiling lines" animace čar jako z ručně
kresleného filmu. Funguje offline z dvojkliku, na počítači i na mobilu
(dotyk), má pauzu (P i ztráta fokusu), tahák s pravidly v menu, uložený
rekord (bezpečně, i bez localStorage hra běží) a čistou konzoli.
