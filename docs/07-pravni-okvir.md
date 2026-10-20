# 07 — Pravni okvir

Platforma ne drži novac i ne naplaćuje ništa, pa nije ni platna institucija ni ECSP
pružatelj. Regulirani dio radi Monerium kao licencirana institucija za elektronički
novac: KYB organizacije, IBAN, mint i redeem EURe. Podržavatelj plaća iz svoje banke.

| Tko | Uloga | Regulacija |
| --- | --- | --- |
| Monerium | izdaje EURe, drži IBAN, KYC/KYB | licencirana EMI |
| Organizacija | prima uplate na vlastiti Monerium profil, troši iz Safea | vlastiti KYB; prima u svoje ime, ne preko platforme (Monerium ToS §16, vidi `pay.domovina.ai/docs/2026-10-11-funding-po-projektu.md`) |
| Platforma | softver: profili, projekti, izvješća | ne drži novac ni ključeve, nema naknade |
| Podržavatelj | SEPA uplata iz svoje banke | KYC već kod banke |

**Granica koju treba čuvati:** podržavatelj ne dobiva financijski povrat (kamatu,
udjel, dio prihoda elektrane). Dok je tako, ECSP se ne primjenjuje, bez obzira na
tehnologiju plaćanja. Zato copy kaže „doprinos”, ne „ulaganje”.

Za elektrane vrijedi detaljna razrada u `energy.domovina.ai/docs/03` (model A,
doprinos kolektivnom korisniku) i `docs/14` (zašto nije ECSP).
