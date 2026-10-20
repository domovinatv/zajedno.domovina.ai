# zajedno.domovina.ai — CLAUDE.md

Platforma za projekte lokalnih zajednica: organizacija objavi projekt, bilo tko ga
podrži SEPA uplatom, novac ide izravno u Safe projekta (Monerium EURe, Gnosis).

**Stanje: baza znanja, bez koda.** `docs/` je jedini izvor istine. Kod se piše iz
dokumenata, ne obrnuto; kad se odluka promijeni, prvo se mijenja dokument.

## Potvrđene odluke (20. 10. 2026.)

1. **Nije ECSP / HANFA.** Podržavatelj daje doprinos, ne dobiva financijski povrat.
   Novac ide SEPA → Monerium IBAN → EURe u Safe multisig projekta (`docs/07`).
2. **Podržati smije bilo tko**, ne samo članovi. Cilj je privući opću javnost na
   dobre projekte. Članstvo je oznaka i pravo upravljanja, nije uvjet (`docs/03`).
3. **Identitet = Certilia login** (OIDC, OIB). Verifikacija članstva je sporedna.
4. **Plaćanja i KYC/KYB = Monerium**, kroz MPT rail iz pay.domovina.ai. Platforma
   ne drži novac ni ključeve.
5. **Bez naknada.** Platforma je besplatna infrastruktura. Ako domovina.energy gradi
   elektranu kao izvođač, to piše uz projekt s javnom cijenom izvedbe.
6. **Pilot: župe i nogometni klubovi**, projekt = sunčana elektrana na nekretnini
   organizacije (`docs/02`).
7. **Zaseban repo** s vlastitom bazom znanja; ime `zajedno.domovina.ai`
   (`projekti.domovina.ai` je zauzet).

## Pravila

- Tvrdnja o drugom repou (rail, energy, karta) ulazi u dokument tek kad je provjerena
  u tom repou; uz nju ide put do izvora (`pay.domovina.ai/docs/...`).
- Dijagrami su mermaid u markdownu.
- Riječ „ulaganje” ne koristi se u copyju: podržavatelj **doprinosi**, ne ulaže
  (vidi `docs/07`).
