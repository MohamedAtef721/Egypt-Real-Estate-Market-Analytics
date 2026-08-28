# Egypt Real Estate Data Catalog

## Overview

This document describes the dataset used in the **Egypt Real Estate Analytics** project.

The dataset contains real estate listings collected from the Egyptian property market. Each record represents a property listing and includes information about the property, location, pricing, listing features, amenities, agents, brokers, and contact details.

---

# Data Dictionary

## 1. Listing Identification

| Column | Description | Example |
|---|---|---|
| `listing_id` | Unique identifier for each property listing. | `F7QB31CGWE509V2W7DF2GARB2C` |
| `internal_id` | Internal identifier associated with the listing in the source platform. | `56009081` |
| `category` | Main transaction category of the listing. | `buy` |
| `listing_type` | Type of listing available on the platform. | `property` |
| `detail_url` | URL of the original property listing. | Property listing URL |
| `reference` | Reference code used by the agent or broker for the listing. | `250pncash` |
| `rera` | Regulatory or registration reference associated with the listing, when available. | `NULL` |

---

## 2. Property Information

| Column | Description | Example |
|---|---|---|
| `property_type` | Type of property. | `Apartment`, `Villa`, `Duplex` |
| `offering_type` | Type of real estate offering. | `Residential for Sale` |
| `completion_status` | Current completion status of the property. | `completed`, `off_plan` |
| `title` | Title or headline of the property listing. | `Garden Villa - Lake View Boutique` |
| `description` | Detailed description of the property provided in the listing. | Property description text |
| `bedrooms` | Number of bedrooms in the property. | `3` |
| `bathrooms` | Number of bathrooms in the property. | `6` |
| `area_value` | Size of the property. | `445` |
| `area_unit` | Unit used to measure the property area. | `sqm` |
| `furnished` | Furnishing status of the property. | `PARTLY` |
| `listing_level` | Listing level or promotion tier on the platform. | `premium` |

---

## 3. Pricing Information

| Column | Description | Example |
|---|---|---|
| `price_egp` | Property price in Egyptian Pounds. | `24500000` |
| `price_period` | Period or transaction context associated with the price. | `sell` |
| `price_currency` | Currency of the listed price. | `EGP` |
| `payment_method` | Payment method specified in the listing. | `cash` |

---

## 4. Location Information

The dataset stores property locations at multiple geographic levels.

| Column | Description | Example |
|---|---|---|
| `location_full` | Full property location as provided in the listing. | `The Lakeview Boutique Villas, 5th Settlement...` |
| `city` | Main city or governorate classification. | `Cairo` |
| `town` | City or town within the main geographic area. | `New Cairo City` |
| `district` | Main district or neighborhood. | `The 5th Settlement` |
| `subdistrict` | More specific location within the district. | `5th Settlement Compounds` |
| `lat` | Geographic latitude of the property. | `30.04060173` |
| `lon` | Geographic longitude of the property. | `31.52594185` |

### Location Hierarchy

```text
City
└── Town
    └── District
        └── Subdistrict
```

---

## 5. Listing Attributes and Flags

The following columns indicate whether a listing has specific attributes.

| Column | Description | Example |
|---|---|---|
| `is_premium` | Indicates whether the listing has premium status. | `TRUE` |
| `is_verified` | Indicates whether the listing is verified. | `FALSE` |
| `is_featured` | Indicates whether the listing is featured. | `FALSE` |
| `is_new_construction` | Indicates whether the property is classified as new construction. | `FALSE` |
| `is_direct_from_dev` | Indicates whether the listing is directly from the developer. | `FALSE` |
| `is_exclusive` | Indicates whether the listing is exclusive to an agent or broker. | `FALSE` |

---

## 6. Listing Media

| Column | Description | Example |
|---|---|---|
| `images_count` | Number of images available in the property listing. | `6` |
| `has_view_360` | Indicates whether a 360-degree property view is available. | `FALSE` |
| `video_url` | URL of the property video, when available. | Video URL or `NULL` |

---

## 7. Dates and Data Collection

