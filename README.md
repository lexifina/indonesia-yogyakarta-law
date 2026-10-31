# Yogyakarta (Indonesia): law history in git

The Peraturan Daerah (Perda) and Peraturan Daerah Istimewa (Perdais) of Daerah Istimewa Yogyakarta, Indonesia, as a git history: one folder per Perda, one file per Pasal (article), one paragraph per line, so `git blame`, `git log` and `git diff` work line by line. The text is the Indonesian text of each Perda as enacted, from the copy (salinan) published by JDIH Daerah Istimewa Yogyakarta (Biro Hukum Sekretariat Daerah DIY).

It follows the shared design of [lexifina/global-law](https://github.com/lexifina/global-law).

## What this repository holds

**Each Perda as enacted, not yet a history of amendments.** JDIH publishes each Perda as its signed copy; there is no consolidated text. So each Perda is one commit holding its text as enacted ("oldest version available"), credited to the publisher, not to an amending law. An amending Perda is its own folder; its amendments are not applied to the Perda it amends, and a repeal is not applied.

| File | What |
| --- | --- |
| `a-pembukaan.md` | heading, title, preamble (Menimbang, Mengingat) and enacting words |
| `pasal-NNN.md` | one Pasal; chapter, part and paragraph headings printed before the next Pasal stay at its end |
| `z1-penutup.md` | promulgation order, signatures, Lembaran Daerah number, certification of the copy |
| `z2-penjelasan.md` | the elucidation (Penjelasan), where printed |
| `z3-lampiran.md` | the annex (Lampiran), where printed |

The record is built in parts, oldest Perda first, and holds only the Perda JDIH publishes as a PDF with a text layer that passes the check below; scans and documents the reader cannot split into Pasal are left out for now. Budgets (APBD and their accountability reports), development plans (RPJMD, RPJPD) and spatial plans (RTRW, zoning), which are mostly tables and maps, are not included. It is not (yet) every Perda of Daerah Istimewa Yogyakarta.

## Source

[JDIH Daerah Istimewa Yogyakarta (Biro Hukum Sekretariat Daerah DIY)](https://jdih.jogjaprov.go.id/produk-hukum/peraturan-perundang-undangan): each Perda as a PDF with a text layer. Each PDF's sha256 is recorded with its version in `data/versions.json`.

## Dates

Each Perda is dated by the day it takes effect under its own last Pasal, at noon local time (WIB, UTC+7): the day it was promulgated (diundangkan, printed in its closing) when it says "mulai berlaku pada tanggal diundangkan", or the calendar day it names. Perda whose commencement is a period after promulgation or another event are left out for now.

## How it is built

Lexifina reads the sources listed here and records each act's dated versions, and the laws that made each change, in one corpus file. `tools/build.py` writes this repository from that file, and the same corpus always gives the same commit hashes; `REPRODUCE.md` gives the details and the checks. A model (Claude) wrote Lexifina's code; it wrote no legal text, and no model runs when the history is built.

The text layer of each PDF (no OCR) becomes the record, row by row in reading order, rows joined into paragraphs. Left out: page numbers and the "SALINAN" stamp line. Nothing is reworded.

## How it is checked

Every version is read back from git on the day it took effect and must match the corpus. A second, independent reading of every PDF (a different PDF engine, pdftotext) must hold every paragraph of the record as one unbroken stretch, letter for letter and digit for digit, and the paragraphs together must cover the whole PDF with nothing left over but page numbers and the stamp. Results are in `REPRODUCE.md`.

## What "author" means

The author of each commit is the publisher, with an e-mail address that cannot exist; the committer is always Lexifina.

## Limits

Only each Perda as enacted: no later amendments, no consolidation, no repeal applied, Indonesian text only, and only the Perda published with a text layer that pass the check. The official text is the one promulgated in the Lembaran Daerah.

## Licence

See [LICENSE](LICENSE): Undang-Undang Nomor 28 Tahun 2014 tentang Hak Cipta, Pasal 42, gives no copyright in peraturan perundang-undangan. Source: JDIH Daerah Istimewa Yogyakarta (Biro Hukum Sekretariat Daerah DIY), https://jdih.jogjaprov.go.id.
