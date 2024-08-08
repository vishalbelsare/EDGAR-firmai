# EDGAR

<a href="https://www.bellingcat.com"><img alt="Bellingcat logo: Discover Bellingcat" src="https://img.shields.io/badge/Discover%20Bellingcat-%20?style=for-the-badge&logo=data%3Aimage%2Fpng%3Bbase64%2CiVBORw0KGgoAAAANSUhEUgAAAA4AAAAYCAYAAADKx8xXAAABhGlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw0AcxV9TS0UqDnZQEcxQneyiIo6likWwUNoKrTqYXPoFTRqSFBdHwbXg4Mdi1cHFWVcHV0EQ%2FABxdnBSdJES%2F5cUWsR4cNyPd%2Fced%2B8AoVllqtkTA1TNMtKJuJjLr4rBVwQwhhBEDEvM1JOZxSw8x9c9fHy9i%2FIs73N%2Fjn6lYDLAJxLHmG5YxBvEs5uWznmfOMzKkkJ8Tjxp0AWJH7kuu%2FzGueSwwDPDRjY9TxwmFktdLHcxKxsq8QxxRFE1yhdyLiuctzir1Tpr35O%2FMFTQVjJcpzmKBJaQRIo6klFHBVVYiNKqkWIiTftxD%2F%2BI40%2BRSyZXBYwcC6hBheT4wf%2Fgd7dmcXrKTQrFgcCLbX%2BMA8FdoNWw7e9j226dAP5n4Err%2BGtNYO6T9EZHixwBA9vAxXVHk%2FeAyx1g6EmXDMmR%2FDSFYhF4P6NvygODt0Dfmttbex%2BnD0CWulq%2BAQ4OgYkSZa97vLu3u7d%2Fz7T7%2BwHEU3LHAa%2FQ6gAAAAZiS0dEAAAAAAAA%2BUO7fwAAAAlwSFlzAAAuIwAALiMBeKU%2FdgAAAAd0SU1FB%2BgFHwwiMH4odB4AAAAZdEVYdENvbW1lbnQAQ3JlYXRlZCB3aXRoIEdJTVBXgQ4XAAAA50lEQVQ4y82SvWpCQRCFz25ERSJiCNqlUiS1b5AuEEiZIq1NOsGXCKms0wXSp9T6dskDiFikyiPc%2FrMZyf3FXSGQ0%2BzuzPl2ZoeVKgQ0gQ2wBVpVHlcDkjM5V%2FJ5nag6sJ%2FZX%2Bh%2FC7gEhqeAFKf7p1M9aB3b5oN1OomB7g1axUBPBr3GQHODHmOgqUF3MZAzKI2d4LWBV4H%2BMXDuJd1a7Cew1k7SwksaHC4LqNaw7aeX9GWHXkC1G1sTAS17Y3Kk2lnp4wNLiz0DrgLq8qt2MfmSSabAO%2FBBXp26dtrADPjOmN%2BAUdG7B3cE61l5hOZiAAAAAElFTkSuQmCC&logoColor=%23fff&color=%23000"></a><!--
--><a href="https://discord.gg/bellingcat"><img alt="Discord logo: Join our community" src="https://img.shields.io/badge/Join%20our%20community-%20?style=for-the-badge&logo=discord&logoColor=%23fff&color=%235865F2"></a><!--
--><a href="https://colab.research.google.com/github/bellingcat/EDGAR/blob/main/notebook/Bellingcat_EDGAR_Tool.ipynb"><img alt="Colab icon: Try it on Colab" src="https://img.shields.io/badge/Try%20it%20on%20Colab-%20?style=for-the-badge&logo=googlecolab&logoColor=fff&logoSize=auto&color=e8710a">
</a>

Python tool to search and retrieve corporate and financial data from the United States Securities and Exchange Commission (SEC).

## What is EDGAR?

EDGAR is a database of corporate filings maintained by the SEC.
These filings contain a wealth of quantitative and qualitative information on every legal entity that issues non-exempt securities in the United States.
Whether you are looking to study the fundamentals of your favorite stocks, or to track the corporate webs weaved by a person or company of interest, EDGAR is the place to do it.

This tool was initially developed as part of the Bellingcat Tech Fellowship program, we hope it helps you utilise this incredible, free resource.

## Installation :magic_wand:

