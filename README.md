# PHYSICAL MEDIA CATALOGING SYSTEM - COMPLETE PACKAGE
=====================================================

This document contains all the necessary components for your Physical Media Cataloging System.
1. README / SOP (Standard Operating Procedure)
2. MASTER ARCHIVIST PROMPT (To be pasted into AI)
3. SAMPLE HTML STRUCTURE (For reference)

-------------------------------------------------------------------------------
PART 1: README & SOP
-------------------------------------------------------------------------------
# Physical Media Cataloging System (v5)

An optimized workflow for mapping physical disc locations to digital Table of Contents (ToCs) for 336-slot binders.

## 🛠 Features & Rules
1. **Dynamic Header:** Supports '{{Genre}} Table of Contents' for easy identification.
2. **Fixed Column Logic:** HTML output is hardcoded to a 22/18/60 split for readability.
3. **Async Handling:** "Unsure" discs (Category B) are queued so they don't block known titles.
4. **Append Protection:** Defaults to "Append" mode to prevent physical re-indexing of 300+ discs.
5. **Print Ready:** HTML includes repeating headers and page-break prevention.

## 📝 How to Use
1. Copy the 'MASTER PROMPT' section below.
2. Paste it into your AI session.
3. Upload your current catalog file (or paste the text) when asked.
4. Supply new titles via list, UPC, or photo.

-------------------------------------------------------------------------------
PART 2: MASTER ARCHIVIST PROMPT
-------------------------------------------------------------------------------
**Act as a Professional Media Archivist.**

### 1. Initialization & Structural Intent
I am cataloging physical media into **336-slot binders**. 
* **The 'No-Reorg' Rule:** Always ask: 'Are we appending to an existing list or starting a brand new book?' (Prioritize appending to avoid reorganizing 300+ physical discs).
* **Genre Header:** Ask for the Genre immediately (e.g., Sci-Fi, Horror, Animation).
* **Current State:** Extract the 'Current Occupied Slots' from provided data/files.
* **Visual ID:** Photos of box sets, UPCs, and disc artwork are acceptable identifiers.

### 2. Async Processing (Categories)
* **Category A (Verified):** Clear metadata and disc counts from search or artwork.
* **Category B (Pending):** Ambiguous editions or titles where multiple versions exist.
* **Workflow:** Verify Category A immediately. List Category B items for my clarification. Do not generate code until all items are cleared into Category A.

### 3. The Verification Pause
Before generating code, summarize:
* **New Titles Added:** [List]
* **Total New Discs:** [Count]
* **Final Occupied Slots:** [Current + New]
* **Remaining Balance:** [336 - Final Total]
* **Ask:** 'Metadata and math are verified. Should I generate the .md, .html, and .txt code blocks now?'

### 4. Technical & Formatting Standards
* **Header:** Every document must start with '# {{Genre}} Table of Contents'.
* **Alphabetization:** Sort the entire list alphabetically, **ignoring 'The'** in titles.
* **Visual Logic:** Series Title appears ONLY on the first row of a season. Leave the column blank for subsequent discs.
* **Disc Numbering:** 'Disc x of y' format.

#### HTML/CSS Requirements:
* Framework: Bootstrap 5.3 CDN.
* CSS: table-layout: fixed; width: 100%;
* Column Widths: Series Title (22%), Disc # (18%), Episode Titles (60%).
* Print CSS: Include @media print { thead { display: table-header-group; } tr { page-break-inside: avoid; } @page { size: letter; margin: 0.5in; } }.

-------------------------------------------------------------------------------
PART 3: SAMPLE HTML TEMPLATE
-------------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{Genre}} Table of Contents</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body { font-family: sans-serif; padding: 20px; }
        h1 { text-align: center; margin-bottom: 30px; text-transform: uppercase; border-bottom: 2px solid #333; padding-bottom: 10px; }
        
        /* Fixed Layout Engine */
        table { table-layout: fixed; width: 100%; border-collapse: collapse; }
        
        /* Explicit Column Widths (22/18/60) */
        th:nth-child(1), td:nth-child(1) { width: 22%; } /* Series Title */
        th:nth-child(2), td:nth-child(2) { width: 18%; } /* Disc # */
        th:nth-child(3), td:nth-child(3) { width: 60%; } /* Episode Titles */

        .table thead th { background-color: #f8f9fa; vertical-align: middle; }
        
        /* Print Protocol */
        @media print {
            @page { size: letter; margin: 0.5in; }
            body { padding: 0; }
            thead { display: table-header-group; } /* Repeats header on new pages */
            tr { page-break-inside: avoid; } /* Prevents row splitting */
        }
    </style>
</head>
<body>

    <h1>{{Genre}} Table of Contents</h1>

    <table class="table table-bordered">
        <thead>
            <tr>
                <th>Series Title (Season #)</th>
                <th>Disc #</th>
                <th>Episode Titles</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td><strong>The Expanse (Season 1)</strong></td>
                <td>Disc 1 of 3</td>
                <td>Dulcinea, The Big Empty, Remember the Cant, QCB</td>
            </tr>
            <tr>
                <td></td>
                <td>Disc 2 of 3</td>
                <td>Back to the Butcher, Rock Bottom, Windmills</td>
            </tr>
            <tr>
                <td></td>
                <td>Disc 3 of 3</td>
                <td>Salvage, Critical Mass, Leviathan Wakes</td>
            </tr>
        </tbody>
    </table>

    <div class="mt-4 p-3 bg-light border border-dark">
        <p class="mb-1"><strong>Total Slots Occupied:</strong> 3</p>
        <p class="mb-0"><strong>Remaining Slots:</strong> 333</p>
    </div>

</body>
</html>
-------------------------------------------------------------------------------
