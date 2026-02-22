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

The full dataset (quran, tafsir, hadith, audio, mushaf, fonts, and optional PDFs) is included in this repo. For backup or offline use, a copy is also available on [Quran-Data on Google Drive](https://drive.google.com/drive/folders/1-kI84TefHznw7IFabzNbZTkIcfIUsg1q?usp=sharing).

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

## 99 Asmaul Husna

| No  | Name (Latin)          | Name (Arabic)                 | Meaning (EN)                | Meaning (ID)                                    |
| --- | --------------------- | ----------------------------- | --------------------------- | ----------------------------------------------- |
| 1   | Ar-Rahmânu            | الرَّحْمـٰنُ                  | The Beneficent              | Yang Maha Pengasih                              |
| 2   | Ar-Raḫîmu             | الرَّحِيْمُ                   | The Merciful                | Yang Maha Penyayang                             |
| 3   | Al-Maliku             | الْمَلِكُ                     | The King                    | Yang Maha Merajai/Memerintah                    |
| 4   | Al-Quddûsu            | الْقُدُّوْسُ                  | The All-Holy                | Yang Mahasuci                                   |
| 5   | As-Salâmu             | السَّلاَمُ                    | The Peace                   | Yang Maha Memberi Kesejahteraan                 |
| 6   | Al-Mu'minu            | الْمُؤْمِنُ                   | The Granter of Security     | Yang Maha Memberi Keamanan                      |
| 7   | Al-Muhaiminu          | الْمُهَيْمِنُ                 | The Controller              | Yang Maha Pemelihara                            |
| 8   | Al-`Azizu             | الْعَزِيْزُ                   | The Exalted in Might        | Yang Memiliki Mutlak Kegagahan                  |
| 9   | Al-Jabbâru            | الْجَبَّارُ                   | The Omnipotent              | Yang Maha Perkasa                               |
| 10  | Al-Mutakabbiru        | الْمُتَكَبِّرُ                | The Majestic                | Yang Maha Megah                                 |
| 11  | Al-Khâliqu            | الْخَالِقُ                    | The Creator                 | Yang Maha Pencipta                              |
| 12  | Al-Bâri'u             | الْبَارِئُ                    | The Initiator               | Yang Maha Melepaskan                            |
| 13  | Al-Mushawwiru         | الْمُصَوِّرُ                  | The Fashioner               | Yang Maha Membentuk Rupa (makhluknya)           |
| 14  | Al-Ghaffaru           | الْغَفَّارُ                   | The Repeatedly Forgiving    | Yang Maha Pengampun                             |
| 15  | Al-Qahhâru            | الْقَهَّارُ                   | The Subduer                 | Yang Maha Memaksa                               |
| 16  | Al-Wahhâbu            | الْوَهَّابُ                   | The Absolute Bestower       | Yang Maha Pemberi Karunia                       |
| 17  | Ar-Razzâqu            | الرَّزَّاقُ                   | The Provider                | Yang Maha Pemberi Rezeki                        |
| 18  | Al-Fattâhu            | الْفَتَّاحُ                   | The Opener                  | Yang Maha Pembuka Rahmat                        |
| 19  | Al-`Alîmu             | الْعَلِيْمُ                   | The All-Knowing             | Yang Maha Mengetahui (Memiliki Ilmu)            |
| 20  | Al-Qâbiḍu             | الْقَابِضُ                    | The Restrainer              | Yang Maha Menyempitkan (makhluknya)             |
| 21  | Al-Bâsithu            | الْبَاسِطُ                    | The Extender                | Yang Maha Melapangkan (makhluknya)              |
| 22  | Al-Khâfiḍu            | الْخَافِضُ                    | The Abaser                  | Yang Maha Merendahkan (makhluknya)              |
| 23  | Ar-Râfi`u             | الرَّافِعُ                    | The Exalter                 | Yang Maha Meninggikan (makhluknya)              |
| 24  | Al-Mu`izzu            | الْمُعِزُّ                    | The Giver of Honor          | Yang Maha Memuliakan (makhluknya)               |
| 25  | Al-Mudzillu           | الْمُذِلُّ                    | The Giver of Dishonor       | Yang Maha Menghinakan (makhluknya)              |
| 26  | As-Samî`u             | السَّمِيْعُ                   | The All-Hearing             | Yang Maha Mendengar                             |
| 27  | Al-Bashîru            | الْبَصِيْرُ                   | The All-Seeing              | Yang Maha Melihat                               |
| 28  | Al-Ḥakamu             | الْحَكَمُ                     | The Judge                   | Yang Maha Menetapkan                            |
| 29  | Al-`Adlu              | الْعَدْلُ                     | The Just                    | Yang Mahaadil                                   |
| 30  | Al-Lathîfu            | اللَّطِيْفُ                   | The Gentle                  | Yang Mahalembut                                 |
| 31  | Al-Khabîru            | الْخَبِيْرُ                   | The All-Aware               | Yang Maha Mengetahui Rahasia                    |
| 32  | Al-Ḥalîmu             | الْحَلِيْمُ                   | The Forbearing              | Yang Maha Penyantun                             |
| 33  | Al-`Adhîmu            | الْعَظِيْمُ                   | The Most Great              | Yang Mahaagung                                  |
| 34  | Al-Ghafûru            | الْغَفُوْرُ                   | The Ever-Forgiving          | Yang Maha Pengampun                             |
| 35  | Asy-Syakûru           | الشَّكُوْرُ                   | The Grateful                | Yang Maha Pembalas Budi (Menghargai)            |
| 36  | Al-`Aliyyu            | الْعَلِيُّ                    | The Most High               | Yang Maha Tinggi                                |
| 37  | Al-Kabîru             | الْكَبِيْرُ                   | The Great                   | Yang Maha Besar                                 |
| 38  | Al-Ḥafîdhu            | الْحَفِيْظُ                   | The Preserver               | Yang Maha Menjaga                               |
| 39  | Al-Muqîtu             | الْمُقِيْتُ                   | The Nourisher               | Yang Maha Pemberi Kecukupan                     |
| 40  | Al-Ḥasîbu             | الْحَسِيْبُ                   | The Ever-Reckoner           | Yang Maha Membuat Perhitungan                   |
| 41  | Al-Jalîlu             | الْجَلِيْلُ                   | The Majestic                | Yang Mahamulia                                  |
| 42  | Al-Karîmu             | الْكَرِيْمُ                   | The Noble                   | Yang Maha Pemurah                               |
| 43  | Ar-Raqîbu             | الرَّقِيْبُ                   | The Watchful                | Yang Maha Mengawasi                             |
| 44  | Al-Mujîbu             | الْمُجِيْبُ                   | The Responsive              | Yang Maha Mengabulkan                           |
| 45  | Al-Wâsi`u             | الْوَاسِعُ                    | The Vast                    | Yang Maha Luas                                  |
| 46  | Al-Ḥakîmu             | الْحَكِيْمُ                   | The Wise                    | Yang Maha Bijaksana                             |
| 47  | Al-Wadûdu             | الْوَدُوْدُ                   | The Affectionate            | Yang Maha Pencinta                              |
| 48  | Al-Majîdu             | الْمَجِيْدُ                   | The All-Glorious            | Yang Maha Mulia                                 |
| 49  | Al-Bâ`itsu            | الْبَاعِثُ                    | The Resurrector             | Yang Maha Membangkitkan                         |
| 50  | Asy-Syahîdu           | الشَّهِيْدُ                   | The Witness                 | Yang Maha Menyaksikan                           |
| 51  | Al-Ḥaqqu              | الْحَقُّ                      | The Truth                   | Yang Mahabenar                                  |
| 52  | Al-Wakîlu             | الْوَكِيْلُ                   | The Trustee                 | Yang Maha Memelihara                            |
| 53  | Al-Qawiyyu            | الْقَوِيُّ                    | The Strong                  | Yang Mahakuat                                   |
| 54  | Al-Matînu             | الْمَتِيْنُ                   | The Firm                    | Yang Mahakokoh                                  |
| 55  | Al-Waliyyu            | الْوَلِيُّ                    | The Helper                  | Yang Maha Melindungi                            |
| 56  | Al-Ḥamîdu             | الْحَمِيْدُ                   | The All-Praiseworthy        | Yang Maha Terpuji                               |
| 57  | Al-Muḫshî             | الْمُحْصِيُ                   | The Accounter               | Yang Maha Mengalkulasi                          |
| 58  | Al-Mubdi'u            | الْمُبْدِئُ                   | The Originator              | Yang Maha Memulai                               |
| 59  | Al-Mu`idu             | الْمُعِيْدُ                   | The Restorer                | Yang Maha Mengembalikan Kehidupan               |
| 60  | Al-Muḫyi              | الْمُحْيِي                    | The Giver of Life           | Yang Maha Menghidupkan                          |
| 61  | Al-Mumîtu             | الْمُمِيْتُ                   | The Bringer of Death        | Yang Maha Mematikan                             |
| 62  | Al-Ḥayyu              | الْحَيُّ                      | The Living                  | Yang Mahahidup                                  |
| 63  | Al-Qayyûmu            | الْقَيُّوْمُ                  | The Subsisting              | Yang Mahamandiri                                |
| 64  | Al-Wâjidu             | الْوَاجِدُ                    | The Finder                  | Yang Maha Penemu                                |
| 65  | Al-Mâjidu             | الْمَاجِدُ                    | The Illustrious             | Yang Mahamulia                                  |
| 66  | Al-Wâḫidu             | الْوَاحِدُ                    | The Unique                  | Yang Maha Tunggal                               |
| 67  | Al-Aḫadu              | الْأَحَدُ                     | The One                     | Yang Maha Esa                                   |
| 68  | Ash-Shamadu           | الصَّمَدُ                     | The Eternal                 | Yang Maha Dibutuhkan, Tempat Meminta            |
| 69  | Al-Qâdiru             | الْقَادِرُ                    | The All-Powerful            | Yang Maha Menentukan, Maha Menyeimbangkan       |
| 70  | Al-Muqtadiru          | الْمُقْتَدِرُ                 | The Determiner              | Yang Maha Berkuasa                              |
| 71  | Al-Muqaddimu          | الْمُقَدِّمُ                  | The Expediter               | Yang Maha Mendahulukan                          |
| 72  | Al-Muakhiru           | الْمُؤَخِّرُ                  | The Delayer                 | Yang Maha Mengakhirkan                          |
| 73  | Al-Awwalu             | الْأَوَّلُ                    | The First                   | Yang Mahaawal                                   |
| 74  | Al-Âkhiru             | الْآخِرُ                      | The Last                    | Yang Mahaakhir                                  |
| 75  | Adh-Dhâhiru           | الظَّاهِرُ                    | The Manifest                | Yang Mahanyata                                  |
| 76  | Al-Bâthinu            | الْبَاطِنُ                    | The Hidden                  | Yang Maha Ghaib                                 |
| 77  | Al-Wâlî               | الْوَالِي                     | The Patron                  | Yang Maha Memerintah                            |
| 78  | Al-Muta`âli           | الْمُتَعَالِي                 | The Supremely Exalted       | Yang Maha Tinggi                                |
| 79  | Al-Barru              | الْبَرُّ                      | The Good                    | Yang Maha Penderma                              |
| 80  | At-Tawwabu            | التَّوَّابُ                   | The Ever-Returning          | Yang Maha Penerima Tobat                        |
| 81  | Al-Muntaqimu          | الْمُنْتَقِمُ                 | The Avenger                 | Yang Maha Penuntut Balas                        |
| 82  | Al-`Afuwwu            | الْعَفُوُّ                    | The Pardoner                | Yang Maha Pemaaf                                |
| 83  | Ar-Ra'ûfu             | الرَّؤُوْفُ                   | The Kind                    | Yang Maha Pengasih                              |
| 84  | Mâlikul-mulki         | مَالِكُ الْمُلْكِ             | Owner of all Sovereignty    | Yang Maha Penguasa Kerajaan (Semesta)           |
| 85  | Dzul-Jalâli wal-Ikram | ذُو الْجَلَالِ وَالْإِكْرَامِ | Owner of Majesty and Honour | Yang Maha Pemilik Kebesaran dan Kemuliaan       |
| 86  | Al-Muqsithu           | الْمُقْسِطُ                   | The Equitable               | Yang Mahaadil                                   |
| 87  | Al-Jâmi`u             | الْجَامِعُ                    | The Gatherer                | Yang Maha Mengumpulkan                          |
| 88  | Al-Ghaniyyu           | الْغَنِيُّ                    | The Rich                    | Yang Maha Berkecukupan                          |
| 89  | Al-Mughnî             | الْمُغْنِيْ                   | The Enricher                | Yang Maha Memberi Kekayaan                      |
| 90  | Al-Mâni`u             | الْمَانِعُ                    | The Preventer               | Yang Maha Mencegah                              |
| 91  | Aḍ-Ḍâru               | الضَّارُ                      | The Distressor              | Yang Maha Memberi Derita                        |
| 92  | An-Nâfi`u             | النَّافِعُ                    | The Benefactor              | Yang Maha Memberi Manfaat                       |
| 93  | An-Nûru               | النُّوْرُ                     | The Light                   | Yang Maha Bercahaya (Menerangi, Memberi Cahaya) |
| 94  | Al-Hâdî               | الْهَادِيْ                    | The Guide                   | Yang Maha Pemberi Petunjuk                      |
| 95  | Al-Badî`u             | الْبَدِيْعُ                   | The Originator              | Yang Maha Pencipta                              |
| 96  | Al-Bâqî               | الْبَاقِيْ                    | The Everlasting             | Yang Mahakekal                                  |
| 97  | Al-Wâritsu            | الْوَارِثُ                    | The Heir                    | Yang Maha Pewaris                               |
| 98  | Ar-Rasyîdu            | الرَّشِيْدُ                   | The Guide to the Right Path | Yang Mahapandai                                 |
| 99  | Ash-Shabûru           | الصَّبُوْرُ                   | The Patient                 | Yang Mahasabar                                  |

**Reference:** For the full list, Quranic verses, and scholarly sources, see [Names of God in Islam (Wikipedia)](https://en.wikipedia.org/wiki/Names_of_God_in_Islam).

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
