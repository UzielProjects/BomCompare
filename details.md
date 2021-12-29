---
layout: page
---

### BOM file formats

The application is designed to import **EXCEL** files (`xls`/`xlsx`).

Most commonly used files are exported from **Altium Designer**, **OrCAD (CIS)** and **Agile** (to export an Agile BOM see @@@).

The BOM file:

1. May contain more then a single worksheet (_defaults to the first worksheet_. See [settings](#format-settings) below).
2. **Must** have a **header row**.
3. Data may start on **_any row_** below the header (_defaults to the second row_. See [settings](#format-settings) below).
4. Data **sorting is irrelevant** for all rows/columns.
5. The columns positions are user defined (or loaded from external file).
6. Used columns:
   - P/N - (**mandatory**) the items part number.
   - Comments/Value - (_optional_) the item's comment or value. _This data is not compared_.
   - Description - (_optional_) the item's description. _This data is not compared_.
   - Quantity - (**mandatory**) item's count.
   - Designators - (**mandatory**) item's reference designators.
7. Number of rows to import is unlimited (_default_) or set by the user.

### Format settings

(values are set when `Defaults` button is click)

- Worksheet index: **0** (first worksheet)
- Headers row: **1**
- Data start row: **1** (saved as relative to headers)
- Last row to import: **0** (auto-detect)
- Part numbers: **1**
- Comments/Value: **2**
- Description: **3**
- Quantity: **4**
- Designators: **5**

Sample settings files are installed with the application and can be downloaded:
[**Altium**](./docs/altium.xml), [**Agile**](./docs/orcad.xml)

### XML BOM file

The application saves the imported file as an **XML** file.

The file can also be opened using external text editor to validate the data imported.

Editing the file externally is OK but care must be taken not to change the file structure, since the file may fail a schema validation on opening it in the application.

### Compare and report

Once two files are loaded they can be compared to each other by clicking the `Tools\Compare` menu.

**NOTE:** The panel/file selected (border highlighted) when starting the check is the "base" file, compared to the second file which is the "changed" file.

If the application detects difference between the files, a pop-up message is displayed notifying the user to save an _optional_ error report.

The report is also shown in the lower message text box.

On the first lines the two file details are shown with general info.

The report consists of `DIFF` tag(s)/line(s) indicating the diff, followed by `=>` tag(s)/line(s), describing the necessary action to do in order to fix the diff between the files.

At the footer a sum total info is listed.

The compare is done is 3 phases:

- Extra P/N are "removed"
- Matched P/N items are compared
- Missing P/N are "added"

The matched P/N's are compared also in the same 3 phase strategy ("remove" extra parts, check matched, and "add" missing parts).
