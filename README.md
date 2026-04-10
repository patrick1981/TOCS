# Physical Media Cataloging SOP 

## 1. Objective
To maintain a high-fidelity, scannable Table of Contents (ToC) that maps physical disc locations to specific episode content, ensuring the collection is organized by genre and season.

## 2. Structural Requirements
* **Grid System:** 3-Column Table.
    * **Column 1 (Series Title):** The name of the show and the specific season.
    * **Column 2 (Disc #):** Relative numbering in the format **"Disc x of y"**.
    * **Column 3 (Episode Titles):** A comma-separated list of episodes found on that specific disc.
* **Total Capacity:** 336 slots.
* **Remaining Balance:** Every ToC update must conclude with a "Total Slots Occupied" and "Remaining Slots" tally.

## 3. Formatting Standards
* **Title Logic:** The **Series Title (Season #)** is entered **only once** at the beginning of a season's run. All subsequent discs for that season leave Column 1 blank.
* **Naming Convention:** Header must strictly follow `**Series Title (Season #)**`.
* **Column Widths (HTML Only):** * Series Title: ~22% (or 200px)
    * Disc #: ~18% (or 150px)
    * Episode Title: Auto/Remaining width.

## 4. Genre Classification Policy
* **Strict Thematic Filtering:** Only series clearly identified as the book's primary theme (e.g., Sci-Fi) are included.
* **Edge Case Resolution:** Series with primary tags like "Historical Drama," "Psychological Horror," or "Western" are excluded even if they contain minor supernatural or sci-fi elements (e.g., *The Terror*, *Castle Rock*).

## 5. Information Retrieval Workflow
1.  **Input:** User provides a list of titles or images of box sets.
2.  **Data Verification:**
    * Check for format (Blu-ray vs. DVD) as this dictates disc count.
    * Use network search to confirm the specific episode-to-disc mapping for that retail release.
3.  **Drafting:** Generate the table in Markdown for immediate review.
4.  **Finalization:** Convert the confirmed list into a standalone HTML file for browser viewing and printing.

## 6. Maintenance & Updates
* **New Book Trigger:** When a book reaches 336 slots, the system prompts for the creation of a new Book/ToC.
* **Revision:** Any change to a series (e.g., swapping a 5-disc set for a 6-disc set) requires a full recount of the binder's occupied slots.

---
