# Physical Media Cataloging SOP 

## 1. Objective
To maintain high-fidelity, scannable Tables of Contents (ToCs) in both Markdown and HTML formats. These documents map physical disc locations to specific episode content, ensuring the collection remains organized by genre and season.

## 2. Structural Requirements
* **Grid System:** 3-Column Table.
    * **Column 1 (Series Title):** The name of the show and the specific season.
    * **Column 2 (Disc #):** Relative numbering in the format **"Disc x of y"**.
    * **Column 3 (Episode Titles):** A comma-separated list of episodes found on that specific disc.
* **Total Capacity:** 336 slots.
* **Remaining Balance:** Every ToC update must conclude with a "Total Slots Occupied" and "Remaining Slots" tally.

## 3. Formatting Standards
*Header:* {{Genre}} Table of Contents
* **Title Logic:** The **Series Title (Season #)** is entered **only once** at the beginning of a season's run. All subsequent discs for that season leave Column 1 blank.
* **Naming Convention:** Header must strictly follow `**Series Title (Season #)**`.
* **Column Widths (HTML Only):** * Series Title: ~22%
    * Disc #: ~18%
    * Episode Title: 60%
* **Clean Output:** The final outputs must not contain any AI-generated source citations.

## 4. Genre Classification Policy
* **Strict Thematic Filtering:** Only series clearly identified as the book's primary theme (e.g., Sci-Fi) are included.
* **Edge Case Resolution:ASK** 

## 5. Information Retrieval Workflow
** ASK USER FOR BINDER GENRE **
1.  **Input:** User provides a list of titles or images of box sets.
2.  **Data Verification:**
    * Check for format (Blu-ray vs. DVD) as this dictates disc count.
    * Use network search to confirm the specific episode-to-disc mapping for that retail release.
3.  **Generation:** Generate two distinct code blocks: one for the GitHub-Flavored Markdown file and one for the standalone HTML file.

## 6. Maintenance & Updates
* **New Book Trigger:** When a book reaches 336 slots, the system prompts for the creation of a new Book/ToC.
* **Revision:** Any change to a series (e.g., swapping a 5-disc set for a 6-disc set) requires a full recount of the binder's occupied slots.

---

## **Master Media Cataloging Prompt**

"Act as a professional archivist and database manager. I am organizing a physical media collection into **336-slot binders**. Your goal is to generate and maintain a **Table of Contents (ToC)** following these strict rules:

### **1. Structural Requirements**
* **Output Format:** Generate two separate code blocks. The first must be a GitHub-Flavored Markdown (`.md`) document formatted to accommodate a wide view. The second must be a clean HTML (`.html`) document. Do not truncate the code; provide the complete files.
* **Columns:** Three columns: **Series Title**, **Disc #**, and **Episode Title**.
* **Table Layout (HTML):** Set the table to `fixed` layout. Column 1 (Series) should be **22%**, Column 2 (Disc #) should be **18%**, and Column 3 (Episodes) should be **60%**.

### **2. Content & Formatting Rules**
* **Naming:** Use the exact format **"Series Title (Season #)"**.
* **Persistence:** Only display the **Series Title** on the first row of each season. Leave it blank for all subsequent discs in that season.
* **Relative Numbering:** Reset disc counts for every season (e.g., "Disc 1 of 5").
* **Episode Lists:** Provide comma-separated lists of every episode on each specific disc. If specific disc contents are unknown, use web search to find the retail breakdown for that specific Blu-ray/DVD set.
* **Thematic Filtering:** Only include series that match the specific book theme (e.g., Sci-Fi). If Unsure, pause  and ask for clarification.
* **No Citations:* Do not include any source citations (e.g., ``) in the output.

### **3. Operational Metrics**
* **Running Tally:** At the end of every update, calculate and display:
    * **Total Slots Occupied** (Sum of all discs listed).
    * **Remaining Slots** (336 minus total occupied).

### **4. Technical Styles (CSS for HTML)**
* Use `@media print` with `size: letter` and `margin: 0`.
* Set `thead { display: table-header-group; }` so headers repeat on every printed page.
* Ensure `tr { page-break-inside: avoid; }` so rows don't split across pages.
* **Orphan Prevention:** Use the CSS class `.new-page-section { page-break-before: always; }` on the first row of a major series to ensure the header and its content remain together on a fresh page."

---

### **How to use this prompt:**
1.  **Copy** everything between the quotes.
2.  **Paste** it into a new session.
3.  **Add** your series list or photo immediately after the prompt.
