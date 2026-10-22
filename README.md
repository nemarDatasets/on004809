[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.on004809-blue)](https://doi.org/10.82901/nemar.on004809)

### Categorized Free Recall: Delayed Free Recall of Word Lists Organized by Semantic Categories

#### Description
This dataset contains behavioral events and intracranial electrophysiological recordings from a categorized free recall task.  The experiment consists of participants studying a list of words, presented visually one at a time, completing simple arithmetic problems that function as a distractor, and then freely recalling the words from the just-presented list in any order.  The data was collected at clinical sites across the country as part of a collaboration with the Computational Memory Lab at the University of Pennsylvania.

Unique to this paradigm is the semantic construction of the word lists.  Each word comes from one of 25 semantic categories, and each list of 12 items contains 6 pairs of same-category words from 3 different categories.  This means that each list has 4 words from 3 semantic categories, and in each half of the list there will be 1 pair of words from each category.  For example, if a list contains words from categories A, B, and C, a possible list construction would be: 

**A1 - A2 - B1 - B2 - C1 - C2 - A3 - A4 - C3 - C4 - B3 - B4**

#### To Note
* The iEEG recordings are labeled either "monopolar" or "bipolar."  The monopolar recordings are referenced (typically a mastoid reference), but should always be re-referenced before analysis.  The bipolar recordings are referenced according to a paired scheme indicated by the accompanying bipolar channels tables.
* Each subject has a unique montage of electrode locations.  MNI and Talairach coordinates are provided when available, along with brain region annotations.
* Recordings were made on multiple different systems, so we have done the scaling to provide all voltage values in V.

#### Contact
For questions or inquiries, please contact sas-kahana-sysadmin@sas.upenn.edu.

## Channel names follow the data headers (18 Oct 2026)

In 11 recordings the channel list of channels.tsv did not equal the data-file header (names, order or count). In the 11 with a different channel count, `mne_bids.read_raw_bids` warned and kept the header names, so the channels.tsv types and bad-channel status reached only the channels whose names happen to be identical; a reader that applies the channels.tsv rows by position gives wrong labels wherever the two lists are not aligned. Since 18 Oct 2026 every channels.tsv lists exactly the header channels, in header order, with the header names (MNE names: duplicated header labels numbered -0, -1).

Rows were matched to header channels BY NAME, never by position (exact; then case/whitespace; then the recorder prefix 'EEG '/'POL ', '_' and zero padding; then a trailing '-<reference>' token). Matched rows keep all their columns (type, units, status, ...); 0 rows took the header name.

120 channels.tsv rows had no channel in the data file (11 files) and were removed; they are kept verbatim under `sourcedata/channels-removed-2026-10-18/` (same relative path). Examples: `sub-R1354E_ses-0_task-catFR1_acq-bipolar_ieeg.edf`: 5Ldm1-5Ldm2, 5Ldm2-5Ldm3, 5Ldm3-5Ldm4, 5Ldm4-5Ldm5, 5Ldm5-5Ldm6; `sub-R1354E_ses-1_task-catFR1_acq-bipolar_ieeg.edf`: 5Ldm1-5Ldm2, 5Ldm2-5Ldm3, 5Ldm3-5Ldm4, 5Ldm4-5Ldm5, 5Ldm5-5Ldm6; `sub-R1354E_ses-2_task-catFR1_acq-bipolar_ieeg.edf`: 5Ldm1-5Ldm2, 5Ldm2-5Ldm3, 5Ldm3-5Ldm4, 5Ldm4-5Ldm5, 5Ldm5-5Ldm6.

Applied by position, the former rows would have given wrong labels to 385 channels in 7 files (rows missing, extra or out of order before that position).

## Electrode locations (19 Oct 2026)

Sub-R1004D ses-0: MNI pair (outside the head) replaced by a space-Talairach pair. Evidence: sub-R1004D ses-0 MNI x/y/z lie outside any plausible head position; the same rows' tal.x/y/z are within the head and the deposit's *_electrodes.json defines them as "position in Talairach coordinates". New space-Talairach electrodes.tsv (x/y/z = tal.*) and coordsystem.json (the same content as the deposit's other space-Talairach coordsystem files, e.g. sub-R1016M); the MNI electrodes.tsv/coordsystem.json pair is removed so that readers choose the Talairach pair (EEGDash reads a named space before Other, then alphabetically, so MNI would otherwise win).

Source: the deposit's own files only (the `*_electrodes.json` column definitions and this deposit's other space-Talairach coordsystem files). No coordinate value was computed or inferred: x/y/z of the new pair are the deposit's tal.x/y/z values of the same rows. This dataset mirrors OpenNeuro; the same change belongs upstream.
