# Quran-Data [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

A complete static dataset of the Quran: verses, Indonesian translation, Kemenag tafsir, per-verse audio, mushaf page images (multiple variants), and hadith. Suited for PWAs, APIs, bots, or read/memorization apps.

## Data Source

Data is sourced from the following official or open sources:

| Source                                                | Content                                              |
| ----------------------------------------------------- | ---------------------------------------------------- |
| [Quran Kemenag](https://quran.kemenag.go.id/)         | Verses, Indonesian translation, tafsir, footnotes    |
| [Quran KSU](https://quran.ksu.edu.sa/)                | Mushaf page images (Hafs, Hafs Tajweed, Warsh)       |
| [Hadith API](https://github.com/gadingnst/hadith-api) | Hadith collections (Bukhari, Muslim, Abu Daud, etc.) |

Murattal audio (per verse) from Kemenag media; reference format: `001001` = surah 1 verse 1.

## Folder structure (`public/`)

| Path                  | Description                                                      |
| --------------------- | ---------------------------------------------------------------- |
| `quran/`              | 114 JSON files (one per surah, verses + translation + audio URL) |
| `tafsir/`             | 114 JSON files (one per surah, tafsir per verse)                 |
| `audio/`              | 6236 `.m4a` files (`{surah}-{ayah}.m4a`)                         |
| `mushaf/kemenag/`     | Mushaf page images (`.webp`), 604 pages                          |
| `mushaf/ksu-hafs/`    | KSU Hafs mushaf (`.png`), 604 pages                              |
| `mushaf/ksu-tajweed/` | KSU Hafs Tajweed (`.png`), 604 pages                             |
| `mushaf/ksu-warsh/`   | KSU Warsh (`.png`), 604 pages                                    |
| `hadith/`             | 9 hadith collection JSON files (bukhari, muslim, etc.)           |
| `fonts/`              | Optional Arabic/UI fonts (in Drive backup)                       |
| `*.pdf` (root)        | Optional docs (e.g. Juz Amma methods, mushaf reading guide)      |

`audio/` and `mushaf/` may be omitted from version control due to size (~1 GB total). To generate them locally, use the scripts in the repo (e.g. `scraper.ts`, `ksu.ts`).

**Backup (full dataset):** [Quran-Data on Google Drive](https://drive.google.com/drive/folders/1-kI84TefHznw7IFabzNbZTkIcfIUsg1q?usp=sharing) — folders `audio`, `fonts`, `hadith`, `mushaf`, `quran`, `tafsir`, plus PDFs (Juz Amma, pedoman mushaf). Download to restore or use offline.

## File Format

### `public/quran/{1-114}.json`

One file per surah. Structure:

```json
{
  "data": [
    {
      "id": 1,
      "surah_id": 1,
      "ayah": 1,
      "page": 1,
      "quarter_hizb": 1,
      "juz": 1,
      "manzil": 1,
      "arabic": "بِسْمِ اللّٰهِ الرَّحْمٰنِ الرَّحِيْمِ",
      "kitabah": "...",
      "latin": "Bismillāhir-raḥmānir-raḥīm(i).",
      "arabic_words": ["بِسْمِ", "اللّٰهِ", ...],
      "translation": "In the name of Allah, the Most Gracious, the Most Merciful.",
      "footnotes": null,
      "surah": { "id": 1, "arabic": " الفاتحة", "latin": "Al-Fātiḥah", "translation": "The Opener", "num_ayah": 7, "location": "Makkiyah" },
      "audio": "https://..."
    }
  ]
}
```

Each item in `data` is one verse (including surah metadata and audio URL).

### `public/tafsir/{1-114}.json`

One file per surah. Each file has a single `data` object with tafsir fields per verse: `tafsir.wajiz` (brief), `tafsir.tahlili` (detailed), `intro_surah`, `kosakata`, etc. (structure follows Kemenag API.)

### `public/audio/{surah}-{ayah}.m4a`

Murattal audio per verse. Example: `1-1.m4a` = Al-Fatihah verse 1. Total 6236 files (one per verse).

### `public/mushaf/`

Mushaf page images (one file = one page, 604 pages standard):

| Folder         | Format  | Description            |
| -------------- | ------- | ---------------------- |
| `kemenag/`     | `.webp` | Kemenag mushaf (khat)  |
| `ksu-hafs/`    | `.png`  | Hafs (KSU)             |
| `ksu-tajweed/` | `.png`  | Hafs Tajweed (KSU)     |
| `ksu-warsh/`   | `.png`  | Warsh recitation (KSU) |

Filenames: 3-digit page number (e.g. `001.png`, `604.png`).

### `public/hadith/*.json`

One file per collection (bukhari, muslim, abu-daud, ahmad, tirmidzi, nasai, ibnu-majah, malik, darimi). Structure follows [hadith-api](https://github.com/gadingnst/hadith-api).

### Root-level PDFs in `public/`

Optional reference documents (not required for the dataset):

- **Juz-Amma-Metode-Kitabah.pdf** — Juz Amma (reading) method (kitabah).
- **Juz-Amma-Metode-Tilawah.pdf** — Juz Amma tilawah method.
- **Pedoman-Membaca-Mushaf-Al-Quran-Isyarat.pdf** — Guide for reading the mushaf (signs/symbols).

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
