# 04 — Ključni tokovi

Tri toka nose cijelu platformu: organizacija ulazi i otvara projekt, bilo tko
podržava, organizacija troši. Novac nikad ne prolazi kroz platformu.

## 1. Organizacija ulazi i otvara projekt

Upravitelj se prijavi Certilijom, preuzme točku s karte i prođe KYB kod Moneriuma. Za
svaki projekt `pay.domovina.ai/tools/funding` (idempotentno) kreira Safe s potpisanom
Monerium porukom, linka ga na Monerium i registrira kampanju na railu.

```mermaid
sequenceDiagram
    actor U as Upravitelj (župnik, predsjednik kluba)
    participant CE as Certilia
    participant K as Karta (gis.domovina.ai)
    participant P as Platforma
    participant MON as Monerium
    participant MPT as MPT rail
    participant G as Gnosis
    U->>CE: prijava (eOsobna / mToken)
    CE-->>P: OIDC token (OIB)
    U->>K: nalazi svoju organizaciju
    K->>P: map_ref (sloj, slug)
    U->>MON: KYB organizacije (jednom)
    MON-->>MPT: profil + IBAN → novi tenant
    U->>P: novi projekt (cilj, rok, potpisnici)
    P->>G: Safe projekta (vlasnici = potpisnici, prag 2/3)
    P->>MON: link adrese Safea (ERC-1271)
    P->>MPT: kampanja projekta
    P-->>U: projekt otvoren, QR za oglasnu ploču
```

## 2. Podrška projektu (bilo tko)

Podržavatelj ne treba ni članstvo ni kriptonovčanik. Skenira QR u Revolutu ili
mobilnom bankarstvu i plati SEPA uplatu. Certilia je potrebna samo za potvrdu na ime i
ime na listi podržavatelja (otvoreno pitanje, `docs/08`).

```mermaid
sequenceDiagram
    actor D as Podržavatelj (član ili ne)
    participant P as Platforma
    participant MPT as MPT rail
    participant B as Banka (Revolut)
    participant MON as Monerium
    participant S as Safe projekta (Gnosis)
    D->>P: "podrži" + iznos
    P->>MPT: POST /api/intents (iznos, kampanja)
    MPT-->>P: sid + kratka referenca + EPC QR
    P-->>D: QR
    D->>B: skenira QR, SEPA na IBAN tenanta
    B->>MON: SEPA uplata (opis = referenca)
    MON->>S: mint EURe izravno u Safe projekta
    MON->>MPT: webhook order processed
    MPT->>MPT: referenca → intent (ili stray resolver)
    MPT-->>P: potpisani webhook "paid" (tx potvrđen)
    P-->>D: hvala + potvrda o uplati
```

## 3. Trošenje

```mermaid
sequenceDiagram
    actor U as Upravitelj
    actor S2 as Drugi potpisnik
    participant P as Platforma
    participant S as Safe projekta
    participant MON as Monerium
    participant DOB as Dobavljač (IBAN)
    U->>P: novi trošak (iznos, dobavljač, račun)
    P->>S: predložena transakcija (redeem EURe)
    U->>S: potpis 1/2
    S2->>S: potpis 2/2
    S->>MON: burn EURe + redeem nalog
    MON->>DOB: SEPA isplata
    P-->>P: TROSAK zapisan (safe_tx_hash, račun)
```
