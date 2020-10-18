# Procurement Data Extraction

Thanks for offering to help out!
For more info, join: http://join.keepthereceipts.org.za/
or Slack, channel #keep-the-receipts on https://zatech.co.za/

## Basic steps to get started:
- Download and install [Tabula](https://tabula.technology/)
- Download a copy of the PDF from the GitHub issue that you will be processing.
- Load the PDF into Tabula.
- Highlight/select the tables in Tabula, export to CSV.
- Open the CSV files in a spreadsheet app (Excel / Google Sheets / LibreOffice)
- Examine the CSV, and make any adjustments:
  - DON'T fix any spelling mistakes or typos, these should match the original document as closely as possible.
  - DON'T remove the headings for the table.
  - [DON'T remove total columns](https://github.com/keep-the-receipts/data-extraction/issues/11#issuecomment-711157413)
  - DO remove any totals rows - we are interested in individual line items, not totals.
  - DO remove any empty lines that aren't needed.
  - DO make sure that everything that is in one row or columns on the PDF is one row or column on the CSV [More info here](https://github.com/keep-the-receipts/data-extraction/issues/104#issuecomment-703076609)
- Save the resulting CSV file, which you will use for creating the Pull Request. Use the same name as the source PDF file for the CSV (naturally replacing the .pdf extension with .csv).
  - See the [correct folder layout for this repository](https://github.com/keep-the-receipts/project-docs/wiki/Data-models-and-standards#file-locations).
- Raise a PR using the Github UI.
  - Include a screenshot of the table in the PDF and the CSV table in Excel/Calc/Google Sheets - that makes it a lot easier for us to spot issues quickly and discuss. [See example](https://github.com/keep-the-receipts/data-extraction/pull/127)

## If you're already familiar with Git, some extra tips:
- Fork the [data-extraction](https://github.com/keep-the-receipts/data-extraction) repository into your own account.
- You can work in `master` or use branches - up to you.
- The CSV files go into a [folder structure matching the structure on the  OCPO website/government](https://github.com/keep-the-receipts/project-docs/wiki/Data-models-and-standards#file-locations)
- If you're not sure where a file should go - using the repository root is ok too - we'll move it later.
- For commits of new files, you can use "[#ISSUE-NUMBER] Create + file name".
- Raise a PR against the source repo, put a reference to the issue in the PR description so it will be linked.


## F.A.Q.:

### Which tables do we want?

We only want the tables that tie a specific supplier to a specific _organ of state_ - a specific national or provincial department, municipality, or public entity.

Summary tables that just show the total for each department, or is just a summary of a more granular table in the same document aren't needed - we just want the granular table.

### Should we put different tables into different CSVs?

If the column headings are the same, they can be in one CSV, however the source table and related entity/ department should be identified within the table. If the column headings are different, they should be included as separate csv files. 

Wherever relevant, insert a new column named "TABLE", preferrably in the first column (A) position and copy the table name into each row that is a part of that table. Similarly, if tables relate to multiple state entities, add a column named "ENTITY" and copy the entity name (this can be a lowercase department ID e.g. saps, treasury, cogta, drdlr) into all of the relevant rows.

If multiple output tables are required from a single source document, simply append an incremental suffix before the csv file extension which identifies the table number, e.g. *FILE01_output1.csv* or *FILENAME_output2.csv* . Note that using the term **_output0** is important as it is entirely possible that the input document could end in a number or other matching pattern. The ordering of these tables is not important, however they should contain a *TABLE* column as described above.

### What should I do if there are merged cells that should be split?

Instructions for managing merged cells are here: https://github.com/keep-the-receipts/data-extraction/pull/119#issuecomment-703073670

### What should I do if Tabula splits cells that should be on a single row?
Instructions for this are here: https://github.com/keep-the-receipts/data-extraction/issues/104#issuecomment-703076352

### Should I do 'pass 2' of a file?

Preferably do pass 1 first, just so we easily keep track and ensure there's a first pass of everything.
Once Pass 1 is done, you can do pass 2 unless it was you who did pass 1.
The idea with two passes is to identify errors when by looking at the differences between two passes done by two different people

### Tabula gives me the following error for the PDF: "Sorry, your PDF file is image-based; it does not have any embedded text. It might have been scanned from paper... Tabula isn't able to extract any data from image-based PDFs. Click the Help button for more information."

For PDFs like this, we need to use Optical Character Recognition (OCR) software to convert the image-based PDFs to text-based. This is easiest done on Linux or MacOS, but you have to download a bash script and run it on the PDF. If any of those things sound scary or foreign to you, feel free to reach out on the issue or in Slack and someone else will be happy to convert the PDF for you in the mean time.

If you wanna try download the bash script and run it on the PDF yourself, here is what you need to do:

1. Make sure you have tesseract 4 installed (`brew install tesseract` on MacOS)
1. Download the `pdf-ocr.sh` bash script from this gist: https://gist.githubusercontent.com/zoidbergwill/e48ddeab1552c868a4c140fd14c4aeb2/raw/bc44ee1a0a132d83b945fdacda479d52ac3dc1ed/pdf-ocr.sh
1. Make it executable:
  `chmod +x pdf-ocr.sh`
1. Run it on your scanned PDF.
  e.g. `./pdf-ocr.sh "HOME AFFAIRS - COVID SUMMARY.pdf"`

## Pull Request Review checks

_You will need to open the original PDF file to do comparisons/spot-checks_

- Does it capture all the data? (or is there another file or pull request for other tables, e.g. when it's different column headings in the different tables)
- Is the data in the correct column? Sometimes some rows are shifted and not aligned with the respective heading.
- Is each "record" - one supplier, one buyer, one order amount - in one row? Sometimes tabula splits multiline cells into multiple rows - these must be single rows (with multiple lines as in the PDF table) in the CSV.
