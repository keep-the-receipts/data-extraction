# Procurement Data Cleaning

Thanks for offering to help out!
For more info, join: http://join.keepthereceipts.org.za/
or Slack, channel #keep-the-receipts on https://zatech.co.za/

## Basic steps to get started:
- Download and install Tabula: https://tabula.technology/
- Download a copy of the PDF from the GitHub issue that you will be processing.
- Load the PDF into Tabula.
- Highlight/select the tables in Tabula
- Check the export review. Tip: See whether the "Stream" or "Lattice" extraction method will give better results.
- Export the file to CSV.
- Open the CSV files in a spreadsheet app (Excel / Google Sheets / LibreOffice)
- Examine the CSV, and make any adjustments:
  - DON'T fix any spelling mistakes or typos, these should match the original document as closely as possible.
  - DON'T remove the headings for the table.
  - DO remove any totals rows - we are interested in individual line items, not totals.
  - DO remove any empty lines that aren't needed.
  - DO make sure that everything that is in one row on the PDF is one row on the CSV (More info here)[https://github.com/South-Africa-Government-Procurement/Data-cleaning/issues/104#issuecomment-703076609]
- Save the resulting CSV file, which you will use for creating the Pull Request. Use the same name as the source PDF file for the CSV (naturally replacing the .pdf extension with .csv).
- Raise a PR using the Github UI.
  - Include a screenshot of the table in the PDF and the CSV table in Excel/Calc/Google Sheets - that makes it a lot easier for us to spot issues quickly and discuss. See example https://github.com/South-Africa-Government-Procurement/Data-cleaning/pull/127

## If you're already familiar with Git, some extra tips:
- Fork https://github.com/South-Africa-Government-Procurement/Data-cleaning into your own account.
- It can be helpful to work branches, e.g. `patch-1`, `patch-2`, but this is up to you.
- The CSV files go into a folder structure matching the structure described here: https://github.com/South-Africa-Government-Procurement/project-docs/wiki/Data-models-and-standards#file-locations
- If you're not sure where a file should go - using the repository root is ok too - we'll move it later.
- For commits of new files, you can use "[#ISSUE-NUMBER] Create + file name".
- Raise a PR against the source repo, put a reference to the issue in the PR description so it will be linked.


## F.A.Q.:
1. Should we put different tables into different CSVs?

If the column headings are the same, they can be in one CSV. But if the tables relate to different departments or entities, add a column to specify who that part of the CSV relates to.
If the columns headings are different, they should be separate CSVs.

2. What should I do if there are merged cells that should be split?

Instructions for managing merged cells are here: https://github.com/South-Africa-Government-Procurement/Data-cleaning/pull/119#issuecomment-703073670

3. What should I do if Tabula splits cells that should be on a single row?
Instructions for this are here: https://github.com/South-Africa-Government-Procurement/Data-cleaning/issues/104#issuecomment-703076352

4. Should I do 'pass 2' of a file?

Preferably do pass 1 first, just so we easily keep track and ensure there's a first pass of everything.
Once Pass 1 is done, you can do pass 2 unless it was you who did pass 1.
The idea with two passes is to identify errors when by looking at the differences between two passes done by two different people

5. Tabula gives me the following error for the PDF: "Sorry, your PDF file is image-based; it does not have any embedded text. It might have been scanned from paper... Tabula isn't able to extract any data from image-based PDFs. Click the Help button for more information."

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
