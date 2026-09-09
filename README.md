Avionics Telemetry Analysis and Fault Detection Tool

**Submitted Files**

telemetry_sol.cpp — C++17 source code

telemetry_data.csv — input telemetry dataset

README.md — build and run instructions

**Requirements**

C++17-compatible compiler

GCC, Clang, or Microsoft Visual C++


**Input Format**

The program expects a CSV file with these columns:

Timestamp,Temperature,Pressure,Altitude,Velocity,Vibration,Acceleration

Missing values may be represented by an empty field, NA, N/A, null, or NULL.

**Build**

Linux/macOS

g++ -std=c++17 -Wall -Wextra -O2 telemetry_sol.cpp -o telemetry_sol

Windows with MinGW

g++ -std=c++17 -Wall -Wextra -O2 telemetry_sol.cpp -o telemetry_sol.exe

Windows with Visual Studio Developer Command Prompt

cl /std:c++17 /EHsc /O2 telemetry_sol.cpp

**Run**

Linux/macOS

./telemetry_sol telemetry_data.csv

Windows

telemetry_sol.exe telemetry_data.csv

To select the report filename:

./telemetry_sol telemetry_data.csv telemetry_report.csv

If no output filename is provided, the default file is:

telemetry_report.csv

**Processing Performed**

Read telemetry records from the CSV file.
Validate required columns and numeric values.
Detect physically invalid sensor values.
Handle missing values using linear interpolation when both neighboring values are available.
Apply a three-sample moving-average filter.
Detect threshold-based anomalies.
Detect rapid trend changes.
Calculate minimum, maximum, average, valid-sample, and missing-sample statistics.
Generate a structured CSV report.

**Configuration**

Sensor physical limits, operating limits, and trend thresholds are defined in the CONFIG map in telemetry_analyzer.cpp.

These values are example engineering limits and should be replaced with project-specific limits when official requirements are available.

**Output**

The report contains two sections:
Sensor summary statistics
Detailed anomaly records

The report can be opened in Microsoft Excel, LibreOffice Calc, or any text editor.

Example

g++ -std=c++17 -Wall -Wextra -O2 telemetry_sol.cpp -o telemetry_analyzer
./telemetry_sol telemetry_data.csv telemetry_report.csv

**Expected console output format:**

Telemetry analysis completed successfully.
Records processed: <number>
Anomalies detected: <number>
Report: telemetry_report.csv

**Error Handling**

The application reports errors for missing files, empty input files, missing required columns, invalid timestamps, and report-creation failures. Invalid records are handled without terminating the complete analysis where possible.
