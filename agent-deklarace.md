# Deklarace agenta, toolingu a nastavení

- **AI agent:** Claude Code (Anthropic) — **cloud session na claude.ai/code**
- **Model:** `claude-fable-5-1` (Claude Fable 5.1); režim *Auto*, úroveň úsilí *Max*
- **Prostředí běhu:** čerstvý cloudový sandbox Claude Code, bez jakékoli
  uživatelské konfigurace (žádné CLAUDE.md, skilly, pluginy ani MCP servery
  autora). Pracovní složka = klon veřejného repozitáře
  `github.com/Matyasek/svacina-finale`, který před během obsahoval **jen
  jednořádkový README** (žádný kód, žádné assety).
- **Tooling:** standardní nástroje Claude Code v cloudu (čtení/zápis souborů,
  spouštění příkazů, git). Pro vlastní testování si agent během běhu sám
  nainstaloval headless Chromium (Playwright) — prompt na žádný nástroj
  neodkazuje.
- **Průběh:** jediná zpráva = doslovný obsah `prompt.md`, nic před ním ani za
  ním; po odeslání žádný lidský vstup, žádné odpovědi agentovi, žádné úpravy
  souborů. Agent autonomně plánoval, stavěl, testoval a opravoval.
- **Datum a délka:** 4. 9. 2026, 16:07–16:58 UTC — **51 minut** (soutěžní
  limit 60 minut dodržen).
- **Výstup:** jediný soubor `index.html` (56 283 B). Agent ho na konci sám
  commitnul a pushnul do repozitáře (větev `claude/svacina-minigame-vronfj`,
  commit „Přidej minihru SVAČINA – Snake naruby v jednom index.html“);
  odevzdaný soubor je s tímto commitem bajtově shodný, ručně nedotčený.
- **Živě k vyzkoušení:** https://matyasek.github.io/svacina-finale/
  (GitHub Pages z téhož repozitáře — tentýž nezměněný soubor).
