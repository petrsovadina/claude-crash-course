# Hlavní plán aplikace pro generování obsahu poháněné umělou inteligencí

## Přehled a cíle aplikace

Cílem této aplikace Next.js je automatizovat pracovní postup tvorby obsahu využitím umělé inteligence ke zpracování videoklipů, generování shrnutí a vytváření příspěvků na sociálních sítích. Hlavními cíli jsou:

1. Zjednodušit proces převodu videoobsahu na psané příspěvky pro různé platformy.
2. Využít AI k přepisu a shrnutí videoklipů.
3. Poskytnout uživatelsky přívětivé rozhraní pro správu procesu vytváření obsahu

## Cílová skupina

- Tvůrci obsahu
- Správci sociálních médií
- Jednotlivci, kteří chtějí znovu použít video obsah pro více platforem

## Základní vlastnosti a funkce

1. Nahrávání videa

   - Nahrávání více videoklipů
   - Ukládání nahraných videí pomocí služby UploadThing

2. Zpracování umělé inteligence

   - Přepisujte videa pomocí rozhraní API Whisper od OpenAI
   - Shrňte přepisy do souhrnu o 2 000 slovech pomocí GPT-4

3. Konfigurace výzvy

   - Vytváření a úprava výzev pro různé platformy sociálních médií

4. Generování obsahu

   - Generování příspěvků pro konkrétní platformu na základě shrnutí videa a nakonfigurovaných výzev.

5. Správa výsledků

   - Zobrazení a kopírování vygenerovaného obsahu pro každou platformu

6. Systém fronty úloh
   - Správa a sledování stavu zpracování úloh

## Technický zásobník na vysoké úrovni

1. Frontend:

   - UI: 1. frontend: Next.js s komponentami uživatelského rozhraní ShadCN
   - Úředník pro ověřování

2. Backend:

   - Pro hlavní logiku aplikace jsou použity trasy API Next.js
   - Backend Flask pro úlohy zpracování umělé inteligence

3. Databáze:

   - Databáze: PostgreSQL s Drizzle ORM

4. Ukládání souborů:

   - UploadThing pro ukládání videa

5. Služby umělé inteligence:
   - (Whisper pro přepis, GPT-4 pro sumarizaci a generování obsahu).

## Konceptuální datový model

1. Uživatel

   - ID
   - Název
   - E-mail

2. Projekt

   - ID
   - Název
   - Datum vytvoření
   - Stav

3. VideoClip

   - ID
   - ProjectID
   - FileName
   - UploadThingURL

4. Přepis

   - ID
   - VideoClipID
   - Obsah

5. Shrnutí

   - ID
   - ProjectID
   - Obsah

6. Výzva

   - ID
   - ProjectID
   - Platforma
   - Obsah

7. GeneratedPost

   - ID
   - ProjectID
   - Platforma
   - Obsah

8. Práce
   - ID
   - ID projektu
   - Typ (přepis, sumarizace, postgenerace)
   - Stav (Připraveno, Probíhá, Dokončeno, Nepovedlo se)
   - CreationDate

## Zásady návrhu uživatelského rozhraní

1. Čistý a intuitivní design s použitím komponent ShadCN
2. Jasné oddělení jednotlivých fází (Nahrát, Konfigurace, Spustit, Výsledek)
3. Snadno použitelné rozhraní drag-and-drop pro nahrávání videa
4. Jednoduché textové oblasti pro pohotovou konfiguraci
5. Přehledné zobrazení stavu a průběhu úlohy
6. Snadno kopírovatelný generovaný obsah ve fázi výsledků

## Bezpečnostní aspekty

1. Ověřování a autorizace uživatelů pomocí Clerk
2. Bezpečné zpracování klíčů API pro OpenAI a UploadThing
3. Správná sanitizace a validace dat pro uživatelské vstupy
4. Bezpečné ukládání citlivých informací (např. přepisů, souhrnů).

## Fáze vývoje

1. Fáze 1: Nastavení projektu a základní infrastruktura

   - Nastavení projektu Next.js pomocí adresáře aplikace s ShadCN
   - Implementujte ověřování úředníků
   - Nastavení databáze PostgreSQL a ORM Drizzle
   - Implementace základní správy projektu (vytvoření, seznam, zobrazení)

2. Fáze 2: Nahrávání a ukládání videí

   - Integrace služby UploadThing pro ukládání videí
   - Implementace funkce nahrávání videí
   - Vytvoření rozhraní pro správu videoklipů

3. Fáze 3: Integrace zpracování umělé inteligence

   - Nastavení backendu Flask pro úlohy AI
   - Integrace rozhraní API OpenAI (Whisper a GPT-4)
   - Implementujte logiku přepisu a shrnutí

4. Fáze 4: Konfigurace výzvy a generování obsahu

   - Vytvoření konfiguračního rozhraní výzvy
   - Implementujte logiku generování obsahu pomocí GPT-4
   - Vyvinout systém fronty úloh pro zpracování běhů

5. Fáze 5: Správa výsledků a zdokonalení uživatelského rozhraní

   - Vytvoření rozhraní pro zobrazení výsledků
   - Implementace funkce kopírování na tabuli
   - Zdokonalení celkového uživatelského rozhraní a prostředí

6. Fáze 6: Testování, optimalizace a nasazení
   - Proveďte důkladné testování všech funkcí
   - Optimalizujte výkon a využití zdrojů
   - Připravte se na nasazení a spuštění

## Potenciální výzvy a řešení

1. Výzva: Zpracování velkých video souborů
   Řešení: Zavedení chunked uploadu a zpracování

2. Úkol: Vytvoření datových souborů: Řešení: Správa dlouhotrvajících úloh umělé inteligence
   Řešení: Implementace robustního systému fronty úloh s aktualizacemi stavu

3. Výzva: Zajištění přesnosti obsahu generovaného umělou inteligencí
   Řešení: Implementace funkcí pro kontrolu a úpravy generovaného obsahu

4. Výzva: Škálovatelnost systému
   Řešení: Zvažte architekturu bez serveru pro zpracování umělé inteligence.

## Možnosti budoucího rozšíření

1. Přímá integrace s platformami sociálních médií pro zveřejňování příspěvků
2. Podpora dalších typů obsahu (např. zvuk, obrázky)
3. Pokročilá analytika a sledování výkonu pro generovaný obsah
4. Kolaborativní funkce pro týmovou tvorbu obsahu
5. Vlastní vyladění modelu umělé inteligence pro lepší sumarizaci
