# 08 — Plan i otvorena pitanja

Rail, Safe po projektu i karta već rade, pa MVP nije novi sustav nego povezivanje
postojećeg. Projekti Karta Hrvatske i Stranke već imaju Safe i kampanju na sandboxu
(`pay.domovina.ai/docs/2026-10-11-funding-po-projektu.md`).

```mermaid
flowchart LR
    F0["Faza 0<br/>ITalk projekti<br/>Safe po projektu, javni saldo (postoji)"]
    F1["Faza 1<br/>Prva župa i prvi klub, elektrana<br/>vlastiti Monerium KYB + tenant"]
    F2["Faza 2<br/>Self-serve onboarding<br/>Certilia + tools/funding kao API"]
    F3["Faza 3<br/>Sloj na karti<br/>aktivni projekti po točki, cijela RH"]
    F0 -- "rail u produkciji" --> F1
    F1 -- "KYB postupak opisan" --> F2
    F2 -- "desetak organizacija" --> F3
```

## Otvorena pitanja

- [ ] Koliko traje i što traži Monerium KYB za župu i za klub (udrugu)? To je najveće trenje onboardinga.
- [ ] Tko su potpisnici Safea: župnik + ekonom + član ekonomskog vijeća; predsjednik + blagajnik + član uprave kluba?
- [ ] Treba li župi suglasnost biskupije za elektranu na crkvenoj nekretnini, i može li to biti korak u onboardingu?
- [ ] Standardni tekst izjave o namjeni viška sredstava, jedan za sve projekte.
- [ ] Je li Certilia obavezna za podršku ili samo za potvrdu na ime i javnu listu podržavatelja?
- [ ] Prazan repo `domovinatv/funding.domovina.ai` (lokalno samo `.git`): obrisati ili preimenovati.
