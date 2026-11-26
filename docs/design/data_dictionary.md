# Data Dictionary – Rwanda Crop Production Dataset

This data dictionary describes the tables designed from the Rwanda Seasonal Agricultural Survey 2024, Season C dataset. The design separates repeated information into related tables to reduce duplication and support normalization.

## 1. PROVINCE

Stores Rwanda's provinces.

| Column | Meaning | Key | Required | Unique |
|---|---|---|---|---|
| province_code | Province identification code | PK | Yes | Yes |
| province_name | Province name | — | Yes | Yes |

## 2. DISTRICT

Stores districts and the provinces they belong to.

| Column | Meaning | Key | Required | Unique |
|---|---|---|---|---|
| district_code | District identification code | PK | Yes | Yes |
| province_code | Province the district belongs to | FK | Yes | No |
| district_name | District name | — | Yes | Yes |

## 3. SURVEY_SEGMENT

Stores survey segment locations and classifications.

| Column | Meaning | Key | Required | Unique |
|---|---|---|---|---|
| segment_id | Survey segment identifier | PK | Yes | Yes |
| district_code | District where the segment is located | FK | Yes | No |
| stratum_code | Survey area classification | — | Yes | No |
| survey_segment_number | Segment number within the survey | — | Yes | No |

## 4. CROP_RECORD

Stores the main farmer, plot, crop and production information for each original survey record.

| Column | Meaning | Key | Required | Unique |
|---|---|---|---|---|
| record_id | Original dataset row identifier | PK | Yes | Yes |
| segment_id | Survey segment linked to the record | FK | Yes | No |
| farmer_identifier | Farmer identification number | — | Yes | No |
| farmer_type | Type of farmer | — | Yes | No |
| farmer_gender | Farmer's gender code | — | No | No |
| farmer_age | Farmer's age | — | No | No |
| farmer_responded | Indicates whether the farmer answered personally | — | No | No |
| respondent_relationship | Relationship of respondent to farmer | — | No | No |
| other_relationship | Other respondent relationship description | — | No | No |
| plot_number | Plot identification number | — | Yes | No |
| plot_size_sqm | Plot size in square metres | — | No | No |
| main_crop_count | Number of main crops on the plot | — | No | No |
| crop_code | Crop identification code | — | Yes | No |
| other_crop_name | Description when another crop is specified | — | No | No |
| perennial_plant_count | Number of perennial plants on the plot | — | No | No |
| perennial_plants_to_harvest | Number of perennial plants to be harvested | — | No | No |
| crop_proportion_percent | Proportion of the main crop in the plot | — | No | No |
| crop_proportion_code | Crop proportion classification code | — | No | No |
| crop_density_percent | Crop density percentage | — | No | No |
| crop_density_code | Crop density classification code | — | No | No |
| planting_period_code | Planting period code | — | No | No |
| harvesting_period_code | Harvesting period code | — | No | No |
| improved_seed_used | Indicates whether improved seed was used | — | No | No |
| improved_seed_source | Source of improved seed | — | No | No |
| other_seed_source | Description of another seed source | — | No | No |
| seed_type_code | Seed type reported by the farmer | — | No | No |
| seed_for_current_season | Indicates whether seed was for the current season | — | No | No |
| already_harvested_kg | Quantity already harvested in kilograms | — | No | No |
| remaining_to_harvest_kg | Quantity remaining to be harvested in kilograms | — | No | No |
| total_season_harvest_kg | Total harvest quantity for the season in kilograms | — | No | No |
| production_change_status | Comparison of production with the previous year | — | No | No |
| total_produced_kg | Total quantity produced or expected in kilograms | — | No | No |
| selling_place | Place where the crop is sold | — | No | No |
| other_selling_place | Description of another selling place | — | No | No |
| selling_price_per_kg | Selling price per kilogram in Rwandan francs | — | No | No |
| total_damaged_harvest_kg | Total damaged harvest or estimated loss in kilograms | — | No | No |
| harvested_area | Area harvested | — | No | No |
| crop_yield | Crop yield at plot level | — | No | No |
| post_harvest_measure | Dataset's post-harvest summary measure | — | No | No |
| production_harvesting_loss | Dataset's production and harvesting loss measure | — | No | No |
| plot_weight | Survey plot weight | — | No | No |
| analysis_weight | Survey analysis weight | — | No | No |
| crop_category_code | General crop category code | — | No | No |
| disease_details | Description of reported crop disease or pests | — | No | No |

