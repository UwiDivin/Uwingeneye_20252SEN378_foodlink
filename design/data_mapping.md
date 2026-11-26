# Data Mapping – Rwanda Crop Production Dataset

This document shows where each of the 102 original dataset fields is stored in the normalized FoodLink research database design. Fields are either transferred directly, reorganized into related tables, or converted into separate records.

## 1. Location and survey information

| Original field | Target table | Target column |
|---|---|---|
| id | CROP_RECORD | record_id |
| segment_id | SURVEY_SEGMENT | segment_id |
| s1q1 | PROVINCE | province_code |
| s1q2 | DISTRICT | district_code |
| s1q3 | SURVEY_SEGMENT | stratum_code |
| s1q4 | SURVEY_SEGMENT | survey_segment_number |

Province and district names are obtained from the dataset metadata because the raw CSV contains their codes.

## 2. Farmer information

| Original field | Target table | Target column |
|---|---|---|
| s1q6 | CROP_RECORD | farmer_identifier |
| s1q7 | CROP_RECORD | farmer_type |
| s1q8 | CROP_RECORD | farmer_gender |
| s1q9 | CROP_RECORD | farmer_age |
| s1q14 | CROP_RECORD | farmer_responded |
| s1q17 | CROP_RECORD | respondent_relationship |
| s1q17_o | CROP_RECORD | other_relationship |

## 3. Plot and crop information

| Original field | Target table | Target column |
|---|---|---|
| s2q1 | CROP_RECORD | plot_number |
| s2q2 | CROP_RECORD | plot_size_sqm |
| s2q3 | CROP_RECORD | main_crop_count |
| s2q4 | CROP_RECORD | crop_code |
| s2q4_o | CROP_RECORD | other_crop_name |
| s2q5 | CROP_RECORD | perennial_plant_count |
| s2q6 | CROP_RECORD | perennial_plants_to_harvest |
| s3q2_1 | CROP_RECORD | crop_proportion_percent |
| s3q2_2 | CROP_RECORD | crop_proportion_code |
| s3q3_1 | CROP_RECORD | crop_density_percent |
| s3q3_2 | CROP_RECORD | crop_density_code |
| s2q7 | CROP_RECORD | planting_period_code |
| s2q8 | CROP_RECORD | harvesting_period_code |

## 4. Seed information

General seed information remains in CROP_RECORD. Individual seed measurements are moved into SEED_USE.

| Original field | Target table | Target column |
|---|---|---|
| s2q9 | CROP_RECORD | improved_seed_used |
| s2q10 | CROP_RECORD | improved_seed_source |
| s2q10_o | CROP_RECORD | other_seed_source |
| s2q11 | CROP_RECORD | seed_type_code |
| s2q12 | CROP_RECORD | seed_for_current_season |
| s2q13_1 | SEED_USE | seed_unit (traditional seed) |
| s2q13_2 | SEED_USE | quantity_sown (traditional seed) |
| s2q14 | SEED_USE | quantity_purchased (traditional seed) |
| s2q15 | SEED_USE | seed_cost_rwf (traditional seed) |
| s2q16_1 | SEED_USE | seed_unit (improved seed) |
| s2q16_2 | SEED_USE | quantity_sown (improved seed) |
| s2q17 | SEED_USE | quantity_purchased (improved seed) |
| s2q18 | SEED_USE | seed_cost_rwf (improved seed) |

The seed type in SEED_USE distinguishes traditional seed from improved seed.

## 5. Harvest and production information

| Original field | Target table | Target column |
|---|---|---|
| s2q19_1 | CROP_RECORD | harvested_quantity_unit |
| s2q19_3 | CROP_RECORD | already_harvested_quantity |
| s2q20_2 | CROP_RECORD | remaining_to_harvest_kg |
| s2q21 | CROP_RECORD | total_season_harvest_kg |
| s2q22_status | CROP_RECORD | production_change_status |
| s2q23 | CROP_RECORD | total_produced_kg |
| harvested_area | CROP_RECORD | harvested_area |
| yield | CROP_RECORD | crop_yield |

## 6. Production reasons

Each reported reason becomes a separate row in PRODUCTION_REASON. The reason position preserves its original order.

| Original field | Target table | Target column |
|---|---|---|
| s2q22_1 | PRODUCTION_REASON | reason_code (position 1) |
| s2q22_2 | PRODUCTION_REASON | reason_code (position 2) |
| s2q22_3 | PRODUCTION_REASON | reason_code (position 3) |
| s2q22_3_o | PRODUCTION_REASON | other_reason_details |
| s2q22_disease | CROP_RECORD | disease_details |

## 7. Harvest allocation information

Each type of harvest use becomes a separate row in HARVEST_ALLOCATION.

