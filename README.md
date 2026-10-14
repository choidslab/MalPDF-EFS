# Temporally Labeled Malicious PDF Feature Dataset (Sample)

A sample of the feature data used in the following article:

> D.-S. Choi, T. Kim, B. Kang, and E. G. Im, "Machine learning-based detection method for malicious
> PDF files: A temporal classification approach," *Applied Soft Computing*, vol. 189, Art. no. 114461,
> Mar. 2026 (available online 23 Dec. 2025). https://doi.org/10.1016/j.asoc.2025.114461

**If you find this dataset useful in your research, please consider citing the article above.**
A BibTeX entry is provided in the [Citation](#citation) section. Thank you.

Malicious PDFs are labeled by the period in which they were created: `old_malicious` (before 2020)
or `recent_malicious` (2020-2024). Benign PDFs (`benign`) are not split by period. The features
themselves are static features of a PDF file, not time-series features.

## What this is

This repository releases **part of** the experimental data of the paper: 1,000 randomly sampled
PDF files per group, 3,000 in total. It is not the full dataset, so the numbers reported in the
paper cannot be reproduced exactly from these files. The remaining data are available from the
authors on request.

Only numeric features extracted from the PDF files are included. The PDF files themselves, file
names, and file hashes are not included.

## Files

| Folder | File | Rows | Columns |
|---|---|---|---|
| `FS31/` | `feature31_benign.csv` | 1,000 | 31 features + `class` |
| `FS31/` | `feature31_old_malicious.csv` | 1,000 | 31 features + `class` |
| `FS31/` | `feature31_recent_malicious.csv` | 1,000 | 31 features + `class` |
| `FS43/` | `feature43_benign.csv` | 1,000 | 43 features + `class` |
| `FS43/` | `feature43_old_malicious.csv` | 1,000 | 43 features + `class` |
| `FS43/` | `feature43_recent_malicious.csv` | 1,000 | 43 features + `class` |

- `FS31` is the basic feature set (Table 2 of the paper). `FS43` adds the 12 features proposed in
  the paper (Table 8). Row *i* of an `FS31` file and row *i* of the matching `FS43` file describe
  the same PDF.
- `class` is `benign`, `old_malicious` (created before 2020), or `recent_malicious` (created in
  2020-2024).

## Features

**Basic 31:** `pdfsize`, `metadata size`, `pages`, `xref Length`, `title characters`, `isEncrypted`,
`embedded files`, `images`, `text`, `header`, `obj`, `endobj`, `stream`, `endstream`, `xref`,
`trailer`, `startxref`, `Page`, `encrypt`, `ObjStm`, `JS`, `JavaScript`, `AA`, `OpenAction`,
`AcroForm`, `JBIG2Decode`, `RichMedia`, `Launch`, `EmbeddedFile`, `XFA`, `Colors`.
These follow the feature definitions of CIC-Evasive-PDFMal2022; please also cite that dataset when
you use them.

**Proposed 12:**

| Column | Name in the paper | Meaning |
|---|---|---|
| `hyperlink` | hyperlink | number of hyperlinks |
| `entropy` | file entropy | entropy of the PDF byte sequence |
| `creator` | creator | number of characters in the metadata creator field |
| `producer` | producer | number of characters in the metadata producer field |
| `author` | author | number of characters in the metadata author field |
| `layout size` | page layout size | page area (width x height) |
| `creationDate` | creationDate | 1 if a valid creation date is recorded, else 0 |
| `modDate` | modDate | 1 if a valid modification date is recorded, else 0 |
| `font` | font | number of fonts |
| `email` | email | number of email addresses |
| `image size` | embedded image size | total size of embedded images |
| `graphics` | graphics | number of vector graphic objects |

Notes: values are the raw extractor output. `pdfsize` is in bytes (the paper reports KB), and
`layout size` is not log-scaled (the paper reports the log10 value). `header` is the PDF version
string and is the only non-numeric feature.

## Sampling

Rows whose 31 basic features were identical to another row were removed first, then 1,000 rows per
group were drawn uniformly at random with a fixed seed (42).

## Citation

If you use this dataset, please cite:

```bibtex
@article{choi2026temporal,
  author  = {Choi, Doo-Seop and Kim, Taeguen and Kang, BooJoong and Im, Eul Gyu},
  title   = {Machine learning-based detection method for malicious {PDF} files: A temporal classification approach},
  journal = {Applied Soft Computing},
  volume  = {189},
  pages   = {114461},
  year    = {2026},
  month   = mar,
  note    = {Available online 23 December 2025},
  doi     = {10.1016/j.asoc.2025.114461}
}
```

## License

Creative Commons Attribution 4.0 International (CC BY 4.0).
