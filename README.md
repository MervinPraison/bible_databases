# Bible Versions and Cross-Reference Databases: MySQL, SQLite, CSV, JSON, YAML, TXT, MD.

This is a collection of bible versions in different formats. Here are some quick introductions:

- Find the bible versions you are looking for in the [Formats Folder](./formats).
- Find the source texts/resources in the [Sources Folder](./sources).
- Utilize the production / conversion scripts for this project in the [Scripts Folder](./scripts).
- A large and accurate cross-reference resource is included from https://www.openbible.info/labs/cross-references/ 

See the simple [DOCUMENTATION](https://github.com/scrollmapper/bible_databases/blob/2025/docs/README.md).

> **⚠️ Important: The legacy version of this project is available on the [2024](https://github.com/scrollmapper/bible_databases/tree/2024) branch. Please note that significant changes to the database schema have been implemented in the 2025 branch and subsequent versions.**


## Available Translations (30)

- **ACV (en)**: ACV: A Conservative Version
- **ASV (en)**: ASV: American Standard Version (1901)
- **BBE (en)**: BBE: 1949/1964 Bible in Basic English
- **BSB (en)**: BSB: Berean Standard Bible
- **CPDV (en)**: CPDV: Catholic Public Domain Version
- **DRC (en)**: DRC: Douay-Rheims Bible, Challoner Revision
- **Darby (en)**: Darby: Darby Bible (1889)
- **Geneva1599 (en)**: Geneva1599: Geneva Bible (1599)
- **JPS (en)**: JPS: Jewish Publication Society Old Testament
- **Jubilee2000 (en)**: Jubilee2000: English Jubilee 2000 Bible
- **KJV (en)**: KJV: King James Version (1769) with Strongs Numbers and Morphology and CatchWords
- **KJVA (en)**: KJVA: King James Version (1769) with Strongs Numbers and Morphology and CatchWords, including Apocrypha (without glosses)
- **KJVPCE (en)**: KJVPCE: King James Version: Pure Cambridge Edition
- **LEB (en)**: LEB: The Lexham English Bible
- **LITV (en)**: LITV: Green's Literal Translation
- **MKJV (en)**: MKJV: Green's Modern King James Version
- **NHEB (en)**: NHEB: New Heart English Bible
- **NHEBJE (en)**: NHEBJE: New Heart English Bible: Jehovah Edition
- **NHEBME (en)**: NHEBME: New Heart English Bible: Messianic Edition
- **Noyes (en)**: Noyes: 1869 Noyes Translation
- **OEB (en)**: OEB: Open English Bible (US Spelling)
- **RLT (en)**: RLT: Revised Literal Translation (2018) of the King James Version with Strongs Numbers and Morphology
- **RWebster (en)**: RWebster: Revised Webster Version (1833)
- **Rotherham (en)**: Rotherham: The Emphasised Bible by J. B. Rotherham
- **Twenty (en)**: Twenty: Twentieth Century New Testament
- **Tyndale (en)**: Tyndale: William Tyndale Bible (1525/1530)
- **UKJV (en)**: UKJV: Updated King James Version
- **WLC (hbo)**: WLC: Westminster Leningrad Codex
- **Webster (en)**: Webster: Webster Bible
- **YLT (en)**: YLT: Young's Literal Translation (1898)

## Database Schema

The following sections describe the general database schema used in this project:

#### Table: `<translation>_books`
This table lists all the books in the given translation of the Bible.

| Column Name | Type          | Nullable | Key         | Default | Extra          | Description                       |
|-------------|---------------|----------|-------------|---------|----------------|-----------------------------------|
| `id`        | int           | NO       | Primary Key | NULL    | auto_increment | Unique identifier for each book.  |
| `name`      | varchar(255)  | YES      |             | NULL    |                | The name of the book.             |

#### Table: `<translation>_verses`
This table contains all the verses in the given translation of the Bible.

| Column Name | Type          | Nullable | Key         | Default | Extra          | Description                       |
|-------------|---------------|----------|-------------|---------|----------------|-----------------------------------|
| `id`        | int           | NO       | Primary Key | NULL    | auto_increment | Unique identifier for each verse. |
| `book_id`   | int           | YES      | Index       | NULL    |                | The ID of the book (foreign key to `<translation>_books`). |
| `chapter`   | int           | YES      |             | NULL    |                | The chapter number.               |
| `verse`     | int           | YES      |             | NULL    |                | The verse number.                 |
| `text`      | text          | YES      |             | NULL    |                | The text of the verse.            |

#### Table: `translations`
This table contains information about the available Bible translations.

| Column Name  | Type          | Nullable | Key         | Default | Extra | Description                    |
|--------------|---------------|----------|-------------|---------|-------|--------------------------------|
| `translation`| varchar(255)  | NO       | Primary Key | NULL    |       | The abbreviation of the translation. |
| `title`      | varchar(255)  | YES      |             | NULL    |       | The full title of the translation. |
| `license`    | text          | YES      |             | NULL    |       | The license information for the translation. |

#### Table: `cross_references`
This table contains cross-reference data between different verses.

| Column Name     | Type          | Nullable | Key         | Default | Extra          | Description                           |
|-----------------|---------------|----------|-------------|---------|----------------|---------------------------------------|
| `id`            | int           | NO       | Primary Key | NULL    | auto_increment | Unique identifier for each cross-reference entry. |
| `from_book`     | varchar(255)  | YES      | Index       | NULL    |                | The book from which the cross-reference starts. |
| `from_chapter`  | int           | YES      |             | NULL    |                | The chapter number in the `from_book`. |
| `from_verse`    | int           | YES      |             | NULL    |                | The verse number in the `from_book`. |
| `to_book`       | varchar(255)  | YES      | Index       | NULL    |                | The book to which the cross-reference points. |
| `to_chapter`    | int           | YES      |             | NULL    |                | The chapter number in the `to_book`. |
| `to_verse_start`| int           | YES      |             | NULL    |                | The starting verse number in the `to_book`. |
| `to_verse_end`  | int           | YES      |             | NULL    |                | The ending verse number in the `to_book`. |
| `votes`         | int           | YES      |             | NULL    |                | The number of votes indicating the relevance of the cross-reference. |


# MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
