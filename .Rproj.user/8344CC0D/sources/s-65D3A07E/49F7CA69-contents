library(readr)
library(dplyr)
library(tidyverse)
library(tigris)

# The zipcodes we want to focus on:
zipcodes <- c(77005, 77004, 77030)

# Importing the safegraph weekly patterns and home panel datasets
X2020_06_08_weekly_patterns_csv <- read_csv("safegraph/2020-06-08-weekly-patterns.csv.gz")
X2020_06_08_home_panel_summary <- read_csv("safegraph/2020-06-08-home-panel-summary.csv")
X2020_06_01_weekly_patterns_csv <- read_csv("safegraph/2020-06-01-weekly-patterns.csv.gz")
X2020_06_01_home_panel_summary <- read_csv("safegraph/2020-06-01-home-panel-summary.csv")


# Filtering them for certain zip codes and writing them into a CSV
X2020_06_08_weekly_patterns_csv <- filter(X2020_06_08_weekly_patterns_csv, is.element(postal_code, zipcodes))
X2020_06_01_weekly_patterns_csv <- filter(X2020_06_01_weekly_patterns_csv, is.element(postal_code, zipcodes))
write_csv(X2020_06_08_weekly_patterns_csv, "C:\\Users\\roone\\Documents\\demoShiny\\safegraph\\2020-06-08-weekly-patterns.csv.gz")
write_csv(X2020_06_01_weekly_patterns_csv, "C:\\Users\\roone\\Documents\\demoShiny\\safegraph\\2020-06-01-weekly-patterns.csv.gz")

# Combining core-POI from SG by binding the rows 
core_poi_part1_csv <- read_csv("core_poi-part1.csv.gz")
core_poi_part2_csv <- read_csv("core_poi-part2.csv.gz")
core_poi_part3_csv <- read_csv("core_poi-part3.csv.gz")
core_poi_part4_csv <- read_csv("core_poi-part4.csv.gz")
core_poi_part5_csv <- read_csv("core_poi-part5.csv.gz")

# Binding the rows together into the df poi
poi <- bind_rows(core_poi_part1_csv, core_poi_part2_csv, core_poi_part3_csv, core_poi_part4_csv, core_poi_part5_csv)
summary(poi)

# Filtering the POI for the zipcodes and writing them in a CSV
poi <- filter(poi, is.element(postal_code, zipcodes))
write_csv(poi, "C:\\Users\\roone\\Documents\\demoShiny\\safegraph\\poi.gz")

# Go through all df parts in a the subdirectories of a directory, parse, and then bind them together 
# and then write them into a folder with unique tags based on the date on the directory. 

# Meant to be used after downloading an entire data catalog
dirs <- list.dirs(path="C:/Users/roone/Downloads/FireShot/safegraph/patterns/2020/08", full.names=TRUE, recursive=FALSE)
for (dir in dirs) {
  dir
  seconddirs <- list.dirs(path=dir, full.names=TRUE, recursive=FALSE)
  seconddirs
  files <- list.files(path=seconddirs[1], pattern="*.csv.gz", full.names=TRUE, recursive=FALSE)
  for (df in files) {
    csvFiles <- c()
    csvFiles <- csvFiles %>% append(read_csv(df))
    # newWeekPatterns
  }
  newWeekPatterns <- bind_rows(csvFiles)
  # summary(csvFiles)
  # summary(newWeekPatterns)
  newWeekPatterns <- filter(newWeekPatterns, is.element(postal_code, zipcodes))
  splitDir <- unlist(strsplit(dir, split = "/")[1])
  date <- paste(splitDir[length(splitDir)-2], splitDir[length(splitDir)-1], splitDir[length(splitDir)], sep = "-")
  date
  write_csv(newWeekPatterns, paste("C:\\Users\\roone\\Documents\\demoShiny\\safegraph\\", date, ".csv.gz"))
}

# Go through all weeklyPatterns parts held in a folder and then bind them together
files <- list.files(path="C:\\Users\\roone\\Downloads\\FireShot\\safegraph\\patterns\\2020\\06\\24", pattern="*.csv.gz", full.names=TRUE, recursive=FALSE)
for (df in files) {
  csvFiles <- c()
  csvFiles <- csvFiles %>% append(read_csv(df))
  newWeekPatterns <- bind_rows(csvFiles)
  # newWeekPatterns
}
newWeekPatterns <- filter(newWeekPatterns, is.element(postal_code, zipcodes))
write_csv(newWeekPatterns, "C:\\Users\\roone\\Documents\\demoShiny\\safegraph\\2020-06-24-weeky-patterns.csv.gz")

# Use this for combining the parts of and filtering homegroup data catalogs
# Meant to be used after downloading an entire data catalog
dirs <- list.dirs(path="C:/Users/roone/Downloads/FireShot/safegraph/home_panel_summary/2020/08", full.names=TRUE, recursive=FALSE)
for (dir in dirs) {
  dir
  seconddirs <- list.dirs(path=dir, full.names=TRUE, recursive=FALSE)
  seconddirs
  files <- list.files(path=seconddirs[1], pattern="*.csv", full.names=TRUE, recursive=FALSE)
  for (df in files) {
    csvFiles <- c()
    csvFiles <- csvFiles %>% append(read_csv(df))
    # newWeekPatterns
  }
  # head(csvFiles[1])
  newWeekPatterns <- bind_rows(csvFiles)
  # summary(csvFiles)
  # summary(newWeekPatterns)
  
  newWeekPatterns <- filter(newWeekPatterns, is.element(state, "tx"))
  splitDir <- unlist(strsplit(dir, split = "/")[1])
  date <- paste(splitDir[length(splitDir)-2], splitDir[length(splitDir)-1], splitDir[length(splitDir)], sep = "-")
  write_csv(newWeekPatterns, paste0("C:/Users/roone/Documents/demoShiny/safegraph/",date, "-home-panel.csv"))
}
