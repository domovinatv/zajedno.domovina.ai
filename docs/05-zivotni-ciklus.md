# 05 — Životni ciklus

Novac stiže u Safe odmah, pa nema „sve ili ništa” preko autorizacija. Rok i cilj su
javno obećanje organizacije; što se događa s novcem ako cilj nije dosegnut,
organizacija navodi unaprijed (izjava o namjeni viška, `docs/02`). Stanja podrške
preslikavaju stanja MPT intenta (`pay.domovina.ai/docs/state-machines.md`).

## Projekt

```mermaid
stateDiagram-v2
    [*] --> Nacrt: upravitelj kreira
    Nacrt --> Priprema: predaj
    Priprema --> Otvoren: Safe deployan, Monerium link, kampanja na railu
    Otvoren --> CiljDosegnut: saldo Safea >= cilj
    CiljDosegnut --> Otvoren: nastavlja primati (opcionalno)
    Otvoren --> RokIstekao: rok, cilj nije dosegnut
    RokIstekao --> UProvedbi: unaprijed navedeno - provodi djelomično
    RokIstekao --> Povrat: unaprijed navedeno - vraća uplatiteljima
    CiljDosegnut --> UProvedbi: prvi trošak
    UProvedbi --> Zavrsen: završno izvješće, saldo Safea 0
    Povrat --> Zavrsen: svi povrati isplaćeni
    Zavrsen --> [*]
```

## Podrška

```mermaid
stateDiagram-v2
    [*] --> Kreirana: intent (sid + referenca)
    Kreirana --> Istekla: nema uplate u roku intenta
    Kreirana --> Primljena: Monerium order processed
    Primljena --> Placena: mint u Safe potvrđen na lancu
    Kreirana --> RucnoUparena: uplata bez reference, stray resolver
    RucnoUparena --> Placena
    Placena --> Vracena: projekt u stanju Povrat
    Istekla --> [*]
    Placena --> [*]
    Vracena --> [*]
```

Povrat je skup: svaki je zasebna Safe transakcija s redeemom na IBAN uplatitelja.
Razumna zadana postavka je „novac ostaje projektu za istu namjenu”, a povrat samo kad
ga organizacija izričito obeća.
