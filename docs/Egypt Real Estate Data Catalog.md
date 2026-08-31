# Egypt Real Estate Data Catalog

## Overview

This document describes the dataset used in the **Egypt Real Estate
Analytics** project.

The dataset contains real estate property listings collected from the
Egyptian real estate market. Each row represents one property listing
and contains information about:

-   Listing identification
-   Property characteristics
-   Pricing
-   Location
-   Listing attributes
-   Media
-   Amenities
-   Agent and broker information
-   Contact information
-   Listing and scraping dates

The dataset was prepared and cleaned in Python before being used for
analysis and Power BI.

------------------------------------------------------------------------

# Data Dictionary

## 1. Listing Identification

  ------------------------------------------------------------------------------------
  Column            Data Type         Description       Example
  ----------------- ----------------- ----------------- ------------------------------
  `listing_id`      string            Unique business   `F7QB31CGWE509V2W7DF2GARB2C`
                                      identifier for    
                                      the property      
                                      listing.          

  `internal_id`     string            Internal          `56009081`
                                      identifier        
                                      associated with   
                                      the listing in    
                                      the source        
                                      platform.         

  `category`        category          Main transaction  `buy`
                                      category of the   
                                      listing.          

  `listing_type`    category          Type of listing   `property`
                                      on the source     
                                      platform.         

  `detail_url`      string            URL of the        Property listing URL
                                      original property 
                                      listing.          

  `reference`       string            Reference code    `250pncash`
                                      associated with   
                                      the listing,      
                                      usually provided  
                                      by the            
                                      agent/broker.     

  `rera`            string            Regulatory or     `NULL`
                                      registration      
                                      reference, when   
                                      available.        
  ------------------------------------------------------------------------------------

> **Note:** Identifier columns are stored as strings because they are
> identifiers, not measures. They should not be summed or averaged.

------------------------------------------------------------------------

## 2. Property Information

  ------------------------------------------------------------------------------------------------------
  Column                Data Type         Description              Example
  --------------------- ----------------- ------------------------ -------------------------------------
  `property_type`       category          Type of property.        `Apartment`, `Villa`, `Duplex`

  `offering_type`       category          Type of real estate      `Residential for Sale`
                                          offering.                

  `completion_status`   category          Completion/development   `completed`, `off_plan`
                                          status of the property.  

  `title`               string            Title or headline of the `Garden Villa - Lake View Boutique`
                                          property listing.        

  `description`         string            Detailed description     Property description text
                                          provided in the listing. 

  `bedrooms`            Int64             Number of bedrooms in    `3`
                                          the property.            

  `bathrooms`           Int64             Number of bathrooms in   `6`
                                          the property.            

  `area_value`          float             Numeric property area.   `445`

  `area_unit`           category          Unit used to measure the `sqm`
                                          property area.           

  `furnished`           category          Furnishing status of the `PARTLY`
                                          property.                

  `listing_level`       category          Listing                  `premium`
                                          promotion/visibility     
                                          level on the platform.   
  ------------------------------------------------------------------------------------------------------

### Completion Status

The `completion_status` values are preserved as provided by the source:

-   `completed`
-   `completed_primary`
-   `off_plan`
-   `off_plan_primary`
-   `Not Specified`

The values were **not merged or reclassified**, because the project
keeps the original source distinctions.

------------------------------------------------------------------------

## 3. Pricing Information

  ---------------------------------------------------------------------------
  Column             Data Type         Description          Example
  ------------------ ----------------- -------------------- -----------------
  `price_egp`        float             Listed property      `24500000`
                                       price in Egyptian    
                                       Pounds.              

  `price_period`     category          Price                `sell`
                                       transaction/period   
                                       context.             

  `price_currency`   category          Currency of the      `EGP`
                                       listed price.        

  `payment_method`   category          Payment method       `cash`
                                       specified in the     
                                       listing.             
  ---------------------------------------------------------------------------

### Payment Method

Possible values include:

-   `cash`
-   `installments`
-   `cash \| installments`
-   `Not Specified`

------------------------------------------------------------------------

## 4. Location Information

