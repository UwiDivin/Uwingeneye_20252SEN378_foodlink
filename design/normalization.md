# Database Normalization – Rwanda Crop Production Dataset

## 1. Dataset overview

The dataset used for this project is the Rwanda Seasonal Agricultural Survey 2024, Season C – Crop Production dataset.

It contains 5,818 records and 102 columns. Each record represents crop production information collected for a farmer's plot.

The purpose of normalization is to organize the data into related tables, reduce unnecessary repetition and make the database easier to maintain.

## 2. Unnormalized Form (UNF)

In its original form, the dataset stores farmer details, location information, plot details, seed information, production reasons, harvest allocation and crop losses together in one wide table.

For example, one record can contain:

- Farmer and location details.
- Traditional and improved seed information in separate groups of columns.
- Up to three production reasons.
- Several harvest allocation quantities.
- Several crop loss measurements.

This structure makes the dataset wide and repeats information across records.

The following are three real records from the original CSV:

| id | segment_id | s1q2 (district) | s1q6 (farmer ID) | s2q1 (plot) | s2q4 (crop) | s2q21 (harvest kg) |
|---:|---:|---:|---:|---:|---:|---:|
| 1 | 112002 | 11 | 1 | 1 | 120 | 1500 |
| 2 | 112002 | 11 | 2 | 2 | 120 | 4032 |
| 3 | 112003 | 11 | 1 | 1 | 122 | 15 |

These records show that different crop records can share the same survey segment and district information.

## 3. First Normal Form (1NF)

To reach 1NF, each field must contain a single value, and each record must be uniquely identifiable.

The original dataset already has a unique `id` for each record. Its separate survey columns also hold individual values.

However, groups of columns represent repeated information, such as:

- Traditional and improved seed measurements.
- Up to three production reasons.
- Different harvest allocation purposes.
- Different crop loss stages.

These groups are reorganized into separate related records rather than being treated as one repeating group.

For example, the first three records retain their unique identifiers and individual crop information:

| record_id | segment_id | farmer_identifier | plot_number | crop_code | total_season_harvest_kg |
|---:|---:|---:|---:|---:|---:|
| 1 | 112002 | 1 | 1 | 120 | 1500 |
| 2 | 112002 | 2 | 2 | 120 | 4032 |
| 3 | 112003 | 1 | 1 | 122 | 15 |

**What changed:** Each crop record is kept as one identifiable row. Repeated seed, reason, allocation and loss information is prepared for storage in related tables.

## 4. Second Normal Form (2NF)

A table is in 2NF when it is already in 1NF and every non-key attribute depends on the whole primary key.

The original crop record uses a single-column primary key, `id`. Therefore, there are no partial dependencies on part of a composite primary key.

The repeated information is separated into child tables, each with its own primary key and a foreign key linking it to CROP_RECORD.

| New table | Information separated | Reason |
|---|---|---|
| SEED_USE | Traditional and improved seed measurements | Stores each seed type as a separate record |
| HARVEST_ALLOCATION | Different uses of harvested crops | Stores each allocation purpose separately |
| LOSS_STAGE | Different crop loss causes and stages | Stores each loss type separately |
| PRODUCTION_REASON | Up to three production reasons | Stores each reason as a separate record |
| STORAGE | Storage facility information | Separates storage details from the main crop record |

For example, the first original record contains traditional seed measurements. These values can be represented in SEED_USE as:

| seed_use_id | record_id | seed_type | seed_unit | quantity_sown |
|---:|---:|---|---:|---:|
| 1 | 1 | Traditional | 2 | 150 |

The original source value `s2q13_1 = 2` is retained as the seed unit code.

**What changed:** Repeated information is stored in separate tables and connected through `record_id`. This makes each table easier to manage.

## 5. Third Normal Form (3NF)

A table is in 3NF when it is in 2NF and non-key attributes do not depend on other non-key attributes.

The dataset contains location information that can be organized into a separate relationship:

- A district belongs to one province.
- A survey segment belongs to one district.
- A crop record belongs to one survey segment.

Instead of repeating province and district information in every crop record, the design separates it into three tables.

### PROVINCE

| province_code | province_name |
|---:|---|
| 1 | Kigali City |

### DISTRICT

| district_code | province_code | district_name |
|---:|---:|---|
| 11 | 1 | Nyarugenge |

### SURVEY_SEGMENT

| segment_id | district_code | stratum_code | survey_segment_number |
|---:|---:|---:|---:|
| 112002 | 11 | 20 | 2 |
| 112003 | 11 | 20 | 3 |

These values are taken from the original dataset and its metadata.

The CROP_RECORD table keeps `segment_id` as a foreign key instead of repeating province code, district code, stratum code and survey segment number.

**Dependency removed:** District information is stored in DISTRICT, where `district_code` identifies its province. Survey segment details are stored in SURVEY_SEGMENT, where `segment_id` identifies its district and survey details.

## 6. Final normalized tables

The resulting logical design contains nine related tables:

1. PROVINCE
2. DISTRICT
3. SURVEY_SEGMENT
4. CROP_RECORD
5. SEED_USE
6. HARVEST_ALLOCATION
7. LOSS_STAGE
8. PRODUCTION_REASON
9. STORAGE

The tables are connected using primary keys and foreign keys.

## 7. Data limitation

The source contains some farmer identifiers with conflicting farmer details within the same survey segment. For that reason, farmer information is kept in CROP_RECORD for now instead of creating a separate FARMER table.

This avoids making an unsupported assumption about farmer identity and prevents incorrect relationships.

## 8. Conclusion

Normalization organizes the original survey data into related tables. The design separates location information, seed use, harvest allocation, crop losses, production reasons and storage details.

This reduces repeated information and provides a clearer structure for implementing the database in Oracle.
