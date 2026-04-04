# Building Regulations Atlas

A global interactive atlas of building regulatory environments, developed by the World Bank Group's Development Economics Global Indicators Group (DECIG). The atlas harmonizes data from four complementary datasets covering 152 economies, providing a unified view of building codes, energy efficiency standards, planning requirements, inspection processes, and transparency mechanisms.

**Live site:** [africa-building-regulations-atlas1.netlify.app](https://africa-building-regulations-atlas1.netlify.app/)

---

## Overview

The Building Regulations Atlas is a single-page web application that allows users to:

- **Explore a global map** of dataset coverage across 152 economies, filterable by data source
- **View country profiles** with key facts (population, urbanization, hazards) and detailed regulatory indicators
- **Filter indicators** by topic and subtopic (building design, compliance mechanisms, spatial planning, materials)
- **Export data** as CSV or Excel for further analysis

All data is embedded directly in the HTML file — no backend, no API calls, no database. The site is fully static and can be deployed to any hosting service.

## Data Sources

| Dataset | Coverage | Indicators | Description |
|---|---|---|---|
| **B-READY** (Business Ready) | 101 economies | 57 | World Bank assessment of regulatory frameworks and public services for firms, covering building permits, zoning, inspections, and transparency. |
| **Building Green** | 88 economies | 147 | Global dataset on building energy efficiency codes, HVAC/lighting standards, passive design requirements, enforcement mechanisms, and financial incentives. |
| **GFDRR SSA Study** | 48 economies | 80 | Building Regulation for Resilience study covering Sub-Saharan Africa — structural design, fire safety, accessibility, and building control. |
| **GFDRR Global Assessment** | 22 economies | 89 | Global Assessment of Building Codes covering structural resilience, fire safety, universal accessibility, and compliance mechanisms. |

**Additional data:** Population, urban population, and urban growth from [World Bank Open Data (2023)](https://data.worldbank.org/). Major hazards from [ThinkHazard](https://thinkhazard.org/).

## Regulatory Topics

The atlas organizes indicators into four main topics:

- **Spatial Planning** — land use maps, hazard maps, zoning plans, infrastructure requirements
- **Building Design** — general provisions, structural resilience, fire safety, green buildings, universal accessibility, MEP services
- **Materials** — hazardous materials regulation and disposal
- **Compliance Mechanisms** — building control, inspections, dispute resolution, transparency, professional registration

## Technical Architecture

### Front-end

- **Leaflet.js** — interactive map with circle markers colored by dataset coverage
- **Vanilla JavaScript** — no framework dependencies; country profiles rendered client-side from embedded data
- **SheetJS (xlsx)** — client-side Excel export

### Data Structure

Three JavaScript objects embedded in `index.html`:

- `COUNTRIES` — 152 economies with coordinates, region, income group, population, urbanization, hazards, and dataset coverage flags
- `INDICATORS` — 373 indicator definitions with topic/subtopic classification, source attribution, and detailed descriptions
- `DATA` — nested object mapping each economy's ISO code to its indicator values

### Supporting Data File

`Global_Building_Regulations_Atlas_Database.xlsx` contains four sheets that serve as the canonical data source:

| Sheet | Description |
|---|---|
| `data_long` | 17,718 rows — one row per country-indicator observation with full metadata |
| `indicator_catalog` | 373 indicators with unique IDs, topics, data types, and legend categories |
| `data_wide` | 152 × 373 pivot table — rows are economies, columns are indicator IDs |
| `countries` | 152 economies with coordinates, region, and dataset availability |

## Deployment

The atlas is a single `index.html` file (~600 KB). Deploy to any static host:

**Netlify:**
```bash
# Drag and drop the file, or:
netlify deploy --prod --dir .
```

**GitHub Pages:**
```bash
git add index.html
git commit -m "Update atlas data"
git push
```

No build step required.

## File Structure

```
├── index.html                                          # Complete atlas (single-file application)
├── Global_Building_Regulations_Atlas_Database.xlsx      # Source data workbook
├── Buildings_Regulations_Atlas_BREADY_items.xlsx        # B-READY indicator catalog
├── Building_Regulations_Atlas_Building_Green_Items.xlsx # Building Green indicator catalog
└── README.md
```

## Data Update Workflow

To update the atlas with new data:

1. Update the source Excel file (`Global_Building_Regulations_Atlas_Database.xlsx`)
2. Regenerate the `COUNTRIES`, `INDICATORS`, and `DATA` JavaScript objects from the `data_wide`, `indicator_catalog`, and `countries` sheets
3. Replace the corresponding variables in `index.html`
4. Deploy

## Credits

- **World Bank Group** — Development Economics Global Indicators Group (DECIG)
- **GFDRR** — Global Facility for Disaster Reduction and Recovery
- **B-READY** — Business Ready Initiative
- **Building Green** — Global Building Energy Efficiency Dataset

## License

Data is provided under the [World Bank Terms of Use](https://www.worldbank.org/en/about/legal/terms-of-use). The atlas code is available for non-commercial use.

---

*Building Regulations Atlas v3.0 (Global) · April 2026*