The dataset stores the property location at multiple geographic levels.

  ----------------------------------------------------------------------------------------------------------
  Column            Data Type         Description        Example
  ----------------- ----------------- ------------------ ---------------------------------------------------
  `location_full`   string            Full location text `The Lakeview Boutique Villas, 5th Settlement...`
                                      as provided by the 
                                      source platform.   

  `city`            category          Main               `Cairo`
                                      city/governorate   
                                      classification.    

  `town`            category          City or town       `New Cairo City`
                                      within the main    
                                      geographic area.   

  `district`        category          Main district or   `The 5th Settlement`
                                      neighborhood.      

  `subdistrict`     category          More specific      `5th Settlement Compounds`
                                      location within    
                                      the district.      

  `lat`             float             Geographic         `30.04060173`
                                      latitude.          

  `lon`             float             Geographic         `31.52594185`
                                      longitude.         
  ----------------------------------------------------------------------------------------------------------

### Location Hierarchy

``` text
City
└── Town
    └── District
        └── Subdistrict
```

### Missing Location Values

Missing values in `district` and `subdistrict` were represented as:

``` text
Not Specified
```

This preserves the records while making the missing category explicit
for Power BI analysis.

------------------------------------------------------------------------

## 5. Listing Attributes and Flags

  -----------------------------------------------------------------------------
  Column                  Data Type         Description       Example
  ----------------------- ----------------- ----------------- -----------------
  `is_premium`            boolean           Indicates whether `TRUE`
                                            the listing has   
                                            premium status.   

  `is_verified`           boolean           Indicates whether `FALSE`
                                            the listing is    
                                            verified.         

  `is_featured`           boolean           Indicates whether `FALSE`
                                            the listing is    
                                            featured.         

  `is_new_construction`   boolean           Indicates whether `FALSE`
                                            the property is   
                                            classified as new 
                                            construction.     

  `is_direct_from_dev`    boolean           Indicates whether `FALSE`
                                            the listing is    
                                            directly from the 
                                            developer.        

  `is_exclusive`          boolean           Indicates whether `FALSE`
                                            the listing is    
                                            exclusive to an   
                                            agent or broker.  

  `agent_is_super`        boolean           Indicates whether `FALSE`
                                            the agent has a   
                                            super/elevated    
                                            status.           

  `has_view_360`          boolean           Indicates whether `FALSE`
                                            a 360-degree      
                                            property view is  
                                            available.        
  -----------------------------------------------------------------------------

------------------------------------------------------------------------

## 6. Listing Media

  -----------------------------------------------------------------------
  Column            Data Type         Description       Example
  ----------------- ----------------- ----------------- -----------------
  `images_count`    Int64             Number of images  `6`
                                      available for the 
                                      listing.          

  `has_view_360`    boolean           Indicates         `FALSE`
                                      availability of a 
                                      360-degree view.  

  `video_url`       string            URL of the        Video URL /
                                      property video,   `NULL`
                                      when available.   
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 7. Amenities

  -----------------------------------------------------------------------------------------------
  Column            Data Type         Description          Example
  ----------------- ----------------- -------------------- --------------------------------------
  `amenities`       string            List of property     `Balcony \| Security \| Shared Pool`
                                      amenities/features   
                                      separated by `|`.    

  -----------------------------------------------------------------------------------------------

A single listing can contain multiple amenities.

Example:

``` text
Balcony | Covered Parking | Private Garden | Private Pool | Security
```

For detailed amenity analysis, this field can later be normalized into a
separate table:

  listing_id   amenity
  ------------ -----------------
  F7QB...      Balcony
  F7QB...      Covered Parking
  F7QB...      Private Garden
  F7QB...      Private Pool

------------------------------------------------------------------------

## 8. Agent Information

  -----------------------------------------------------------------------------
  Column              Data Type         Description       Example
  ------------------- ----------------- ----------------- ---------------------
  `agent_id`          string            Unique identifier `58866`
                                        of the real       
                                        estate agent.     

  `agent_name`        string            Name of the agent `pierre osama`
                                        responsible for   
                                        the listing.      

  `agent_email`       string            Email address of  `agent@email.com`
                                        the agent.        

  `agent_is_super`    boolean           Indicates whether `FALSE`
                                        the agent has a   
                                        super/elevated    
                                        status.           

  `agent_languages`   string            Languages spoken  `English \| Arabic`
                                        by the agent.     
                                        Multiple values   
                                        may be separated  
                                        by `|`.           
  -----------------------------------------------------------------------------

