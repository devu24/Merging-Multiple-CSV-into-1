Report on Merging Multiple CSV Files Using Python

1. Introduction

This report details the Python script designed to merge multiple CSV files stored in a folder into a single CSV file. The script utilizes the Pandas library for data handling and the Glob and OS modules for file management.

2. Libraries Used

pandas: For reading, merging, and saving CSV files.

glob: To retrieve all CSV file paths within a specified folder.

os: To handle file paths in a cross-platform manner.

3. Implementation Details

The script defines a function to automate the merging process:

Function: merge_csv_files(folder_path, output_file)

This function performs the following steps:

Normalize the file path: Ensures correct formatting and removes unwanted characters.

Retrieve all CSV files: Uses glob.glob() to list all CSV files in the given directory.

Check for CSV availability: If no files are found, it prints an error message and exits.

Read and store data: Reads each CSV file into a Pandas DataFrame and stores them in a list.

Concatenate DataFrames: Uses pd.concat() to merge all DataFrames, ensuring that indexing is handled properly.

Save the merged file: Writes the combined DataFrame into a new CSV file.

Code Implementation

import pandas as pd
import glob
import os

def merge_csv_files(folder_path, output_file):
    folder_path = folder_path.strip("'")  # Remove single quotes if present
    folder_path = folder_path.replace("\\", "/")  # Normalize path

    all_files = glob.glob(os.path.join(folder_path, "*.csv"))
    print(all_files)
    if not all_files:
        print("No CSV files found in the folder.")
        return

    df_list = [pd.read_csv(file) for file in all_files]
    merged_df = pd.concat(df_list, ignore_index=True)
    merged_df.to_csv(output_file, index=False)
    print(f"Successfully merged {len(all_files)} files into {output_file}")

4. Usage Example

To execute the script, define the folder containing CSV files and specify an output file path:

folder_path = r"C:\\Users\\rahul\\Downloads\\Sample Dataset"  # Windows path
output_file = r"C:\\Users\\rahul\\Downloads\\Sample Dataset\\merged_output.csv"
merge_csv_files(folder_path, output_file)

5. Key Features & Benefits

Automated Processing: Merges all CSV files in a folder without manual intervention.

Scalability: Works with multiple CSV files of varying sizes and structures.

Efficiency: Uses Pandas for fast data handling and merging.

Error Handling: Includes checks for missing files and path normalization.

6. Potential Enhancements

Handling Different Column Structures: Currently assumes all CSV files have the same structure. Adding support for column alignment would improve versatility.

Logging & Reporting: Implementing logging to track errors and successful merges.

GUI Interface: Developing a graphical user interface for non-programmers to select folders/files easily.

Data Cleaning Options: Adding filters to remove duplicates or empty rows before merging.

7. Conclusion

This script is a robust solution for automating the merging of multiple CSV files into a single dataset. Future improvements can enhance functionality by introducing logging, error handling, and data preprocessing.