| Original field | Target table | Target column |
|---|---|---|
| s2q24 | HARVEST_ALLOCATION | quantity_kg (transformed) |
| s2q25 | HARVEST_ALLOCATION | quantity_kg (sold) |
| s2q26 | CROP_RECORD | selling_place |
| s2q26_o | CROP_RECORD | other_selling_place |
| s2q27 | CROP_RECORD | selling_price_per_kg |
| s2q28 | HARVEST_ALLOCATION | quantity_kg (own consumption) |
| s2q29 | HARVEST_ALLOCATION | quantity_kg (wages) |
| s2q30 | HARVEST_ALLOCATION | quantity_kg (farm rent) |
| s2q31 | HARVEST_ALLOCATION | quantity_kg (gifts) |
| s2q32 | HARVEST_ALLOCATION | quantity_kg (exchanged products) |
| s2q33 | HARVEST_ALLOCATION | quantity_kg (seeds) |
| s2q34 | HARVEST_ALLOCATION | quantity_kg (fodder) |
| s2q35 | HARVEST_ALLOCATION | quantity_kg (stock) |
| s2q39 | HARVEST_ALLOCATION | quantity_kg (other uses) |

The allocation type identifies the purpose of each quantity.

## 8. Storage information

| Original field | Target table | Target column |
|---|---|---|
| s2q36 | STORAGE | facility_type |
| s2q36_o | STORAGE | other_facility |
| s2q37 | STORAGE | public_storage_quantity_kg |

## 9. Crop loss information

Each loss cause or stage becomes a separate row in LOSS_STAGE.

| Original field | Target table | Target column |
|---|---|---|
| s2q38 | LOSS_STAGE | quantity_kg (total damaged harvest) |
| s2q40 | LOSS_STAGE | quantity_kg (theft) |
| s2q41 | LOSS_STAGE | quantity_kg (insects and pests) |
| s2q42 | LOSS_STAGE | quantity_kg (birds and animals) |
| s2q43 | LOSS_STAGE | quantity_kg (fallen stalks) |
| s2q44 | LOSS_STAGE | quantity_kg (harvesting) |
| s2q45 | LOSS_STAGE | quantity_kg (transport) |
| s2q46 | LOSS_STAGE | quantity_kg (storage) |
| s2q47 | LOSS_STAGE | quantity_kg (processing) |
| s2q48 | LOSS_STAGE | quantity_kg (packaging) |
| s2q49 | LOSS_STAGE | quantity_kg (sales) |

## 10. Ratios and survey measures

| Original field | Target table | Target column |
|---|---|---|
| sold_ratio | HARVEST_ALLOCATION | allocation_ratio (sold) |
| consum_ratio | HARVEST_ALLOCATION | allocation_ratio (own consumption) |
| wage_ratio | HARVEST_ALLOCATION | allocation_ratio (wages) |
| rent_ratio | HARVEST_ALLOCATION | allocation_ratio (farm rent) |
| gift_ratio | HARVEST_ALLOCATION | allocation_ratio (gifts) |
| exchanged_ratio | HARVEST_ALLOCATION | allocation_ratio (exchanged products) |
| seed_ratio | HARVEST_ALLOCATION | allocation_ratio (seeds) |
| feed_ratio | HARVEST_ALLOCATION | allocation_ratio (fodder) |
| stock_ratio | HARVEST_ALLOCATION | allocation_ratio (stock) |
| lost_ratio | LOSS_STAGE | loss_ratio (overall loss) |
| other_ratio | HARVEST_ALLOCATION | allocation_ratio (other uses) |
| post_harvest | CROP_RECORD | post_harvest_measure |
| production_harvestinglos | CROP_RECORD | production_harvesting_loss |
| harvesting_ratio | LOSS_STAGE | loss_ratio (harvesting) |
| transport_ratio | LOSS_STAGE | loss_ratio (transport) |
| storage_ratio | LOSS_STAGE | loss_ratio (storage) |
| processing_ratio | LOSS_STAGE | loss_ratio (processing) |
| packaging_ratio | LOSS_STAGE | loss_ratio (packaging) |
| sales_ratio | LOSS_STAGE | loss_ratio (sales) |
| weight_plot | CROP_RECORD | plot_weight |
| aweight | CROP_RECORD | analysis_weight |
| cropcategory | CROP_RECORD | crop_category_code |

## 11. Data transformations

The following changes are made when transferring the original fields:

1. The original `id` becomes `record_id` and remains the primary key of CROP_RECORD.
2. Location codes are separated into PROVINCE, DISTRICT and SURVEY_SEGMENT instead of being repeated in every crop record.
3. Seed measurements are converted into separate SEED_USE records for traditional and improved seeds.
4. Harvest quantities and their ratios are organized by allocation type in HARVEST_ALLOCATION.
5. Crop losses are organized by cause or stage in LOSS_STAGE.
6. Production reasons are converted into separate PRODUCTION_REASON records, preserving their original order.
7. Original survey codes are retained as codes rather than replaced with invented descriptions.
8. Province and district names are added from the dataset metadata.
9. Original measurement units are retained. Quantities are not converted to kilograms unless the source field is already measured in kilograms.

## 12. Fields not transferred

No original dataset field is intentionally discarded in this mapping. All 102 fields are assigned to a target table or column. Some fields are reorganized into multiple related records rather than kept as separate columns.
