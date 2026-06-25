# FASTA Sequence Tool

A browser-based tool for preparing and verifying DNA sequences for oligo ordering. Developed in the [Simon Lab](https://www.fredhutch.org) at Fred Hutchinson Cancer Center.

No installation required — open `index.html` in any modern browser or visit the hosted version at:
**[gracebugos.github.io/fasta-sequence-tool](https://gracebugos.github.io/fasta-sequence-tool)**

---

## Overview

This tool supports a two-step workflow for codon optimization and oligo ordering:

**Step 1 — Prep for codon optimization**
Takes protein FASTA files exported from SnapGene (or any standard FASTA source) and produces a formatted Excel file ready to upload to a codon optimization tool. One row per sequence, with columns for sequence name and protein sequence.

**Step 2 — Process codon optimization output**
Takes the FASTA files output by the codon optimization tool (one per subfolder) and:
- Merges all sequences into a single file
- Optionally reverse complements sequences for antisense oligo ordering
- Translates the sense strand (frame +1) and compares against the original protein from Step 1
- Flags missing start codons, missing stop codons, and sequence mismatches
- Exports a formatted Excel file with DNA sequences and translation verification

---

## Usage

### Step 1: Prep for codon optimization

1. Export each protein sequence from SnapGene as a `.fasta` file
2. Drop all files into the Step 1 upload zone
3. Review the preview table
4. Download `codon_opt_input.xlsx` and upload to your codon optimization tool

> The filename (before the extension) is used as the sequence name in the output.

### Step 2: Process codon optimization output

1. Complete Step 1 first so protein sequences are available for verification
2. Drop the FASTA output files from the codon optimization tool into the Step 2 upload zone
3. If the codon optimization tool appended a trailing `_number` to folder names, this is stripped automatically
4. Toggle **Reverse complement** if sequences need to be RC'd for oligo ordering
5. Select how to handle multiple FASTAs per folder (first, longest, or last alphabetically)
6. Click **Process sequences**
7. Review DNA sequences and translation verification, including any alerts
8. Download `sequences.xlsx` containing:
   - **DNA sequences tab** — sequence name and final DNA sequence
   - **Translation tab** — frame +1 translation, start/stop codon status, and match against Step 1 protein

---

## Translation verification

For each sequence, the tool checks the frame +1 translation of the sense strand (the codon optimization output, prior to any reverse complementation) and reports:

| Alert | Meaning |
|---|---|
| ✅ Translation matches Step 1 protein | Codon optimization and RC steps preserved the sequence |
| 🔴 Translation does not match Step 1 protein | Sequence mismatch — review before ordering |
| ⚠️ No start codon (M) | Sequence may be incomplete or truncated |
| ⚠️ No stop codon | Sequence may be missing a stop codon |

---

## File formats

| Format | Accepted in |
|---|---|
| `.fasta`, `.fa`, `.fna` | Step 1 (protein) and Step 2 (DNA) |
| `.ffn`, `.frn` | Step 2 (DNA) only |

---

## Notes

- All processing happens locally in the browser — no data is uploaded to any server
- Requires an internet connection on first load to fetch fonts and icons from CDN
- Excel export uses [SheetJS](https://sheetjs.com/)
- Tested in Chrome and Safari

---

## Development

Built as a single-file HTML/JS tool with no framework dependencies.

To update: edit `index.html` and push to the `main` branch. GitHub Pages will redeploy within ~60 seconds.

---

## Citation

If you use this tool in your research, please cite:

> Simon Lab, Fred Hutchinson Cancer Center. *FASTA Sequence Tool* (2025). https://gracebugos.github.io/fasta-sequence-tool

---

## Contact

Grace Bugos · [Fred Hutchinson Cancer Center](https://www.fredhutch.org)  
GitHub: [@GraceBugos](https://github.com/GraceBugos)
