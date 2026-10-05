 Data Cleaning Log on Google Sheet

• Step 1: Detected and removed 17 duplicate rows from the dataset.

• Step 2: Identified 8 blank spaces in the description column and filled them with "Unknown Products" to preserve the overall data volume.
	• Formula used: =IF(ISBLANK(D2), "Unknown Product", D2)

• Step 3: Identified and resolved 5 blank entries in the country column by cross-referencing their corresponding Invoice numbers using an XLOOKUP formula to maintain geographical revenue integrity.
	• Formula used: =IF(LEN(TRIM(I2))=0, XLOOKUP(TRIM(A2), A:A, I:I, "Unspecified", 0), TRIM(I2))

• Step 4: Resolved 5 rows of date-time validation errors by switching the file locale from English (United States) to English (United Kingdom). To achieve the desired formatting, the entire column was formatted to date-time, converted to a custom dd/mm/yyyy hh:mm schema, and modified to a 12-hour structure by including AM/PM indicators. The suffixes were then extracted using a text function.
	• Formula used: =LEFT([DateTime], FIND(".", [DateTime]) - 1)

• Step 5: Applied TRIM and PROPER functions to standardize affected inconsistent text values in the description column.

• Step 6: Utilized Find and Replace to standardize and normalize country names across the dataset:
	• Updated RSA to Republic of South Africa
	• Updated 19 instances of EIRE to Ireland
	• Updated USA to United States of America
	• Updated 2 instances of UK to United Kingdom
	• Updated 2 instances of U.K. to United Kingdom
	• Applied TRIM and PROPER functions to ensure absolute consistency across all affected values.

• Step 7: Resolved blank entries in the Customer ID column by cross-referencing matching Invoice numbers using an XLOOKUP formula; any remaining anonymous guest checkouts without an associated account were assigned a placeholder ID of 99999 to preserve total transaction volume.
	• Formula used: =IF(LEN(TRIM(G2))=0, XLOOKUP(TRIM(A2), A:A, G:G, 99999, 0), TRIM(G2))

• Step 8: Dropped 5 rows containing missing values in the price column because they represent critical operational elements and should never be left blank.

• Step 9: Dropped 5 rows containing missing values in the quantity column because they represent critical operational elements and should never be left blank.