## 5. SEED_USE

Stores seed information as separate records for traditional and improved seeds.

| Column | Meaning | Key | Required | Unique |
|---|---|---|---|---|
| seed_use_id | Seed-use record identifier | PK | Yes | Yes |
| record_id | Crop record linked to the seed information | FK | Yes | No |
| seed_type | Traditional or improved seed | — | Yes | No |
| seed_unit | Unit used to measure the seed | — | No | No |
| quantity_sown | Quantity of seed sown | — | No | No |
| quantity_purchased | Quantity of seed purchased or reported as purchased/sown | — | No | No |
| seed_cost_rwf | Cost of the seed in Rwandan francs | — | No | No |

Each crop record can have up to two seed-use records: one for traditional seed and one for improved seed.

## 6. HARVEST_ALLOCATION

Stores how the harvested crop is used or distributed. Each type of use is stored as a separate record.

| Column | Meaning | Key | Required | Unique |
|---|---|---|---|---|
| allocation_id | Harvest allocation identifier | PK | Yes | Yes |
| record_id | Crop record linked to the allocation | FK | Yes | No |
| allocation_type | Purpose for which the harvest is used | — | Yes | No |
| quantity_kg | Quantity allocated in kilograms | — | No | No |
| allocation_ratio | Proportion allocated to this purpose | — | No | No |

Allocation types include transformed, sold, own consumption, wages, farm rent, gifts, exchanged products, seeds, fodder, stock and other uses.

## 7. LOSS_STAGE

Stores crop losses according to the stage or cause of loss.

| Column | Meaning | Key | Required | Unique |
|---|---|---|---|---|
| loss_id | Loss record identifier | PK | Yes | Yes |
| record_id | Crop record linked to the loss | FK | Yes | No |
| loss_type | Stage or cause of crop loss | — | Yes | No |
| quantity_kg | Quantity lost in kilograms | — | No | No |
| loss_ratio | Proportion of crop lost at that stage | — | No | No |

Loss types include theft, insects and pests, birds and animals, fallen stalks, harvesting, transport, storage, processing, packaging and sales.

## 8. PRODUCTION_REASON

Stores the reasons given for changes in crop production.

| Column | Meaning | Key | Required | Unique |
|---|---|---|---|---|
| reason_id | Production reason record identifier | PK | Yes | Yes |
| record_id | Crop record linked to the reason | FK | Yes | No |
| reason_position | Position of the reason in the original survey | — | Yes | No |
| reason_code | Code describing the production change reason | — | Yes | No |
| other_reason_details | Other reason description, where provided | — | No | No |

A crop record can have up to three production reasons. The position preserves the order in which they were recorded.

## 9. STORAGE

Stores information about the facility used to store harvested crops.

| Column | Meaning | Key | Required | Unique |
|---|---|---|---|---|
| storage_id | Storage record identifier | PK | Yes | Yes |
| record_id | Crop record linked to the storage information | FK | Yes | No |
| facility_type | Type of storage facility used | — | No | No |
| other_facility | Description of another storage facility | — | No | No |
| public_storage_quantity_kg | Quantity stored in public storage in kilograms | — | No | No |

## Relationships

- One province can have many districts.
- One district can have many survey segments.
- One survey segment can have many crop records.
- One crop record can have many seed-use records.
- One crop record can have many harvest-allocation records.
- One crop record can have many loss-stage records.
- One crop record can have many production-reason records.
- One crop record can have one storage record.

**Note:** PK means Primary Key and FK means Foreign Key. Required and unique constraints describe the intended database design. Optional source values may remain empty when the survey did not collect an answer. Oracle data types and sizes will be decided during physical database design.