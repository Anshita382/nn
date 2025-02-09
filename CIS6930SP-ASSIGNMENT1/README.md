# cis6930sp25 -- Assignment1

Name: Anshita Rayalla

## Assignment Description

This project creates a Python package that interacts with Gainesville's Crime Reports API to fetch and format crime incident data. Using the Gainesville Open Data Portal, the program downloads crime records and formats them with specific fields (incident type, report date, offense date, latitude, and longitude) separated by the thorn character (þ). Users can specify pagination parameters (offset and limit) to control the amount of data retrieved.

## How to install

```bash
pipenv install -e .
```

## How to run

For API data retrieval:
```bash
pipenv run python main.py --url https://data.cityofgainesville.org/resource/gvua-xt9q.json --offset <OFFSET> --limit <LIMIT>
```

## Example

Example command:
```bash
pipenv run python main.py --url https://data.cityofgainesville.org/resource/gvua-xt9q.json --offset 0 --limit 2
```

Output:
```
Drug Violationþ2025-01-20T20:35:26.000þ2025-01-20T19:35:25.000þ29.66545þ-82.3245
Theft Petit - Retailþ2025-01-20T20:23:15.000þ2025-01-20T19:53:00.000þ29.67054þ-82.33914
```

## Features and functions

#### main.py
- downloaddata() - Downloads crime data from the API URL using requests library, handling pagination
- parse_data() - Processes the downloaded data into the required thorn-separated format
- main() - Orchestrates the data retrieval and processing flow based on command line arguments

#### parsefile.py
- dojsonparse() - Extracts required fields from JSON data and formats them with thorn separators
- validate_fields() - Ensures data integrity and handles missing or null values

## Bugs and Assumptions

* API related:
  - The API endpoint must return data in JSON format
  - Required fields (incident_type, report_date, offense_date, latitude, longitude) are present
  - API supports pagination through offset and limit parameters

* Data handling:
  - Empty or null fields will be represented as blank spaces between thorns
  - All dates must be in ISO format
  - Coordinates are assumed to be valid decimal numbers
  - The program will skip any malformed records
  - File input is assumed to be UTF-8 encoded

* Performance limitations:
  - Large limit values may cause slower performance
  - Memory usage increases with response size
  - Network timeouts or connection errors will return empty results
