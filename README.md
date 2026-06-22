# DrawerDissect Tiger Beetle Data & Analyses

This dataset includes all transcriptions, IDs, and measurements extracted from the Field Museum's entire >13K collection of pinned tiger beetles (Cicindelidae) using [DrawerDissect](https://github.com/EGPostema/DrawerDissect/tree/main).

<img width="1033" height="738" alt="image" src="https://github.com/user-attachments/assets/0dddfb0a-1c22-4f76-a191-c54d9e623d55" />

## Manuscript

Postema, E.G., Briscoe, L., Harder, C., Hancock, G.R.A., Guarnieri, L.D, Eisel, T., Welch, K., Fisher, N., Johnson, C., Souza, D., Sepulveda, T., Phillip, D., Baquiran, R., de Medeiros, B.A.S. 2025. DrawerDissect: Whole-drawer insect imaging, segmentation, and trait extraction using AI. EcoEvoRxiv (pre-print). https://doi.org/10.32942/X2QW84

## Files Included

### R Scripts

- **`size_validation.Rmd`** - Analysis comparing manual vs. digital measurements and generating genus-level size summaries.

- **`transcription_evaluation.Rmd`** - Field-by-field comparison of LLM transcriptions against human-produced DarwinCore records, including similarity scoring, misplacement detection, date standardisation, and a map of geographic coverage.

### Data CSVs

- **`drawerdissect_sizes.csv`** - Specimen-level dataset including IDs, taxonomy, and measurements extracted by DrawerDissect.

- **`handmeasure.csv`** - Manual measurements for a random subset of specimens, used to validate DrawerDissect digital measurements.

- **`dwc_existing_records.csv`** - Human-produced DarwinCore records for tiger beetle specimens (from previous databasing efforts)

- **`claude_transcriptions.csv`** - Raw LLM transcriptions of specimen label text, produced from dorsal images.

- **`country_counts.csv`** - Pre-computed specimen counts per country, used to generate the geographic coverage map.

- **`tray01GT.csv`, `tray03GT.csv`, `34_4_7_tray_07GT.csv`, `34_6_8_tray_09GT.csv`, `34_7_5_tray_04GT.csv`** - Additional human-produced records for five trays not present in `dwc_existing_records.csv`.

## Variables

### drawerdissect_sizes.csv

- `full_id`: specimen ID produced by DrawerDissect; concatenation of drawer_id, tray_id, and specimen position
- `FMNH-INS#`: unique Field Museum-specific ID, associated with a QR code
- `drawer_id`: unique ID for each drawer based on position in collection cabinets
- `tray_id`: unit tray ID produced by DrawerDissect
- `unit_barcode`: 5-digit unique identifier for each tray
- `full_taxonomy`: unstructured taxonomic identity as a full string, e.g. "Species genus subspecies"
- `genus`
- `len1_mm`: longest line (in mm) between two points on the specimen mask, measured by DrawerDissect
- `len2_mm`: longest line perpendicular to len1_mm, measured by DrawerDissect
- `spec_area_mm2`: area of the specimen mask, measured by DrawerDissect

### handmeasure.csv

- `drawer_id`: unique ID for each drawer based on position in collection cabinets
- `unit_barcode`: 5-digit unique identifier for each tray
- `spec_position`: specimen position in a tray, automatically numbered by DrawerDissect (001 = top left)
- `manual_length_mm`: head-to-tip of abdomen measurement, taken manually, in mm
- `manual_width_mm`: widest part of the abdomen, taken manually, in mm

### dwc_existing_records.csv and additional tray-level csvs:

- `specimen_id`: unique specimen identifier
- `country`, `stateProvince`, `county`, `municipality`, `locality`: geographic fields from broadest to most specific
- `islandGroup`, `island`: island-specific geographic fields
- `verbatimElevation`: elevation as recorded on the label
- `habitat`: broad habitat description
- `samplingProtocol`: collection method
- `recordedBy`: collector name(s)
- `verbatimEventDate`: collection date as recorded on the label

### claude_transcriptions.csv

- `specimen_id`: unique specimen identifier
- `match_type`: whether label text was detected (`no_text_detected` indicates a blank or illegible label); if detected, whether the label is unique or similar to another label in the same tray
- `verbatimEventDate`: date as transcribed by the LLM
- `country`, `stateProvince`, `county`, `municipality`, `locality`, `islandGroup`, `island`, `verbatimElevation`, `habitat`, `samplingProtocol`, `recordedBy`: label fields transcribed by the LLM

### country_counts.csv

- `specimen_id`: unique specimen identifier
- `unique_countries`: country the specimen was collected from
- `specimen_count`: number of specimens from that country

