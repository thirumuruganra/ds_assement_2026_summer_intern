# Motorq Data Science Assignment 2025

## Overview
This repository contains the Motorq Data Science Assignment for 2025, focusing on cleaning and processing real-world vehicle telemetry data. The assignment involves handling various data anomalies and issues commonly encountered in vehicle telemetry datasets.

## Dataset Description
The dataset contains vehicle telemetry data where each record is a JSON object with the following structure:

### Key Fields
- **VIN**: Vehicle Identification Number that uniquely identifies a vehicle
- **statusTimestamp**: Timestamp when all parameters in the JSON were recorded for the given vehicle
- **statusData**: List containing parameter items with:
  - `attribute`: Name of the parameter recorded
  - `value`: Value of the parameter recorded
- **pollerFetchTime**: Timestamp when the record was received from the vehicle

## Data Cleaning Tasks

### 1. Out of Order Data
**Problem**: Messages sometimes arrive with older statusTimestamp after newer ones have already been received.

**Impact**: Can cause severe issues including system downtime if not handled properly.

**Solution**: Identify and delete out-of-order messages where statusTimestamp is older than any previously fetched message.

**Example**: If a message with statusTimestamp `2025-07-01 13:50:42.654` is received, drop all subsequent messages with statusTimestamp less than `2025-07-01 13:50:42.654`.

### 2. Duplicate/Conflicting Messages
**Problem**: Multiple messages with the same statusTimestamp exist.

**Impact**: Creates conflicting messages when checking for the last known message.

**Solution**: Keep only the first message (by pollerFetchTime) for each statusTimestamp and delete the rest.

**Example**: For messages with identical statusTimestamp `2025-07-01 13:50:42.654`, retain only the one fetched first.

### 3. Odometer Anomalies
**Problem**: Odometer values decrease over time, which is physically impossible.

**Impact**: Invalid distance calculations and unreliable vehicle tracking.

**Solution**: Identify and delete records where odometer values are decreasing compared to previous readings.

## Files in Repository
- `Motorq Data Science Assignment 2025.docx` - Assignment specification document
- `Test_Case_dataCleaning.zip` - Dataset containing vehicle telemetry data (managed via Git LFS)
- `README.md` - This documentation file

## Technical Requirements
- Handle JSON data processing
- Implement timestamp-based sorting and filtering
- Detect and remove data anomalies
- Maintain data integrity throughout the cleaning process

## Getting Started
1. Clone this repository
2. Extract the dataset from `Test_Case_dataCleaning.zip`
3. Implement the data cleaning logic for each of the three tasks
4. Validate the cleaned dataset

## Next Steps
Upon completion of these tasks, reach out to Motorq for follow-up discussions and further evaluation.

---
*This assignment tests practical data engineering skills with real-world vehicle telemetry data challenges.*
