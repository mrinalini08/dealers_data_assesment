# Data Engineering Code Interview

## 👋 Hi there

Welcome to the Data Engineering code interview! This small data challenge is designed to test out your skills in python, sql, git and basical data visualization.

## What we are looking for

Your code interview will be evaluated based on your repo, so make sure all files you have are stored in your repo. Specifically we are looking at:

- **Project scafolding**: How you name, manage, and organize your files.

- **Reproducibility**:
  - Ideally if it runs on your machine, it would also run on mine.
  - Make sure you document any software dependency, and installation process.
  - Clear and informative commit messages

- **Code**:
  - Clean, formated and readable
  - DRY (Don't Repeat Yourself)

- **Documentation**:
  - A comprehensive `README.md` on anything that we should know about this repo.
  - Clear instructions on commands to run code and what to expect (we love clis).
  - Clear documentation for functions/processes in code.

## Introduction

At Rodo, we have close relations with major car dealers across the country and we maintain a database of car inventories for online listings. For 4 times a day we receive **dealer feeds** from feed providers that contains detailed information about car availabilities at each dealership (you can find them under the `feeds` folder). Each feed provider has consistent data schema for each associated dealerships.
> Example: in the `feeds` folder, you can find two feed providers (**bram** and **silverstar**). Under the `feeds/bram@honcker.com` you can find two feed files for dealership **jenkinskiaocala** and **waynemazda**. The sample feed files you see have maximum 50 records each, in reality, we have way more records available.

## Task 1

Your task will be to build a feed ingestion framework that standardizes raw feed files and load them into a database. While developing, please keep in mind that we have around 50 different feed providers and more than 1000 dealerships, so designing something reusable, extendable and generalizable is important.

### Expected output

You have several options:

1. if you are using postgres, please provide a pgdump of the `dealer_data` table in the `output` folder
2. if you are using sqlite, please provide the database file in the `output` folder
3. if you have trouble working with a database. provide all records in json format (make sure your json schema corresponds to the database schema)

### Target Schema

```sql
CREATE TABLE dealer_data (
    hash text PRIMARY KEY,
    dealership_id text NOT NULL,
    vin text NOT NULL,
    mileage integer,
    is_new boolean,
    stock_number text,
    dealer_year integer,
    dealer_make text,
    dealer_model text,
    dealer_trim text,
    dealer_model_number text,
    dealer_msrp integer,
    dealer_invoice integer,
    dealer_body text,
    dealer_inventory_entry_date date,
    dealer_exterior_color_description text,
    dealer_interior_color_description text,
    dealer_exterior_color_code text,
    dealer_interior_color_code text,
    dealer_transmission_name text,
    dealer_installed_option_codes text[],
    dealer_installed_option_descriptions text[],
    dealer_additional_specs text,
    dealer_doors text,
    dealer_drive_type text,
    updated_at timestamp with time zone NOT NULL DEFAULT now(),
    dealer_images text[],
    dealer_certified boolean
);
```

### Schema Mapping

#### `silverstar@honcker.com` Files

<google-sheets-html-origin><style type="text/css"><!--td {border: 1px solid #ccc;}br {mso-data-placement:same-cell;}--></style>
Target | Source | Info
-- | -- | --
dealership_id | DealerId |  
vin | VIN |  
mileage | Mileage |  
is_new | New/Used | "N" = new = True
stock_number | Stock # |  
dealer_year | Year |  
dealer_make | Make |  
dealer_model | Model |  
dealer_trim | Trim |  
dealer_model_number | Model Code |  
dealer_msrp | MSRP | MSRP if new else List Price
dealer_invoice | Invoice | Invoice if new else List Price
dealer_body | N/A | leave as NULL
dealer_inventory_entry_date | Inventory Date |  
dealer_exterior_color_description | Exterior Color |  
dealer_interior_color_description text, | Interior Color |  
dealer_exterior_color_code | Exterior Color Code |  
dealer_interior_color_code | Interior Color Code |  
dealer_transmission_name | Transmission |  
dealer_transmission_type | N/A | leave as NULL
dealer_installed_option_codes | Option Codes |  
dealer_installed_option_descriptions | Options |  
dealer_additional_specs | N/A | leave as NULL
dealer_doors | N/A | leave as NULL
dealer_drive_type | N/A | leave as NULL
dealer_images | Photos | "\|" delimited
dealer_certified | Certified | "Yes" = True

#### `bram@honcker.com` Files

<google-sheets-html-origin><style type="text/css"><!--td {border: 1px solid #ccc;}br {mso-data-placement:same-cell;}--></style>

Target | Source | Info
-- | -- | --
dealership_id | Dealer ID |  
vin | VIN |  
mileage | Miles |  
is_new | New/Used | "New" = True,  "Used" = False
stock_number | Stock # |  
dealer_year | Year |  
dealer_make | Make |  
dealer_model | Model |  
dealer_trim | Trim |  
dealer_model_number | ModelNumber |  
dealer_msrp | MSRP | MSRP if new else List Price
dealer_invoice | Invoice | Invoice if new else List Price
dealer_body | Body |  
dealer_inventory_entry_date | DateInStock |  
dealer_exterior_color_description | ExteriorColor |  
dealer_interior_color_description | InteriorColor |  
dealer_exterior_color_code | ExteriorColorCode |  
dealer_interior_color_code | InteriorColorCode |  
dealer_transmission_name | Transmission |  
dealer_transmission_type | N/A | leave as NULL
dealer_installed_option_codes | OptionCode |  
dealer_installed_option_descriptions | OptionDescription |  
dealer_additional_specs | AdditionalSpecs |  
dealer_doors | N/A | leave as NULL
dealer_drive_type | Drivetrain |  
dealer_images | ImageList | "," delimited
dealer_certified | Certified | "Yes" = True

#### Notes

1. the `hash` field is use to detect if a car has any information change in the feed files. so please implement it in a way that would serve this purpose.

2. we would highly recommend using the python `typing` library or `pydantic` for data modeling to ensure data quality. If any records has exceptions, e.g. missing data for not null fields, please log the record into a seperate file or table along with reasons. Also please document anything that looks suspicious.

3. The target schema query is provided in postgres format. If you don't have access to a postgres database, you can use `sqlite`

4. It's your call to use or not use a ORM, either way please document your thoughts and reasonings.

## Task 2

Plot a line plot to show number of cars at each dealership through out time. the X axis will be year-month and the Y axis will be the number of cars at each dealership given year and month.

### Expected output

a `.png` file of the plot in the `output` folder. Please have clear title/legend/axis descriptions.

## Task 3 (Bonus)

Write a image downloader that would take a dealer image url and download to a local path (`images`). If you are able to acomplish this task, make sure in the `dealer_images` field, it's reflecting an array of local image file paths instead of urls.

### Expected output

You don't have to commit the images to your repo. Just the code is enough.
