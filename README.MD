# Seat Tracker

This Jupyter Notebook, 

seat_tracker.ipynb

, is designed to track and analyze concert seat availability and pricing for various venues in Toronto. It fetches event data, processes it, and saves the results in a CSV file and JSON files for further analysis.

## Table of Contents

- Installation
- Usage
- [File Structure](#file-structure)
- [Data Processing](#data-processing)
- Output

## Installation

To run this notebook, you need to have the following Python packages installed:

- [`requests`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22vscode-notebook-cell%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Feric9%2FOneDrive%20-%20University%20of%20Waterloo%2FProjects%2FConcert-Seat-Tracker%2Fseat_tracker.ipynb%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22W3sZmlsZQ%3D%3D%22%7D%2C%22pos%22%3A%7B%22line%22%3A0%2C%22character%22%3A7%7D%7D%5D%2C%22779b0ca9-b837-4cbf-99e0-a5a0ec10ab7d%22%5D "Go to definition")
- `beautifulsoup4`
- `pandas`
- [`json`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22vscode-notebook-cell%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Feric9%2FOneDrive%20-%20University%20of%20Waterloo%2FProjects%2FConcert-Seat-Tracker%2Fseat_tracker.ipynb%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22W3sZmlsZQ%3D%3D%22%7D%2C%22pos%22%3A%7B%22line%22%3A15%2C%22character%22%3A11%7D%7D%5D%2C%22779b0ca9-b837-4cbf-99e0-a5a0ec10ab7d%22%5D "Go to definition")

You can install these packages using pip:

```sh
pip install requests beautifulsoup4 pandas
```

## Usage

1. Open the 

seat_tracker.ipynb

 notebook in Jupyter Notebook or JupyterLab.
2. Run the cells sequentially to fetch and process the event data.
3. The notebook will save the processed data into a CSV file and JSON files.

## File Structure

- `Concert Seats.csv`: The main CSV file where the processed seat data is stored.
- 

seat_tracker.ipynb

: The Jupyter Notebook containing the code for fetching and processing event data.
- `venue sections/`: Directory containing JSON files for each venue with section details.
  - `Queen Elizabeth Theatre Toronto sections.json`
  - `Rogers Centre sections.json`
  - `Rogers Stadium sections.json`
  - `The Rockpile East sections.json`

## Data Processing

The notebook performs the following steps:

1. Fetches event data from a specified URL.
2. Filters events based on the venue location (Toronto).
3. Extracts detailed seat information from the event page using BeautifulSoup.
4. Parses the extracted data and converts it into a pandas DataFrame.
5. Merges the new data with existing data in `Concert Seats.csv`.
6. Saves the updated data back to `Concert Seats.csv`.
7. Updates JSON files in the `venue sections/` directory with section details for each venue.

## Output

- **CSV File**: The `Concert Seats.csv` file contains the consolidated seat data for all processed events.
- **JSON Files**: The JSON files in the `venue sections/` directory contain section details for each venue.

## Example

Here is an example of how the data is processed and saved:

```python
import requests
from bs4 import BeautifulSoup
import json
import pandas as pd

# Example artist list
artists = ["Taylor Swift", "Ed Sheeran"]

for a in artists:
    # Get the page source
    artist_search_url = generate_stubhub_url(a, "Toronto")
    response = requests.get(artist_search_url)
    soup = BeautifulSoup(response.content, 'html.parser')
    
    # Extract the JSON string from the script tag with id '