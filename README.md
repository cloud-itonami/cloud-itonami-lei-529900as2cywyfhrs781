# cloud-itonami-lei-529900as2cywyfhrs781

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Six Flags Entertainment Corporation.**

This repository archives the publicly published Terms of Use / Terms and Conditions of
**Six Flags Entertainment Corporation**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: Six Flags Entertainment Corporation
- **LEI (ISO 17442)**: [529900AS2CYWYFHRS781](https://search.gleif.org/#/record/529900AS2CYWYFHRS781) (GLEIF-verified)
- **Jurisdiction**: US-DE (incorporation; headquarters in Charlotte, US-NC — see below)
- **Website**: https://www.sixflags.com
- **Ticker**: FUN (NYSE)

Note the LEI names the *post-merger* entity: the Delaware corporation behind this
record was created 2023-10-23 and became "Six Flags Entertainment Corporation" when
the Cedar Fair–Six Flags merger completed on 2024-07-01 — it is not the pre-merger
Six Flags that traded as SIX. The registry fields below (creation date, Charlotte
headquarters, first LEI registration 2024-03-21) are the evidence.

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived Terms of Use documents,
  each entry carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`,
  `:tos/sha256`, `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.
- `facts.edn` — 13 verified registry facts with per-fact provenance. **Generated** — see below.
- `scripts/verify-facts.cljk` — re-fetches every source `facts.edn` cites and fails if
  the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.

## Verifying the record

The identity table above used to be assertions with nothing in the repository
behind them. `facts.edn` now carries them as data, and every value in it was read
out of a public registry response whose URL and retrieval time sit next to the
value:

```
kbb --backend sci scripts/verify-facts.cljk           # check the recorded facts against the live sources
kbb --backend sci scripts/verify-facts.cljk --write   # re-fetch and rewrite facts.edn
```

Eleven GLEIF/ISO URLs were fetched and 13 facts recorded — the LEI record
(legal name as GLEIF spells it, **`SIX FLAGS ENTERTAINMENT CORPORATION`**, upper
case, `en`; entity **ACTIVE**; two different addresses recorded separately — the
legal address `c/o CORPORATION SERVICE COMPANY, 251 LITTLE FALLS DRIVE, 19808,
WILMINGTON, US-DE, US`, a registered-agent address in Delaware, and the
headquarters `8701 Red Oak Blvd., 28217, Charlotte, US-NC, US`; entity creation
date `2023-10-23` — this Delaware entity is months *younger* than the merger it
was built for, incorporated October 2023 as the merger holding company and
renamed at the 2024-07-01 close, so nothing in this record reaches back to
either predecessor's history; no BIC — the empty list is a measured empty, where
some corporates do carry a treasury SWIFT code; OpenCorporates id
`us_de/2531938`, S&P Global id `1866007509`), its ISIN mapping (**4** instrument
identifiers, read from `meta.pagination.total` of the cited page — the whole
list fits in one page, so unlike this family's larger issuers each ISIN is also
mirrored into `facts.edn` as its own entity: `US83001C1080`, `US83001C2070`,
`US83001AAC62`, `US83001AAD46`), its managing LOU and LEI-issuer accreditation
(**Herausgebergemeinschaft Wertpapier-Mitteilungen Keppler, Lehmann GmbH & Co.
KG** — WM Datenservice, a *German* LOU jurisdiction `DE`, accredited 2017-04-13:
a US-DE theme-park group whose LEI is issued and maintained from Frankfurt,
which the `5299 00` prefix of the LEI itself already encodes), registration
authority `RA000602` (**Division of Corporations, Department of State** —
`corp.delaware.gov`, serving Delaware only — where the entity is file number
`2531938`), ISO 20275 legal form `XTIQ` (**`Corporation`**, US-DE), and **both
consolidation levels**: no parent at either level, each level carried as a
reporting-exception entity with category
`DIRECT_ACCOUNTING_CONSOLIDATION_PARENT` /
`ULTIMATE_ACCOUNTING_CONSOLIDATION_PARENT` and reason **`NO_KNOWN_PERSON`** —
GLEIF's code for an entity with no known person controlling it, the usual shape
of a widely-held listed company (and a different exception reason than this
family's `NON_CONSOLIDATING` records, which mark an entity that tops its
accounting group). Nine of the eleven URLs answered `200`; the `direct-parent`
and `ultimate-parent` endpoints answered `404` because GLEIF publishes the
*exception* side of that pair for this entity, which the checker treats as a
fact rather than a failure.

The registration status is the loudest finding. The entity is ACTIVE, but the
LEI registration itself is **`LAPSED`**: its next-renewal date and its
last-update date are the same instant, `2025-03-21` — the record lapsed on its
renewal date and has not been renewed since, and GLEIF flags it
**`NON_CONFORMING`** (while still `FULLY_CORROBORATED`: lapsing is about the
entity not re-attesting, not about the data being wrong). Those are two
different fields, recorded separately, and this record is exactly why: a
company can operate while its LEI goes stale. Anything downstream that assumes
"has an LEI" implies "maintains an LEI" would misread this entity.

The direct-children count is a measured **0** — for a holding company whose
SEC filings name a long list of subsidiaries, including the two pre-merger
operating groups it combined. That is not the shape of the group — it is the
shape of *LEI regulation*: a subsidiary appears in GLEIF's relationship graph
only if it holds an LEI and reports the relationship, which US rules mostly do
not compel. The 0 is a measured count of what GLEIF's graph holds, not a
census of subsidiaries, and (with the registration LAPSED since 2025-03) the
relationship side of this record is as unmaintained as the rest of it.

No file in this repository was contradicted by the fetch: the identity table's
`US-DE` agrees with the LEI record, the registration authority (Delaware's
Division of Corporations) and the Delaware file number `2531938`. The
jurisdiction line above gained the headquarters clarification because the
registry carries incorporation and headquarters as separate fields — Charlotte,
North Carolina is where the post-merger company is run from, not where it is
incorporated.

The check has three exit codes, not two: `0` when every cited URL answered and
every recorded value still matches, `1` when a citation broke or a value
drifted (each difference is named, with the recorded and live values side by
side), and `3` when the check could not be performed at all — `facts.edn`
missing or empty, or GLEIF unreachable at the transport level — because a check
that could not run must not look like a check that ran and found nothing.
Before this landed, all three were shown against the live API: unmodified →
`0` (`OK all 13 recorded fact(s) still match the live sources`);
`:company/jurisdiction` edited `US-DE` → `FR` → `1`, naming `gleif-lei-record`
and `:company/jurisdiction` as `DRIFT`; the `gleif-direct-children-count`
entity deleted → `1`, naming it as `ADDED`; `facts.edn` absent → `3`
(`INCONCLUSIVE … Refusing to report a pass`). The file was restored
byte-identical afterwards (`shasum` equal).

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
