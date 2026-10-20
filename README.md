# zajedno.domovina.ai

Platforma na kojoj lokalne zajednice (župe, klubovi, škole, udruge, JLS) objavljuju
svoje projekte, a **bilo tko** ih podržava običnom SEPA uplatom. Novac ide izravno u
Safe multisig projekta na Gnosisu preko postojećeg MPT raila
([pay.domovina.ai](https://github.com/domovinatv/pay.domovina.ai)). Platforma ne drži
novac, ne drži ključeve i ne uzima naknadu.

**Pilot:** župe i nogometni klubovi skupljaju za sunčanu elektranu na vlastitoj
nekretnini (župni dom, svlačionica). Manji račun za struju znači manje režija, a njih
ionako plaćaju ti isti članovi.

## Stanje

Faza: **baza znanja**. Koda još nema; `docs/` je jedini izvor istine iz kojeg se gradi
aplikacija. Početak čitanja: [`docs/00-indeks.md`](docs/00-indeks.md).

## Srodni repoi

| Repo | Uloga za zajedno |
|---|---|
| [karta-hrvatske](https://github.com/domovinatv/karta-hrvatske) | imenik ~18.000 zajednica s lokacijom (gis.domovina.ai), ulaz preko točke na karti |
| [pay.domovina.ai](https://github.com/domovinatv/pay.domovina.ai) | MPT rail: payment intenti, Monerium, Safe po projektu, potvrde o uplati, wallet |
| [energy.domovina.ai](https://github.com/domovinatv/energy.domovina.ai) | stručna baza za sunčane elektrane: pravni okvir, izvođač, prave lokacije |
| crkve / klubovi / udruge / oou .domovina.ai | katalozi organizacija iz kojih karta gradi slojeve |
