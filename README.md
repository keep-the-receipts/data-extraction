# Procurement Data Cleaning

Thanks for offering to help out!
For more info, join: http://join.keepthereceipts.org.za/
or Slack, channel #keep-the-receipts on https://zatech.co.za/

## Basic steps to get started:
- Download and install Tabula: https://tabula.technology/
- Download a copy of the PDF from the Git issue that you will be processing.
- Load the PDF into Tabula.
- Highlight/select the tables in Tabula, export to CSV.
- Open the CSV files in a spreadsheet app (Excel / Google Sheets / LibreOffice)
- Examine the CSV, and make any adjustments:
-- DON'T fix any spelling mistakes or typos, these should match the original document as closely as possible.
-- DON'T remove the headings for the table.
-- DO remove any totals rows - we are interested in individual line items, not totals.
-- DO remove any empty lines that aren't needed.
- Save the resulting CSV file, which you will use for creating the Pull Request. Use the same name as the source PDF file for the CSV (naturally replacing the .pdf extension with .csv).
- Raise a PR using the Github UI.

## If you're already familiar with Git, some extra tips:
- Fork https://github.com/South-Africa-Government-Procurement/Data-cleaning into your own account.
- You can work in `master` or use branches - up to you.
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