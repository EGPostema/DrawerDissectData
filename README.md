# DrawerDissect Tiger Beetle Data & Analyses

This dataset includes all transcriptions, IDs, and measurements extracted from the Field Museum's entire >13K collection of pinned tiger beetles (Cicindelidae) using [DrawerDissect](https://github.com/EGPostema/DrawerDissect/tree/main).

## Manuscript

Postema, E.G., Briscoe, L., Harder, C., Hancock, G.R.A., Guarnieri, L.D, Eisel, T., Welch, K., Fisher, N., Johnson, C., Souza, D., Sepulveda, T., Phillip, D., Baquiran, R., de Medeiros, B.A.S. 2025. DrawerDissect: Whole-drawer insect imaging, segmentation, and trait extraction using AI. EcoEvoRxiv (pre-print). https://doi.org/10.32942/X2QW84

## Files Included

### R Scripts

-   **`size_validation.Rmd`** - Analysis comparing manual vs. digital measurements and generating genus-level size summaries.

-   **`specimen_ranges.Rmd`** - Visualizing the geographic distribution of tiger beetle specimens in the FMNH collection.

### Data CSVs

-   **`handmeasure.csv`** - Manual measurements for a random subset
-   **`spec_expanded.csv`** - Fully merged specimen-level dataset for the FMNH tiger beetle collection
-   **`llm_validation.csv`** - Includes all raw LLM transcriptions and revised locations for specimen-level metadata, plus reviewer commentary on estimate quality

## Variables

### handmeasure.csv

-   `drawer_id`: unique ID for each drawer based on position in collection cabinets
-   `unit_barcode`: 5-digit unique identifier for each tray
-   `spec_position`: specimen position in a tray, automatically numbered by DrawerDissect (001 = top left)
-   `manual_length_mm`: head-to-tip of abdomen measurement, taken manually, in mm
-   `manual_width_mm`: widest part of the abdomen, taken manually, in mm

### spec_expanded.csv

-   `full_id`: specimen ID produced by DrawerDissect; concatenation of drawer_id, tray_id, and specimen position
-   `FMNH-INS#`: unique Field Museum-specific ID, associated with a QR code
-   `drawer_id`: same as above
-   `tray_id`: tray ID produced by DrawerDissect
-   `unit_barcode`: same as above
-   `full_taxonomy`: unstructured taxonomic identity as a full string, e.g. "Species genus subspecies"
-   `genus`
-   `len1_mm`: longest line (in mm) between two points on the specimen mask, measured by DrawerDissect
-   `len2_mm`: longest line perpendicular to len1_mm, measured by DrawerDissect
-   `spec_area_mm2`: area of the specimen mask, measured by DrawerDissect
-   `geocode`:
-   `geocode`: 3-digit code for the biogeographical realm of all specimens in the tray (NEA = Nearctic, NEO = Neotropical, PAL = Palearctic, ORI = Oriental, AFR = Afrotropical, AUS = Australasian, PAC = Pacific)
-   `country`
-   `province_state`: also includes prefectures, districts, and similar geographic units
-   `county`
-   `city`
-   `prec_location`: specific natural or manmade features, islands, precise localities, and geographic units that don't fit in other categories
-   `elevation_fr`: collection elevation (start of range)
-   `elevation_to`: collection elevation (end of range)
-   `elevation_fr_ft`: same as above, in ft
-   `elevation_to_ft`: same as above, in ft
-   `site_num`: for campsites, base camps, and other numbered sites
-   `latitude`: in decimal degrees
-   `longitude`: in decimal degrees
-   `habitat`: broad habitat descriptions, e.g. "lakeshore" or "forest"
-   `microhabitat`: more specific habitat descriptions, e.g. "path in dense woods" or "abandoned flooded sand pit"
-   `collect_method:` e.g. light trap, net, pitfall trap
-   `date_from`: collection date (start of range)
-   `date_to`: collection date (end of range)
-   `collectors`: names of specimen collector(s)
-   `sex`: male (M) or female (F), if available
-   `lifestage`: adults only
-   `specimen`: whether the full_id image contains a specimen or not (Y/N)
-   `specimen_condition`: broken (some part is damaged), headless,
-   `mask_condition`: quality of the specimen mask produced by DrawerDissect
-   `notes`

### llm_validation

-   `full_id`: same as above
-   `geocode`: same as above
-   `verbatim`: raw text output by LLM claude in response to specimen dorsal views
-   `claude_location`: comma-seperated location estimate made by LLM based on the verbatim text, organized from largest to smallest geographic unit
-   `claude_assessment`: quality assessment determined by the LLM comapring the verbatim text to the estimate
-   `estimate_made`: whether or not the LLM makes a location estimate
-   `human_score`: whether the LLM's estimate is correct, incorrect, partially correct, or NA (no estimate made)
-   `endpoint`: concatenation of claude_assessment, estimate_made, and human_score

