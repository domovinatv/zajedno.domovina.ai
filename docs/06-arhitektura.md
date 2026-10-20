# 06 — Arhitektura sustava

Nova je samo tanka aplikacija: profili, organizacije, projekti, izvješća. Novac,
potvrde i on-chain dio već postoje u MPT railu, a karta je već imenik zajednica.

```mermaid
flowchart LR
    subgraph Ljudi
        D[Podržavatelj<br/>bilo tko]
        UP[Upravitelj i potpisnici<br/>organizacije]
    end
    subgraph Karta["Karta Hrvatske (postoji)"]
        KW[karta-web<br/>gis.domovina.ai]
    end
    subgraph App["zajedno.domovina.ai (novo)"]
        API[API<br/>organizacije, projekti, podrške, troškovi]
        DB[(Baza<br/>bez ledgera)]
        IDX[Indekser salda<br/>čita Safeove]
        FEED[Javni feed<br/>projects.geojson]
        API --> DB
        IDX --> DB
        DB --> FEED
    end
    subgraph Rail["pay.domovina.ai (postoji)"]
        MPT[MPT rail<br/>intenti, webhook, potvrde]
        FUND[tools/funding<br/>Safe po projektu]
        WAL[wallet.domovina.ai<br/>passkey Safe za potpisnike]
    end
    subgraph Vani["Vanjski"]
        CE[Certilia<br/>prijava, OIB]
        MON[Monerium<br/>KYC/KYB, IBAN, EURe]
        BANK[Banka podržavatelja<br/>Revolut, m-banking]
        G[(Gnosis Chain<br/>Safe po projektu)]
    end
    D --> KW
    D --> API
    UP --> API
    API --> CE
    KW -- "map_ref" --> API
    FEED -- "sloj: aktivni projekti" --> KW
    API -- "intent" --> MPT
    MPT -- "webhook paid" --> API
    API --> FUND
    FUND --> G
    D -- "SEPA QR" --> BANK
    BANK --> MON
    MON -- "mint EURe" --> G
    MON -- "order webhook" --> MPT
    UP --> WAL
    WAL -- "potpis troška" --> G
    IDX --> G
```

| Komponenta | Status | Odgovornost |
| --- | --- | --- |
| karta-web | postoji | imenik zajednica, ulaz preko točke na karti, sloj aktivnih projekata |
| MPT rail | postoji | payment intenti, Monerium webhook, potvrde o uplati, stray resolver |
| `tools/funding` | postoji (sandbox) | Safe po projektu, Monerium link, kampanja; treba API umjesto skripte |
| wallet.domovina.ai | postoji | passkey Safe kao potpisnički ključ upravitelja |
| API + baza | novo | organizacije, članstva, projekti, podrške, troškovi s računima |
| Certilia login | novo | OIDC prijava, OIB u profilu osobe |
| Indekser salda | novo | saldo i izlazi Safea s lanca, keš u bazi |

Veza s kartom je labava u oba smjera: karta šalje na stranicu organizacije preko
`map_ref`, a platforma vraća javni GeoJSON s aktivnim projektima po točki. Novi sloj
na karti mora ući u `SIBLING_LAYERS` u `karta-web/scripts/sync-data.mjs`.
