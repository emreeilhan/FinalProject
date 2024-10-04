Stock Data Extraction and Visualization

Project Overview

This project aims to extract, process, and visualize stock and revenue data for Tesla (TSLA) and GameStop (GME) using both API calls and web scraping techniques. Through the use of various Python libraries such as yfinance, requests, and BeautifulSoup, this project demonstrates how to gather financial data from multiple sources and display it in meaningful and insightful ways.

The end goal of this project is to generate interactive graphs that illustrate the historical stock prices and revenue of Tesla and GameStop. By visualizing this data, users can better understand the financial trends of these companies over time.

Table of Contents

	•	Project Overview
	•	Technologies Used
	•	Installation
	•	Project Structure
	•	How It Works
	•	Usage
	•	Contributors

Technologies Used

The following Python libraries are used in this project:

	•	Pandas: For data manipulation and analysis.
	•	YFinance: To extract historical stock data from Yahoo Finance.
	•	Requests: To fetch HTML content from web pages.
	•	BeautifulSoup: For web scraping and parsing HTML content.
	•	Plotly: For creating interactive visualizations and graphs.

Installation

To run this project locally, follow these steps:

	1.	Clone this repository:

git clone <repository-url>


	2.	Install the required Python packages:

pip install yfinance pandas requests beautifulsoup4 plotly


	3.	If you are working in Jupyter Notebook or Google Colab, make sure to install the nbformat package:

pip install nbformat


	4.	Once installed, you can run the Jupyter notebook or Python script to see the stock and revenue data being fetched, processed, and visualized.

Project Structure

	•	Stock Data Extraction.ipynb: Jupyter notebook containing the complete project code.
	•	README.md: This file, explaining the project and its usage.

How It Works

This project is divided into the following key steps:

1. Extracting Stock Data via YFinance

The YFinance library is used to retrieve historical stock prices for Tesla (TSLA) and GameStop (GME). The data is fetched with the Ticker object and the history() method, which extracts the maximum available period of data.

import yfinance as yf

tesla = yf.Ticker("TSLA")
tesla_data = tesla.history(period="max")
tesla_data.reset_index(inplace=True)

2. Web Scraping for Revenue Data

Since revenue data is not available through YFinance, we use web scraping to retrieve it from provided HTML web pages. Using the requests library, we download the HTML content, then parse it using BeautifulSoup to extract the relevant table of Tesla’s and GameStop’s revenue data.

url = "https://example-url.com/revenue"
html_data = requests.get(url).text
soup = BeautifulSoup(html_data, 'html.parser')
tesla_revenue = pd.read_html(str(soup))[0]

3. Data Cleaning and Processing

After extracting the data, some cleaning steps are applied to ensure the data is in a usable format. Specifically, we remove unwanted characters (such as commas and dollar signs) and handle missing values in the revenue data.

tesla_revenue["Revenue"] = tesla_revenue["Revenue"].str.replace(",|\$", "", regex=True)
tesla_revenue.dropna(inplace=True)

4. Visualizing Stock Prices and Revenue

The make_graph() function is defined to plot both the historical stock prices and revenue trends in one visualization. Plotly is used to create dynamic, interactive graphs.

def make_graph(stock_data, revenue_data, stock):
    fig = make_subplots(rows=2, cols=1, shared_xaxes=True, subplot_titles=("Historical Share Price", "Historical Revenue"))
    fig.add_trace(go.Scatter(x=pd.to_datetime(stock_data.Date), y=stock_data.Close, name="Share Price"), row=1, col=1)
    fig.add_trace(go.Scatter(x=pd.to_datetime(revenue_data.Date), y=revenue_data.Revenue, name="Revenue"), row=2, col=1)
    fig.show()

This function is used to generate visual representations for both Tesla and GameStop.

Usage

	1.	Run the notebook or script to fetch the stock and revenue data for Tesla and GameStop.
	2.	Once the data is fetched and processed, graphs will be displayed showing the trends in stock prices and revenue over time.
	3.	Explore the interactive graphs to gain insights into how these companies have performed historically.

Example

To generate a graph for Tesla, you can simply call the make_graph() function as shown below:

make_graph(tesla_data, tesla_revenue, 'Tesla')

This will display a two-part graph:

	•	The upper graph shows Tesla’s historical stock prices.
	•	The lower graph shows Tesla’s historical revenue data.

Contributors

	•	Joseph Santarcangelo – Lead Developer
	•	Azim Hirjani – Data Science Engineer
	•	Akansha Yadav – Data Scientist

