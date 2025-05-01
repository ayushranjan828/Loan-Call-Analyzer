# Loan Collection Data Pipeline

## Overview
The Loan Collection Data Pipeline is designed to automate the process of fetching, cleaning, transforming, and reporting daily call data for loan collections. This project simulates a real-world operational use case where organizations run daily call campaigns to collect loan payments. The pipeline integrates data from multiple sources, including call logs, agent rosters, and disposition summaries, to provide insights into agent performance.

## Features
- **Data Ingestion**: Read data from multiple CSV files.
- **Data Validation**: Ensure data integrity by checking for missing values and duplicates.
- **Data Merging**: Combine datasets based on common keys to create a comprehensive view.
- **Feature Engineering**: Calculate key performance metrics such as:
  - Total Calls Made
  - Unique Loans Contacted
  - Connect Rate (Completed Calls / Total Calls)
  - Average Call Duration (in minutes)
  - Presence (1 if login_time exists, else 0)
- **Reporting**: Generate a summary report in CSV format and a Slack-style summary message for quick insights.

## File Structure
```
/loan_collection_pipeline
│
├── MultipleFiles
│   ├── call_logs.csv
│   │   ├── Columns: call_id, agent_id, org_id, installment_id, status, duration, created_ts, call_date
│   │   └── Sample Data:
│   │       C5333,A020,O2,L1826,completed,5.68,2025-04-28T15:40:00,2025-04-28
│   │       C3045,A018,O1,L1996,no_answer,14.27,2025-04-28T02:41:00,2025-04-28
│   │       ...
│   │
│   ├── agent_roster.csv
│   │   ├── Columns: agent_id, users_first_name, users_last_name, users_office_location, org_id
│   │   └── Sample Data:
│   │       A001,AgentFirst1,AgentLast1,Bangalore,O1
│   │       A002,AgentFirst2,AgentLast2,Delhi,O1
│   │       ...
│   │
│   └── disposition_summary.csv
│       ├── Columns: agent_id, org_id, call_date, login_time
│       └── Sample Data:
│           A001,O1,2025-04-28,11:58
│           A002,O1,2025-04-28,10:05
│           ...
│
├── agent_performance_summary.csv
│   ├── Columns: agent_id, call_date, total_calls, unique_loans_contacted, completed_calls, avg_call_duration, presence, connect_rate
│   └── Sample Data:
│       A001,2025-04-28,10,5,8,6.5,1,0.80
│       A002,2025-04-28,12,6,10,5.5,1,0.83
│       ...
│
├── loan_collection_pipeline.py
│   ├── Description: Main script to run the data pipeline
│   └── Contains functions for data ingestion, validation, merging, feature engineering, and reporting
│
└── README.md
    ├── Description: Overview of the project, setup instructions, and usage
    └── Example usage of the pipeline
```

## Requirements
- Python 3.x
- Pandas library

## Installation
1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/loan_collection_pipeline.git
   cd loan_collection_pipeline
   ```

2. **Install the required packages**:
   ```bash
   pip install pandas
   ```

## Usage
1. **Prepare your CSV files**: Place your CSV files (`call_logs.csv`, `agent_roster.csv`, `disposition_summary.csv`) in the `MultipleFiles` directory. You can use the sample data provided or replace them with your own data.

2. **Run the pipeline**:
   ```bash
   python loan_collection_pipeline.py
   ```

3. **Output**: The output report will be saved as `agent_performance_summary.csv` in the project directory. A summary message will also be printed to the console, providing insights into the top-performing agent and overall metrics.

## Example Data
Sample data files are included in the `MultipleFiles` directory. You can modify these files or replace them with your own data as needed.

## Logging
The script includes logging for data validation and processing steps. You can adjust the logging level in the script to see more or less detailed output.

## Contributing
Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact
For any questions or feedback, please reach out to [your.email@example.com](mailto:your.email@example.com).

## Future Work
- Implement CLI arguments to accept file paths dynamically.
- Enhance logging to include error handling and debugging information.
- Add unit tests for individual functions to ensure reliability.
- Extend the pipeline to support additional data sources and metrics.
```