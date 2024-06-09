# Enhancing publication data in the university bibliography

## Table of Contents

- [Aim](#aim)
- [Considerations for the three databases](#considerations-for-the-three-databases)
- [Overview of the workflow](#overview-of-the-workflow)
- [Preparation of journal lists](#preparation-of-journal-lists)
- [Matching publication data from the university bibliography](#matching-publication-data-from-the-university-bibliography)

## Aim

Concerning a university's bibliography, the question might arise which publications have undergone peer review. To our knowledge, there is no web service where one could automatically request this information, e.g., based on a DOI. It can be argued that the indexing in established databases may serve as a proxy for peer review. This workflow can therefore be used to check whether articles have been published in journals indexed in Scopus, the different Web of Science indices, or MEDLINE, respectively. The matching is performed based on ISSNs only, regardless of the year of indexing. It therfore ignores that journals might lose their indexing status again. We accept this limitation, as we only look at articles published within the last year.

## Overview of the workflow

- Bring the list of indexed journals of each database into Open Refine.
- Modify the list so that all ISSNs for a journal are in one column in separate rows, i.e. only one ISSN per cell.
- Match ISSNs from articles in the university bibliography with indexed journals based on ISSNs. 
- Add the following information to the university bibliography download:
    - In which database(s) is the jounral indexed?
    - When was the database used for the check last updated?

## Considerations for the three databases

- Do they assess peer review as part of their journal selection process?
- How to download a list of indexed journals?
- How often are the lists of indexed journals updated?

All sources were last accessed on 2024-05-20.

### Web of Science

#### Selection process

> Journals that meet the quality criteria enter Emerging Sources Citation Index™ (ESCI). Journals that meet the additional impact criteria enter Science Citation Index Expanded™ (SCIE), Social Sciences Citation Index™ (SSCI) or Arts & Humanities Citation Index (AHCI) depending on their subject area. 

> Initial Triage: Presence of Peer Review Policy: The journal must provide a readily accessible, clear statement of its commitment to peer review and/or editorial oversight of all published content. Primary research articles must be subject to external peer review. Types of review that are particular to certain scholarly communities, where they are broadly accepted (e.g., arts or law journals) will be taken into consideration.

> Editorial Evaluation (quality): Peer Review: Published content must reflect adequate and effective peer review and/or editorial oversight. Signs of deficient peer review include, but are not limited to, articles that demonstrate lack of scholarly rigor or scientific validity, presence of articles outside the scope of the journal or irrelevant citations.

> -- <cite>[Web of Science Journal Evaluation Process and Selection Criteria](https://clarivate.com/products/scientific-and-academic-research/research-discovery-and-workflow-solutions/webofscience-platform/web-of-science-core-collection/editorial-selection-process/editorial-selection-process/)</cite>

#### Updates

> The list of journals is updated on an at least monthly basis, but some journal profile data is updated on a daily or weekly basis. 

> -- <cite>[Web of Science help center](https://mjl.clarivate.com/help-center)</cite>

### Scopus

#### Selection process

 >   To be considered for review, journal titles should meet all of these minimum criteria:

 >  * Consist of peer-reviewed content and have a publicly available description of the peer review process
 >  * Be published on a regular basis and have an International Standard Serial Number (ISSN) as registered with the ISSN International Centre(opens in new tab/window)
 >  * Have content that is relevant for and readable by an international audience, meaning: have English language abstracts and titles
 >  * Have a publicly available publication ethics and publication malpractice statement

> -- <cite>[Scopus journals scope and selection criteria](https://beta.elsevier.com/products/scopus/content/content-policy-and-selection#4-journals)</cite>


#### Updates

> The title lists and the Sources section are updated 2-3 times per year and include only journals and books with substantial coverage on Scopus.com at the time of the update.
> Titles that are newly added to Scopus will be visible in the title list and the Sources section only as of the next update after the first content appears on Scopus. To check whether the content of a recently added title is already available on Scopus, perform an advanced search on Scopus.com using the search code Source Title (SRCTITLE) and entering the name of the title.

> -- <cite>[Scopus content coverage](https://assets.ctfassets.net/o78em1y1w4i4/EX1iy8VxBeQKf8aN2XzOp/c36f79db25484cb38a5972ad9a5472ec/Scopus_ContentCoverage_Guide_WEB.pdf)</cite>
        
### MEDLINE

#### Selection process

> Editorial Policies and Processes

>   * Is the peer review process explicit and sufficiently detailed, including information on type of peer review and the number of reviewers typically assigned to a manuscript?
>   * Does the journal have a policy for the review of articles authored by editors and editorial board members (if applicable)?

> -- <cite>[Journal Selection for MEDLINE / Scientific and Editorial Quality Assessment](https://www.nlm.nih.gov/medline/medline_journal_selection.html)</cite>

Side note: All journals ever indexed in MEDLINE can be found in the [List of Serials Indexed for Online Users](https://www.nlm.nih.gov/tsd/serials/lsiou.html).

#### Updates

The search can be updated daily.

## Preparation of journal lists

### Web of Science

#### Downloading Title Lists
1. **Log in to Clarivate**: You need a Clarivate login to download the journal title lists from the Web of Science (WoS) indices. Visit the [Clarivate Collection List Downloads](https://mjl.clarivate.com/collection-list-downloads) page. Note down the date of the last upadate (in this example: 2024-05-20).
2. **Download Title Lists**: Download the title lists for the different WoS indices such as ESCI, SCIE, SSCI, and AHCI. 

#### Loading Data into Open Refine
1. **Create a New Project**: Click on "Create Project" and select "Choose Files" to upload the title list file(s) you downloaded. If using multiple indices, upload the files simultaneously.
2. **Configure Project**: Click "Configure parsing options" and make any changes if necessary (all settings should be fine). Enter a meaningful project name, e.g. "WebOfScience_2024-05". Click "Create Project" to load the data.

#### Applying the Script
1. **Use the Script**: Apply the provided Open Refine script ([WebOfScience.json](https://github.com/evamarik/OpenRefine_Journal_Article_Metadata_EAHIL2024/blob/main/WebOfScience.json)) to the loaded data. This script automates several cleaning and transformation steps.
   - In Open Refine, go to "Undo/Redo" > "Apply..." and upload the `WebOfScience.json` file.
   - Please find a description of how to recreate the script manually below.

#### Transformations and Cleaning Steps
1. **Rename Column**: Rename the `File` column to `Database`.
   - Click on the dropdown arrow next to the `File` column header.
   - Select "Edit column" > "Rename this column" and enter `Database`.
2. **Update Entries**: Update entries in the `Database` column to reflect the WoS indices:
   - "Arts & Humanities Citation Index (AHCI).csv" → "WoS-AHCI"
   - "Emerging Sources Citation Index (ESCI).csv" → "WoS-ESCI"
   - "Science Citation Index Expanded (SCIE).csv" → "WoS-SCIE"
   - "Social Sciences Citation Index (SSCI).csv" → "WoS-SSCI"
   - To do this, click on the dropdown arrow next to the `Database` column header, select "Facets" > "Text facet", and update the entries in the facet manually.
3. **Create `journal_info` Column**: Combine the journal name and publisher into a new column named `journal_info`.
   - Click on the dropdown arrow next to the `Journal title` column header.
   - Select "Edit column" > "Add column based on this column..."
   - Enter the following expression:
     ```grel
     join([cells['Journal title'].value, cells['Publisher name'].value], ' ; ')
     ```
     and name the new column `journal_info`.
4. **Combine ISSNs**: Combine the `ISSN` and `eISSN` columns into a single column named `ISSNs`, with values separated by a semicolon.
   - Click on the dropdown arrow next to the `ISSN` column header.
   - Select "Edit column" > "Add column based on this column..."
   - Enter the following expression: 
     ```grel
     join([cells['ISSN'].value, cells['eISSN'].value], ';')
     ```
     and name the new column `ISSNs`.
5. **Remove and re-order Columns**: Remove all columns that are not needed for further analysis.
   - Click on the dropdown arrow next to the `All` column header. Select "Edit columns" > "Re-order / remove columns..."
   - Drag and drop the column headers to remove them. Only keep columns `journal_info`, `ISSNs`, and `Database`, and rearrange them in this order.
6. **Split Multi-valued Cells**: Split the `ISSNs` column, which contains multiple values, into individual rows using the separator ";".
   - Click on the dropdown arrow next to the `ISSNs` column header.
   - Select "Edit cells" > "Split multi-valued cells..." and enter ";" as the separator.
8. **Fill Down Values**: Fill down values in the `Database` and `journal_info` columns.
   - Click on the dropdown arrow next to each column header, select "Edit cells" > "Fill down".
9. **Add `Database(Last_Update)` Column**: Create a new column named `Database(Last_Update)` based on the `Database` column.
   - Click on the dropdown arrow next to the `Database` column header.
   - Select "Edit column" > "Add column based on this column..."
   - Enter the following expression:
     ```grel
     "2024-05-20 ("+value+")"
     ```
     and name the new column `Database(Last_Update)`.
10. Export the data as a tsv file and save it into a new folder named, e.g., "All_Databases".


### Scopus

#### Downloading Title Lists
* Starting point: Download the Source title list from [Scopus Title List](https://beta.elsevier.com/products/scopus/content?trial=true#4-titles-on-scopus).
* Note down the date of the last update from the first worksheet of the file (in this example: "Scopus Sources Oct. 2023" > "2023-10").
* To reduce the data size and complexity for Open Refine, delete all worksheets except the first one (e.g., "Scopus Sources Oct. 2023"). In this worksheet, delete all columns from column U ("All Science Journal Classification Codes (ASJC)") onwards, and export the file as a csv file.

#### Loading Data into OpenRefine
1. **Create a New Project**: Click on "Create Project" and select "Choose Files" to upload the title list file. 
2. **Configure Project**: Make any changes if necessary (all settings should be fine). Enter a meaningful project name, e.g. "Scopus_2024-05". Click "Create Project" to load the data.

#### Applying the Script
1. **Use the Script**: Apply the provided Open Refine script ([Scopus.json](https://github.com/evamarik/OpenRefine_Journal_Article_Metadata_EAHIL2024/blob/main/Scopus.json)) to the loaded data. 
   - In Open Refine, go to "Undo/Redo" > "Apply..." and upload the `Scopus.json` file.
   - Please find a description of how to recreate the script manually below.

#### Transformations and Cleaning Steps
1. **Remove Inactive Rows**: Remove rows where the `Active or Inactive` column is set to "Inactive".
   - Create a facet by clicking on the dropdown arrow next to the `Active or Inactive` column header and select "Facet" > "Text facet".
   - In the facet panel, choose "Inactive" and then click on "Edit rows" > "Remove all matching rows".
2. **Remove Non-Journal Rows**: Remove rows where the `Source Type` is not "Journal" to exclude Trade Journals.
   - Create a facet by clicking on the dropdown arrow next to the `Source Type` column header and select "Facet" > "Text facet".
   - In the facet panel, choose "Journal". Invert the selection and then click on "Edit rows" > "Remove all matching rows".
3. **Create `ISSNs` Column**: Combine the `Print-ISSN` and `E-ISSN` columns into a single column named `ISSNs`, with values separated by a semicolon.
   - Click on the dropdown arrow next to the `Print-ISSN` column header.
   - Select "Edit column" > "Add column based on this column..."
   - Enter the following expression:
     ```grel
     join([cells['Print-ISSN'].value, cells['E-ISSN'].value], ';')
     ```
     and name the new column `ISSNs`.
4. **Split Multi-valued Cells**: Split the `ISSNs` column, which contains multiple values, into individual rows using the separator ";".
   - Click on the dropdown arrow next to the `ISSNs` column header.
   - Select "Edit cells" > "Split multi-valued cells..." and enter ";" as the separator.
5. **Transform ISSN Format**: Ensure the ISSNs are correctly formatted.
   - Click on the dropdown arrow next to the `ISSNs` column header.
   - Select "Edit cells" > "Transform..." and enter the following expression: 
     ```grel
     value.find(/\d{3}[\dxX]/).join("-")
     ```
6. **Create `journal_info` Column**: Combine the source title and publisher into a new column named `journal_info`.
   - Click on the dropdown arrow next to the `Source Title` column header.
   - Select "Edit column" > "Add column based on this column..."
   - Enter the following expression:
     ```grel
     join([cells['Source Title'].value, cells['Publisher's Name'].value], ' ; ')
     ```
     and name the new column `journal_info`.
7. **Remove and re-order Columns**: Remove columns that are not needed for further analysis.
   - Click on the dropdown arrow next to the `All` column header. Select "Edit columns" > "Re-order / remove columns...".
   - Drag and drop the column headers to remove them. Only keep columns `journal_info`, `ISSNs`, and `Database`, and rearrange them in this order.
8. **Add `Database` Column**: Create a new column named `Database` with a static value "Scopus".
   - Click on the dropdown arrow next to any column header.
   - Select "Edit column" > "Add column based on this column..."
   - Enter the following expression: "Scopus" and name the new column `Database`.
9. **Fill Down Values**: Fill down values in the `journal_info` column.
   - Click on the dropdown arrow next to the `journal_info` column header, select "Edit cells" > "Fill down".
10. **Add `Database(Last_Update)` Column**: Create a new column named `Database(Last_Update)` based on the `Database` column.
    - Click on the dropdown arrow next to the `Database` column header.
    - Select "Edit column" > "Add column based on this column..."
    - Enter the following expression:
      ```grel
      "2023-10 ("+value+")"
      ```
      and name the new column `Database(Last_Update)`.
11. Export the data as a tsv file and save it into the "All_Databases" folder.

### MEDLINE

#### Downloading Title Lists
* Starting point: To retrieve a list of all journals currently indexed in MEDLINE, search the NLM catalogue for [journals "currentlyindexed"](https://www.ncbi.nlm.nih.gov/nlmcatalog/?term=currentlyindexed)
* Export results in "Summary (Text)" format by clicking on "Sent to" > "File".
* Note down the date of the search, e.g. 2024-05-31.

#### Loading Data into OpenRefine
1. **Create a New Project**: Click on "Create Project" and select "Choose Files" to upload the title list file. 
2. **Configure Project**: Make any changes if necessary (all settings should be fine). Enter a meaningful project name, e.g. "MEDLINE_2024-05-31". Click "Create Project" to load the data.

#### Applying the Script
1. **Use the Script**: Apply the provided OpenRefine script ([MEDLINE.json(https://github.com/evamarik/OpenRefine_Journal_Article_Metadata_EAHIL2024/blob/main/MEDLINE.json)) to the loaded data. 
   - In OpenRefine, go to "Undo/Redo" > "Apply..." and upload the `MEDLINE.json` file.
   - Please find a description of how to recreate the script manually below.

### Transformations and Cleaning Steps
1. **Rename Column**: Rename the `Column 1` column to `journal_info`.
   - Click on the dropdown arrow next to the `Column 1` column header.
   - Select "Edit column" > "Rename this column" and enter "journal_info".
2. **Create `journal` Column**: Extract the journal information from `journal_info` and create a new column named `journal`.
   - Click on the dropdown arrow next to the `journal_info` column header.
   - Select "Edit column" > "Add column based on this column..."
   - Enter the following expression:
   ```grel
   if(value.contains(/^\d+\. /), value, "")
   ```
   and name the new column `journal`. This expression extracts all lines starting with a number (one or more digits), followed by a dot and then a space.
3. **Reorder Columns**: Reorder the columns to ensure `journal` is the primary column.
   - Click on the dropdown arrow next to the `All` column header. Select "Edit columns" > "Re-order / remove columns...".
   - Drag and drop the column headers to rearrange them.
5. **Join Multi-valued Cells**: Join multi-valued cells in the `journal_info` column.
   - Click on the dropdown arrow next to the `journal_info` column header.
   - Select "Edit cells" > "Join multi-valued cells" and use a space as the separator.
6. **Create `ISSNs` Column**: Extract ISSNs from `journal_info` and create a new column named `ISSNs`.
   - Click on the dropdown arrow next to the `journal_info` column header.
   - Select "Edit column" > "Add column based on this column..."
   - Enter the following expression: 
    ```grel
    value.find(/ISSN:(.*)/)[0].split(".")[0].split("ISSN:")[0]
    ```
    and name the new column `ISSNs`.
7. **Extract `ISSNs`**: Extract only ISSN numbers from the information in the column `ISSNs`.
   - Click on the dropdown arrow next to the `ISSNs` column header.
   - Select "Edit cells" > "Transform..." and enter the following expression:
     ```grel
     value.find(/\d{4}-\d{3}[\dxX]/).join(";")
     ```
7  - Click on the dropdown arrow next to the `ISSNs` column header.
   - Select "Edit cells" > "Split multi-valued cells..." and enter ";" as the separator.
8. **Remove `journal` Column**: Remove the `journal` column as it is no longer needed.
   - Click on the dropdown arrow next to the `journal` column header and select "Edit column" > "Remove this column".
9. **Fill Down Values**: Fill down values in the `journal_info` column.
    - Click on the dropdown arrow next to the `journal_info` column header, select "Edit cells" > "Fill down".
10. **Add `Database` Column**: Create a new column named `Database` with a static value "MEDLINE".
    - Click on the dropdown arrow next to any column header.
    - Select "Edit column" > "Add column based on this column..."
    - Enter: "MEDLINE" and name the new column `Database`.
11. **Add `Database(Last_Update)` Column**: Create a new column named `Database(Last_Update)` based on the `Database` column.
    - Click on the dropdown arrow next to the `Database` column header.
    - Select "Edit column" > "Add column based on this column..."
    - Enter the following expression:
    ```grel
    "2024-05-31 ("+value+")"
    ```
    and name the new column `Database(Last_Update)`.
12. Export the data as a tsv file and save it into the "All_Databases" folder.

### Create a file containing journal lists of all databases

#### Loading Data into OpenRefine
1. **Create a New Project**: Click on "Create Project" and select "Choose Files" to simultaneously upload all tsv files you exported in the previous steps.
2. **Configure Project**: Click "Configure parsing options" and make any changes if necessary (all settings should be fine). Enter a meaningful project name, e.g. "All_databases_2024-05". Click "Create Project" to load the data.

## Matching publication data from the university bibliography

### Download and prepare data from the university bibliography

#### Example data
In this example, we will use data from the [publication server of the University of Augsburg](https://opus.bibliothek.uni-augsburg.de/opus4/home). To select a small subset, we select articles published by members of the Faculty of Medicine in 2024, as recorded in OPUS on 2024-06-03, i.e.:
   - `Document type`: "article"
   - `Year of Publication`: "2024"
   - `Institute`: "Medizinische Fakultät"

On 2024-06-03, this gave 236 results. The full metadata can be downloaded in XML format in the IP range of the university. For the workshop, the file can be downloaded here: [2024-06-04_OPUS_Export_Articles_Med.xml](https://github.com/evamarik/OpenRefine_Journal_Article_Metadata_EAHIL2024/blob/main/2024-06-04_OPUS_Export_Articles_Med.xml)

#### Loading data in Open Refine**: 
1. **Create a New Project**: Click on "Create Project" and select "Choose Files" to upload the xml file. 
2. **Configure Project**: Select "Parse as XML file". Open Refine asks you to "Click on the first XML element corresponding to the first record to load". Select the first article (starting with "<Opus_Document Id="110428" ..."). Enter a meaningful project name, e.g. "Articles_2024_Med_2024-06-04". Click "Create Project" to load the data.

#### Applying the Script
1. **Use the Script**: Apply the provided Open Refine script ([OPUS_Export_ISSN_Matching.json](https://github.com/evamarik/OpenRefine_Journal_Article_Metadata_EAHIL2024/blob/main/OPUS_Export_ISSN_Matching.json)) to the loaded data. 
   - In OpenRefine, go to `Undo/Redo` > `Apply...` and upload the `OPUS_Export_ISSN_Matching.json` file.
   - Please find a description of how to recreate the script manually below.

#### Transformations and Cleaning Steps

1. **Reove and Re-order Columns**: 
   - Click on the dropdown arrow next to the `All` column header. Select "Edit columns" > "Re-order / remove columns...".
   - Remove all columns first.
   - Then, search for the columns of interest and include them in the following order:
     - "Opus_Document - Id"
     - "Opus_Document - PublishedYear"
     - "Opus_Document - IdentifierDoi - Value"
     - "Opus_Document - TitleMain - Value"
     - "Opus_Document - TitleParent - Value"
     - "Opus_Document - PublisherName"
     - "Opus_Document - IdentifierIssn - Value"

2. **Rename Columns**:
Manually, this can be done one by one, by clicking on the dropdown arrow next to each column heading and selecting "Edit colum" > "Rename this colum".
   - "Opus_Document - Id" → "OPUS-ID"
   - "Opus_Document - PublishedYear" → "PublishedYear"
   - "Opus_Document - IdentifierDoi - Value" → "DOI"
   - "Opus_Document - TitleMain - Value" → "ArticleTitle"
   - "Opus_Document - TitleParent - Value" → "Journal"
   - "Opus_Document - PublisherName" → "Publisher"
   - "Opus_Document - IdentifierIssn - Value" → "ISSNs"

**Summary**: 

| Column Name  | Initial name in the example XML (OPUS download) | Notes |
|--------------|-------------------------------------------------|-------|
| OPUS-ID | Opus_Document - Id | internal unique identifier of the repository | |
| PublishedYear | Opus_Document - PublishedYear | |
| DOI | Opus_Document - IdentifierDoi - Value | |
| ArticleTitle | OPUS_Document - TitleMain - Value |  This column can have more than one entry per record (each in a separate row), e.g. subtitle or translated title |
| Journal | Opus_Document - TitleParent - Value | |
| Publisher | Opus_Document - PublisherName | | 
| ISSNs | Opus_Document - IdentifierIssn - Value | This column can have more than one entry per record (each in a separate row) |

3. **Join Multi-valued Cells in `ArticleTitle`**: Join multi-valued cells in the `ArticleTitle` column. Cells can have more than one entry due to, e.g., subtitles or translated titles.
   - Click on the dropdown arrow next to the `ArticleTitle` column header.
   - Select "Edit cells" > "Join multi-valued cells" and use `|` as the separator.

4. **Edit `ISSNs` Column**: For articles without a value in the ISSN column, write "NA" into the corresponding cells.
   - Click on the dropdown arrow next to the `OPUS-ID` column header.
   - Select "Facet" > "Customized facets" > "Facet by blank", select "False".
   - Enter "NA" into a blank cell and click on "Apply to all identical cells".

5. **Remove blank rows**: Remove rows where the `ISSNs` column is blank.
   - Create a facet by clicking on the dropdown arrow next to the `ISSNs` column header and select "Facet" > "Text facet".
   - In the facet panel, select "true" to filter out rows with blank `ISSNs`.
   - Click on "Edit rows" > "Remove all matching rows".

**Explanation**:
Step 3 already removes most empty rows. Steps 4 and 5 were added to ensure that articles without an ISSN recorded in OPUS will be preserved, allowing for a subsequent intellectual check of these articles. For the example data set, this is actually not neccessary, as all articles have entries in the ISSN field.

#### Match university bibliography with the journal indexed in databases

In the following steps, we will match the prepared journal list (named, e.g., "All_databases_2024-05") with journal article data from a university bibliography, based on the ISSNs. This will be done using Open Refine's cross function.

1. **Add `Indexed(Last_Update)` Column**: Create a new column `Indexed(Last_Update)` which lists the databases where each journal is indexed, and the last update of the respective database title list used.
    - Click on the dropdown arrow next to the `ISSNs` column header.
    - Select "Edit column" > "Add column based on this column..."
    - Enter the following expression:
```grel
forEach(cell.cross("All_databases_2024-05", "ISSNs"), v, v.cells["Database(Last_Update)"].value).uniques().join("|")
```

**Explanation:**

   - `cell.cross("All_databases_2024-05", "ISSNs")`: This part of the formula finds matching rows in the "All_databases_2024-05" project based on the "ISSNs" column.
   - `forEach(..., v, v.cells["Database(Last_Update)"].value)`: For each matching row (v), it retrieves the value from the "Database(Last_Update)" column.
   - `uniques()`: This ensures that each date-database combination is listed only once.
   - `join("|")`: This joins the unique date-database combination names into a single string, separated by pipes.

The following steps are only necessary if the dataset from the university bibliography contains more than one ISSN per record (in separate rows).

2. **Join values in the `Indexed(Last_Update)` and `ISSNs` Columns**
   - Click on the dropdown arrow next to the `Indexed(Last_Update)` column header.
   - Select "Edit cells" > "Join multi-valued cells" and use a `|` as the separator.
   - Click on the dropdown arrow next to the `ISSNs` column header.
   - Select "Edit cells" > "Join multi-valued cells" and use a `|` as the separator.

3. **Join values in the `Indexed(Last_Update)`column**: Ensure that each value is listed only once.
   - Click on the dropdown arrow next to the `Indexed(Last_Update)` column header and select `Edit cells` > `Transform...`.
   -  Enter the following expression:
   ```grel
   value.split("|").uniques().join("|")
   ```

4. Export the data in the desired format.

After following the entire workflow, the exported file should look like this: [Articles_2024_Med_2024-06-04_Indexed.tsv](https://github.com/evamarik/OpenRefine_Journal_Article_Metadata_EAHIL2024/blob/main/Articles_2024_Med_2024-06-04_Indexed.tsv).
  
