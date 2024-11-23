# cse6242-Data-Analytic-and-visualization-final-Project-Changda-Part
A radial tree layout with D3.js visualizes this hierarchy, allowing users to expand or collapse categories. 

## Introduction:
This project outlines the development of an interactive visualization tool built using D3.js, which will allow users to visually explore 3D model metadata and discover connections between various attributes, such as model categories and user interactions (likes, saves, comments). The tool will not only provide stakeholders and model publishers with a clear understanding of what drives model popularity and improves search engine optimization and consequently the performance of their products but also help them adjust their content strategies to better meet market demands. Changda is responsible for radial tree with D3.js visualizes this interaction.

## Method:
The overall structure of the visualization includes:  "data import", "data processing", "color mapping", "hierarchical data construction", "legends, nodes, link style processing", and "information display of the pop-up window".

### Dataset Introduction  
The data collection process involved developing a framework to scrape metadata from a 3D model marketplace with dynamic JavaScript content. Nearly 30,000 models were included in this project, presenting challenges in dynamic content rendering and large-scale data management. To overcome these issues, Selenium was employed to interact with JavaScript-rendered elements, while BeautifulSoup parsed static HTML. An SQLite database was used to manage URLs and track scraping progress, preventing redundancy and supporting resumability in case of interruptions。

For data preprocessing, the collected data was cleaned and standardized by removing duplicates and organizing models into hierarchical categories. Sentiment analysis was performed using TextBlob to analyze user comments. The preprocessed data was then exported as a CSV file, making it ready for visualization using D3.js. 

### Data Input
导入处理好的*.csv file后，主要引用“Total Models in Category”，"Total Models in Subcategory","Total Models by Publisher in Category","Total Models by Publisher in Subcategory","RecommandationScore"这几项数据，其中处理了"Total Models by Publisher in Subcategory"与"Total Models in Subcategory"的比值得到Publisher与Subcategory之间的关系，