### Agent Name Cleaning Rule

Where `agent_name` was missing, the project may derive a readable name
from the email username when appropriate.

Example:

``` text
m.rashead@ymail.com
→ M Rashead
```

If the email does not provide a reliable personal name, the value
remains:

``` text
Not Specified
```

------------------------------------------------------------------------

## 9. Broker Information

The broker generally represents the real estate company or brokerage
associated with the listing.

  ---------------------------------------------------------------------------
  Column            Data Type         Description       Example
  ----------------- ----------------- ----------------- ---------------------
  `broker_id`       string            Unique identifier `5758`
                                      of the broker or  
                                      brokerage.        

  `broker_name`     string            Name of the       `Spade Consultancy`
                                      broker or real    
                                      estate company.   

  `broker_email`    string            Email address of  `broker@email.com`
                                      the broker.       

  `broker_phone`    string            Phone number of   `01001436511`
                                      the broker.       
  ---------------------------------------------------------------------------

> Phone numbers are stored as strings to preserve leading zeros and
> avoid numeric formatting problems.

------------------------------------------------------------------------

## 10. Contact Information

  ------------------------------------------------------------------------------
  Column               Data Type         Description       Example
  -------------------- ----------------- ----------------- ---------------------
  `contact_phone`      string            Primary phone     `01201234567`
                                         number associated 
                                         with the listing  
                                         contact.          

  `contact_whatsapp`   string            WhatsApp number   `01201234567`
                                         associated with   
                                         the listing.      

  `contact_email`      string            Email address     `contact@email.com`
                                         associated with   
                                         the listing       
                                         contact.          
  ------------------------------------------------------------------------------

Contact fields are retained in the cleaned dataset but are generally not
required for analytical Power BI dashboards.

------------------------------------------------------------------------

## 11. Dates and Data Collection

  --------------------------------------------------------------------------------------
  Column            Data Type         Description          Example
  ----------------- ----------------- -------------------- -----------------------------
  `listed_date`     datetime          Date and time when   `2026-03-03 19:15:06+00:00`
                                      the listing was      
                                      published/recorded   
                                      on the source        
                                      platform.            

  `scraped_at`      datetime          Date and time when   `2026-03-04 14:20:33+00:00`
                                      the listing was      
                                      collected by the     
                                      scraping process.    
  --------------------------------------------------------------------------------------

### Important Difference

-   `listed_date` = when the property listing was published/recorded.
-   `scraped_at` = when the dataset collection process captured the
    listing.

These fields can be used for time-based analysis.

------------------------------------------------------------------------

# Data Preparation and Cleaning Decisions

The following cleaning decisions were applied during preparation:

### Missing categorical values

Selected categorical missing values were replaced with:

``` text
Not Specified
```

This applies to:

-   `completion_status`
-   `payment_method`
-   `furnished`
-   `district`
-   `subdistrict`

The original distinctions in `completion_status` were preserved.

### Numeric fields

-   `bedrooms` → nullable integer
-   `bathrooms` → nullable integer
-   `price_egp` → numeric
-   `area_value` → numeric
-   `lat` → numeric
-   `lon` → numeric
-   `images_count` → nullable integer

Missing numeric values were not replaced with zero because a missing
value does not mean that the property has zero bedrooms, bathrooms,
area, or images.

### Identifier fields

The following were treated as identifiers and stored as strings:

-   `listing_id`
-   `internal_id`
-   `agent_id`
-   `broker_id`
-   `reference`
-   `rera`

### Phone fields

The following were stored as strings:

-   `broker_phone`
-   `contact_phone`
-   `contact_whatsapp`

### Boolean fields

Boolean attributes were stored using nullable Boolean type.

### Dates

`listed_date` and `scraped_at` were converted to datetime values.

------------------------------------------------------------------------

# Power BI Analytical Dataset

After cleaning, a subset of columns was selected for the Power BI
analytical dataset.

## Selected Columns

### Listing

``` text
listing_id
property_type
offering_type
completion_status
price_egp
price_period
area_value
bedrooms
bathrooms
furnished
```

