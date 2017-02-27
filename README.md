# get-ACLED

## An R function to ingest ACLED event data using jsonlite for ingestion and data.table for processing

Wrap country name with quotes. Normally ACLED returns only 500 records per request.
This function overides that constraint and returns all records matching your country and year parameters.
This may occasionally exceed ACLED API memory limits and throw an error.
If you specify a country and no year, you are requesting all records of that country.
If you get an error, you have likely exceeded the memory limit.

Add a year to your request and see if you get data back.

If you do not specifiy either argument, this function returns the 10,000 most recent records from ACLED.
  
Required packages: jsonlite, data.table, lubridate, stringr

### The function: getACLED()

### An example work flow:

```r
source("acled_api_pull.R")

# make a list of countries you want data about

lcblist <- c("Nigeria", "Niger", "Cameroon", "Chad")

# use lapply to run the getACLED function for each country

lcb_data_list <- lapply(lcblist, getACLED)

# combine the results into a single data.table

lcb <- rbindlist(lcb_data_list)

# remove the big list

rm(lcb_data_list)
```

## Error Handling

This is a simple function that has no error handling. All errors I have received when using this function are result of exceeding ACLED's memory limits. In which case I just run it one country at time with a year specified.

If anyone is interested in adding error handling, I welcome it.