| Column | Description | Example |
|---|---|---|
| `listed_date` | Date and time when the property listing was published or recorded on the platform. | `2026-03-03T19:15:06Z` |
| `scraped_at` | Date and time when the listing data was collected from the source platform. | `2026-03-04T14:20:33.281007` |

### Important Difference

- `listed_date` represents when the listing was published.
- `scraped_at` represents when the data was collected by the scraping process.

---

## 8. Amenities

| Column | Description | Example |
|---|---|---|
| `amenities` | List of property features and amenities separated by the `|` character. | `Balcony \| Security \| Shared Pool` |

A single listing can contain multiple amenities.

Example:

```text
Balcony | Covered Parking | Private Garden | Private Pool | Security
```

This column can later be normalized into a separate table for analysis.

Example structure:

| listing_id | amenity |
|---|---|
| F7QB... | Balcony |
| F7QB... | Covered Parking |
| F7QB... | Private Garden |
| F7QB... | Private Pool |

---

## 9. Agent Information

| Column | Description | Example |
|---|---|---|
| `agent_id` | Unique identifier of the real estate agent. | `58866` |
| `agent_name` | Name of the agent responsible for the listing. | `pierre osama` |
| `agent_email` | Email address of the agent. | `agent@email.com` |
| `agent_is_super` | Indicates whether the agent has a super or elevated status. | `FALSE` |
| `agent_languages` | Languages spoken by the agent. Multiple values may be separated by `|`. | `English \| Arabic` |

---

## 10. Broker Information

The broker generally represents the real estate company or brokerage associated with the listing.

| Column | Description | Example |
|---|---|---|
| `broker_id` | Unique identifier of the broker or real estate company. | `5758` |
| `broker_name` | Name of the broker or real estate company. | `Spade Consultancy` |
| `broker_email` | Email address of the broker. | `broker@email.com` |
| `broker_phone` | Phone number of the broker. | `01001436511` |

---

## 11. Contact Information

| Column | Description | Example |
|---|---|---|
| `contact_phone` | Primary phone number provided for contacting the listing owner or agent. | `01201234567` |
| `contact_whatsapp` | WhatsApp contact number associated with the listing. | `01201234567` |
| `contact_email` | Email address provided for contacting the listing representative. | `contact@email.com` |

---

# Dataset Structure

The dataset can be logically divided into the following business areas:

```text
Egypt Real Estate Listings
│
├── Listing Information
│   ├── listing_id
│   ├── internal_id
│   ├── category
│   ├── listing_type
│   ├── title
│   ├── detail_url
│   └── reference
│
├── Property Information
│   ├── property_type
│   ├── offering_type
│   ├── completion_status
│   ├── bedrooms
│   ├── bathrooms
│   ├── area_value
│   ├── area_unit
│   └── furnished
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
│   └── is_exclusive
│
├── Media
│   ├── images_count
│   ├── has_view_360
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

# Potential Analytical Use

This dataset can be used to analyze:

- Real estate listing distribution across Egyptian cities and districts.
- Property prices and price per square meter.
- Differences between property types.
- Property size, bedrooms, and bathrooms distribution.
- Premium, verified, and featured listing percentages.
- Completed versus off-plan properties.
- Furnished versus unfurnished properties.
- Most expensive cities and districts.
- Agent and broker listing activity.
- Most common property amenities.
- The relationship between amenities and property prices.
- Geographic distribution of listings using latitude and longitude.
- Listing activity over time using listing and scraping dates.

# Data Notes

- Each row represents a real estate listing.
- `listing_id` should be treated as the primary business identifier for the listing.
- Some columns may contain missing or empty values.
- `amenities` and `agent_languages` contain multiple values and may require splitting before detailed analysis.
- Contact information may not be necessary for analytical dashboards and can remain only in the raw data layer.
- `description` and `title` are unstructured text fields and can optionally be used for text analysis.
- `price_egp` can be combined with `area_value` to calculate **Price per Square Meter**.
- Geographic coordinates (`lat`, `lon`) can be used for map-based analysis.