### Location

``` text
city
town
district
subdistrict
lat
lon
```

### Features

``` text
is_premium
is_verified
is_featured
is_new_construction
is_direct_from_dev
is_exclusive
has_view_360
images_count
```

### Agent / Broker

``` text
agent_id
agent_name
agent_is_super
broker_id
broker_name
```

### Dates

``` text
listed_date
scraped_at
```

------------------------------------------------------------------------

# Dataset Structure

``` text
Egypt Real Estate Listings
│
├── Listing Identification
│   ├── listing_id
│   ├── internal_id
│   ├── category
│   ├── listing_type
│   ├── detail_url
│   ├── reference
│   └── rera
│
├── Property Information
│   ├── property_type
│   ├── offering_type
│   ├── completion_status
│   ├── title
│   ├── description
│   ├── bedrooms
│   ├── bathrooms
│   ├── area_value
│   ├── area_unit
│   ├── furnished
│   └── listing_level
│
├── Pricing Information
│   ├── price_egp
│   ├── price_period
│   ├── price_currency
│   └── payment_method
│
├── Location Information
│   ├── location_full
│   ├── city
│   ├── town
│   ├── district
│   ├── subdistrict
│   ├── lat
│   └── lon
│
├── Listing Attributes
│   ├── is_premium
│   ├── is_verified
│   ├── is_featured
│   ├── is_new_construction
│   ├── is_direct_from_dev
│   ├── is_exclusive
│   ├── agent_is_super
│   └── has_view_360
│
├── Media
│   ├── images_count
│   └── video_url
│
├── Amenities
│   └── amenities
│
├── Agent Information
│   ├── agent_id
│   ├── agent_name
│   ├── agent_email
│   ├── agent_is_super
│   └── agent_languages
│
├── Broker Information
│   ├── broker_id
│   ├── broker_name
│   ├── broker_email
│   └── broker_phone
│
├── Contact Information
│   ├── contact_phone
│   ├── contact_whatsapp
│   └── contact_email
│
└── Dates
    ├── listed_date
    └── scraped_at
```

------------------------------------------------------------------------

# Potential Analytical Use

The dataset can be used to analyze:

-   Total number of property listings.
-   Property distribution by property type.
-   Property distribution by city, town, district, and subdistrict.
-   Property prices across different locations.
-   Average and median property prices.
-   Price per square meter.
-   Relationship between property price and area.
-   Property size distribution.
-   Bedroom and bathroom distribution.
-   Completed versus off-plan listings.
-   Furnished versus non-furnished properties.
-   Premium, verified, featured, and exclusive listings.
-   New construction versus other listings.
-   Direct developer versus broker listings.
-   Agent and broker listing activity.
-   Geographic distribution using latitude and longitude.
-   Listing activity over time.
-   Payment method distribution.
-   Relationship between property features and prices.
-   Amenity availability and its relationship with property prices.

------------------------------------------------------------------------

# Recommended Power BI Measures

The cleaned dataset can support measures such as:

``` text
Total Listings
Average Price
Median Price
Average Area
Average Price per SQM
Total Premium Listings
Verified Listings %
Off-Plan Listings %
Completed Listings %
Average Price by Property Type
Average Price by Location
Listings by Broker
Listings by Agent
```

These measures will be implemented in Power BI using DAX.

------------------------------------------------------------------------

# Data Notes

-   Each row represents one real estate listing.
-   `listing_id` is the primary business identifier for a listing.
-   Identifier columns should not be treated as numerical measures.
-   Some fields may contain missing values.
-   Missing categorical values that were explicitly cleaned are
    represented by `Not Specified`.
-   Missing numerical values were preserved rather than replaced with
    zero.
-   `amenities` and `agent_languages` contain multiple values separated
    by `|`.
-   `description` and `title` are unstructured text fields.
-   Contact information is generally not required for analytical
    dashboards.
-   `price_egp` and `area_value` can be used to calculate price per
    square meter.
-   `lat` and `lon` can be used for map-based analysis.
-   `listed_date` should be used for listing activity analysis, while
    `scraped_at` represents the data collection timestamp.
-   The `completion_status` categories were preserved as provided by the
    source rather than being merged.
