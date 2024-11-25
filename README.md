# phbs-qps-cyc-2024
## My Repository URL
https://github.com/YichaoCHEN2023/phbs-qps-cyc-2024
## Inflation Data Fetcher Instructions
This guide will help you set up your environment and run a script to fetch and report the last four quarters of inflation data in the United States.
### Step 1: Install Python
Ensure that Python is installed on your computer. You can download and install it from the [Python official website](https://www.python.org/downloads/).
### Step 2: Install Necessary Libraries
Open your command line interface (CMD or PowerShell on Windows, Terminal on macOS or Linux) and run the following command to install the required Python libraries:
```bash
pip install pandas pandas-datareader
```
### Step 3: Create a Project Folder
Create a new folder on your computer to store the script and any other resources. For example, you can create a folder named "InflationDataProject" on your desktop.
### Step 4: Write the Script
Open a text editor (like Notepad++, Sublime Text, or Visual Studio Code) and copy and paste the following code:
```python
import pandas as pd
from pandas_datareader import data as pdr
import datetime
def fetch_inflation_data():
    # Define the CPI series code for All Urban Consumers
    cpi_code = 'CPIAUCSL'
    
    # Set the end date as today
    end_date = datetime.datetime.today()
    # Set the start date as one year before the end date
    start_date = end_date - datetime.timedelta(days=365)
    
    # Fetch the CPI data from FRED
    cpi_data = pdr.get_data_fred(cpi_code, start=start_date, end=end_date)
    
    # Resample to quarterly data by taking the last observation in each quarter
    cpi_quarterly = cpi_data.resample('Q').last()
    
    # Calculate quarterly percentage change (inflation)
    inflation_quarterly = cpi_quarterly.pct_change().mul(100)
    
    # Get the last four quarters of inflation
    last_four_quarters = inflation_quarterly.tail(4)
    
    # Print the results
    print("Last Four Quarters of Inflation in the US:")
    print(last_four_quarters)

if __name__ == "__main__":
    fetch_inflation_data()
```
Save this code as `fetch_inflation.py` and place it in the project folder you created.
### Step 5: Run the Script
Navigate to the project folder containing `fetch_inflation.py` in your command line interface. For example, if your project folder is on the desktop, you can use the following command:

```bash
cd Desktop/InflationDataProject
```

Then, run the script:

```bash
python fetch_inflation.py
```
### Step 6: View the Results
The script will output the inflation rates for the last four quarters in the United States. If you encounter any errors, check that your Python environment and libraries are correctly installed.

### Notes
- Ensure you have a stable internet connection, as the script requires data from the FRED database.
- If you encounter permission issues when running the script, try running the command line interface as an administrator.
- If you are using Jupyter Notebook or another IDE, you can run the script directly within it without using the command line interface.

By following these steps, you should be able to successfully run the script and obtain the desired inflation data.