[![PyPI - Version](https://img.shields.io/pypi/v/edgar-tool)
](https://pypi.org/project/edgar-tool/)

You can install this tool directly from the [official PyPi release](https://pypi.org/project/edgar-tool/).

```bash
pip install edgar-tool
```

## Usage - Text Search :mag_right:

### What is the text search tool?

If you're interested in finding all the documents mentioning a certain person, company or phrase in the EDGAR database, you can do that via the [full text search page](https://www.sec.gov/edgar/search/#)

It isn't always easy to get the information you might need from the SEC, so this Python tool lets you download the search results to a file without having to go through all the pages of results by hand.

This is a command line tool that takes a search query, queries a server, and downloads the search results into a CSV file that can be opened in a spreadsheet program (such as Excel).

### Examples

```bash
# Display help message describing all supported arguments along with their usage, aliases and eventual default values (type q to exit)
edgar-tool text_search --help

# Basic usage (defaults to searching the last 5 years of records)
edgar-tool text_search John Doe

# Basic usage with a combination of exact and partial search parameters
edgar-tool text_search \"John Doe\" Pharmaceuticals Chemicals

# Usage with date range and export to custom CSV file
edgar-tool text_search Tsunami Hazards --start_date "2021-01-01" --end_date "2021-12-31" --output "results.csv"

# Usage with a partial set of filing forms + single forms
edgar-tool text_search Hurricane Damage --filing_form "registration_statements" --single_forms "['1-K', '1-SA']"

# Usage specifying the location of incorporation
edgar-tool text_search oil --inc_in "Egypt"

# More advanced usage specifying more arguments, with export to JSON
edgar-tool text_search Volcano Monitoring --start_date "2021-01-01" --end_date "2021-12-31" --output "results.json"\
          --filing_form "all_annual_quarterly_and_current_reports" --entity_id "0001030717" \
          --min_wait 5.0 --max_wait 7.0 --retries 3

# Using aliases where supported and exporting to JSONLines
edgar-tool text_search Calabarzon -s "2021-01-01" -o "results.jsonl" -f "all_annual_quarterly_and_current_reports" -r 3 -h
```

> [!WARNING]
> Combining text search parameters with `entity_id` parameter seems to increase the risk of failed requests on the SEC page due to an apparent bug, we recommend to either avoid doing so (you can specify an empty string for search keywords using `""` and use only entity ID) or setting the number of retries accordingly if you do so.

### Detailed Feature Information

<details>
<summary>Expand to view detailed feature information</summary>

#### Search parameters

Most search parameters from the EDGAR text search page are supported, including:
- `Document word or phrase` (mandatory)
- `Company name, ticker or CIK, or individual's name` (optional)
- `Filing category` (optional)
- `Filed from` and `Filed to` dates (optional)
- `Principal executive offices in` or `Incorporated in` (optional)

Currently unsupported search parameters are:
- `Filed date ranges` (since the same behavior can be achieved with `Filed from` and `Filed to` dates)

#### Output formats

Currently supported outputs formats are:
- CSV
- JSONLines (one JSON object per line)

Output format is determined by the file extension of the output file path.
Accepted values are `.csv` and `.jsonl` (case-insensitive).

#### Retries

The tool supports retries in case of failed requests. Retries can be configured with the `--retries` argument, and the wait time between retries will be a random number between `--min_wait` and `--max_wait` arguments.

</details>

## Usage - RSS Feed :card_index:

### What is the RSS feed customized retrieval tool ?

The SEC publish a live feed of filings and this part of the tool lets you monitor particular tickers for new filings, so you can get to-the-minute updates.

The output is a CSV file containing the company and filings' metadata, which can be opened in a spreadsheet program (such as Excel).

### Examples

```bash
# Display help message describing all supported arguments along with their usage, aliases and eventual default values (type q to exit)
edgar-tool rss --help

# Basic one-off usage with export to CSV
edgar-tool rss "GOOG" --output "rss_feed.csv"

# Periodic usage specifying 10 minutes interval duration, with export to JSON
edgar-tool rss "AAPL" "GOOG" "MSFT" --output "rss_feed.json" --every_n_mins 10

# Same example as above, using aliases and exporting to JSONLines (.jsonl)
edgar-tool rss "AAPL" "GOOG" "MSFT" -o "rss_feed.jsonl" -e 10
```

### Detailed Feature Information

<details>
<summary>Expand to view detailed feature information</summary>

#### Companies CIK to Ticker mapping

Since the RSS feed uses CIKs instead of tickers, the tool includes a mapping of CIKs to tickers, which is used to filter the feed by ticker.
This mapping is obtained from the [SEC website](https://www.sec.gov/files/company_tickers.json) and is updated on user request.

#### Periodic retrieval

The RSS feed data returns the last 200 filings and is updated every 10 minutes (which doesn't mean all tickers are updated every 10 minutes).
The tool can fetch the feed either once on-demand, or at regular intervals.

</details>

## Table of Cleaned Financial Data :bank:

There is also a table of data containing most income statements, balance sheets, and cash flow statements for every company traded publicly in the U.S.

This table is updated intermittently and is [available here for download as a .CSV file](https://edgar.marketinference.com/). You can open this file in Excel, use it as a data source for your own code, or use the simple Python script to access time series for the desired data points.

The quality of any programmatically produced financial dataset is not going to be as accurate or as complete as a S&P Global or Bloomberg subscription. It should, however, be of comparable accuracy to what you can find on Yahoo Finance and spans a wider time frame.

George Dyer, the former Bellingcat tech fellow who developed the first version of this tool, describes it as: "good enough use in projects such as [Market Inference](https://www.marketinference.com/) and [Graham](https://graham.marketinference.com/info)".

Please report any inconsistencies in the data to George and he will do his best to refine the existing method.

<details>
<summary>Expand to view the full method</summary>

The current table is created by the following method:

  - Monthly bulk download of all company facts data from EDGAR (this is the data set accessed by the official APIs)
  - Scraping of all calculation sheets related to each filing associated with a publicly traded company
  - Create a dictionary matching the most commonly used GAAP tags with a plain English term
  - For a given company, for each year:
    - Determine what GAAP tags are listed under each cashflow / income / balance sheet headings (or whatever alternative terms the company happens to use) in the calculation sheet
    - For each tag:
      - Obtain all the data associated with the tag in the company's bulk download folder for the desired year, and the preceding one
      - Determine whether the data is duration or point in time
      - Identify quarterly and yearly values based on the time data associated with each data point
      - Recalculate all quarterly values if the reported ones are cumulative
      - Calculate Q4 value
      - Create cleaned and sorted time series
      - Isolate the value for the considered year (or calculate trailing twelve month value based on preceding four quarters for this year if the company hasn't reported yet)
    - For some particularly problematic data points such as debts I use addition between related data points to ensure consistency (this is why the debt amounts are not always perfectly accurate, but almost always in the ballpark)
    - Match the GAAP tags with their plain English term
    - Keep a database of orphan tags, and add them into the dictionary, manually

</details>

## Development :octocat:

<details>
<summary>Expand to view information for developers</summary>

This section describes how to install the project to run it from source, for example if you want to build new features.

### Developing locally

```bash
# Clone the repository
git clone https://github.com/bellingcat/EDGAR.git

# Change directory to the project folder
cd EDGAR
```

This project uses [Poetry](https://python-poetry.org/docs) for dependency management and packaging.

```bash
# Install Poetry if you haven't already
pip install poetry

# Install dependencies
poetry install
```

Check out [Important commands](#important-commands) below for next steps.

### Developing using a GitHub Codespace

This project uses a custom Development Container supported by GitHub Codespaces. Creating a new Codespace automatically takes care of installing all supported Python interpreters, the Poetry package manager, and Python dependencies for you.

To create a new Codespace:
1. Click on the `<> Code` dropdown on the GitHub UI.
2. Click the `+` icon to create a new Codespace.

The Codespace will open for you automatically.

![GitHub UI screenshot showing the buttons to click to create a new Codespace](<docs/create_codespace.png>)

Check out [Important commands](#important-commands) below for next steps.

### Important commands

```bash
# Run the tool
poetry run edgar-tool --help

# Run unit tests using your Poetry environment's Python interpreter
poetry run pytest

# Run unit tests with tox
poetry run tox -- run-parallel
```

You can skip having to write `poetry run` before each command by activating Poetry's virtual environment with `poetry shell`. Once activated the following code is equivalent to the above:

```bash
# Spawn shell within Poetry's virtual environment
poetry shell

# Run the tool
edgar-tool --help

# Run unit tests using your Poetry environment's Python interpreter
pytest

# Run unit tests with tox
tox run-parallel
```

This is an actual example copy/pasted from a terminal:

```console
@edgar-dev ➜ /workspaces/EDGAR (main) $ pytest
bash: pytest: command not found

@edgar-dev ➜ /workspaces/EDGAR (main) $ poetry shell
Spawning shell within /home/vscode/.cache/pypoetry/virtualenvs/edgar-tool-vrvn8V2D-py3.12
(edgar-tool-py3.12) @edgar-dev ➜ /workspaces/EDGAR (main) $ pytest
================= test session starts ==================
platform linux -- Python 3.12.4, pytest-8.3.1, pluggy-1.5.0
rootdir: /workspaces/EDGAR
configfile: pyproject.toml
collected 1 item

tests/test_cli.py .                              [100%]

================== 1 passed in 0.20s ===================
(edgar-tool-py3.12) @edgar-dev ➜ /workspaces/EDGAR (main) $
```

</details>
