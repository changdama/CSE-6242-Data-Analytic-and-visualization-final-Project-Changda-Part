# cse6242-Data-Analytic-and-visualization-final-Project-Changda-Part
## A radial tree layout with D3.js visualizes  hierarchy, allowing users to expand or collapse categories. 

## Description
This project outlines the development of an interactive visualization tool built using D3.js, which will allow users to visually explore 3D model metadata and discover connections between various attributes, such as model categories and user interactions (likes, saves, comments). The tool will not only provide stakeholders and model publishers with a clear understanding of what drives model popularity and improves search engine optimization and consequently the performance of their products but also help them adjust their content strategies to better meet market demands. Changda is responsible for radial tree with D3.js visualizes this interaction.

## Installation:


## Method
The overall structure of the visualization includes:  "data import", "data processing", "color mapping", "hierarchical data construction", "legends, nodes, link style processing", and "information display of the pop-up window".

### Dataset Introduction  
The data collection process involved developing a framework to scrape metadata from a 3D model marketplace with dynamic JavaScript content. Nearly 30,000 models were included in this project, presenting challenges in dynamic content rendering and large-scale data management. To overcome these issues, Selenium was employed to interact with JavaScript-rendered elements, while BeautifulSoup parsed static HTML. An SQLite database was used to manage URLs and track scraping progress, preventing redundancy and supporting resumability in case of interruptions。

For data preprocessing, the collected data was cleaned and standardized by removing duplicates and organizing models into hierarchical categories. Sentiment analysis was performed using TextBlob to analyze user comments. The preprocessed data was then exported as a CSV file, making it ready for visualization using D3.js. 

### Data Input
After importing the processed *.csv file, “Total Models in Category”, “Total Models in Subcategory”, “Total Models by Publisher in Category”, “Total Models by Publisher in Subcategory”, and “Recommandation Score” are mainly imported. The ratio of “Total Models by Publisher in Subcategory” to “Total Models in Subcategory” is processed to obtain the relationship between Publisher and Subcategory; the ratio of “TotalModelsinSubcategory” to "TotalModelsinCategory" is processed to obtain the relationship between Category and Subcategory.

### Data Processing
Since the imported data  are inconsistent in terms of their magnitude and value, so they are normalized from small to large to [0-100] to represent the “score”. This method uses the “scaleLinear” in D3.js, so a total of four scores are generated: “the score of  Ratio to ‘Total Models by Publisher in Subcategory’ to ‘Total Models in Subcategory’”, “the score of Ratio to ‘Total Models in Subcategory’ to ‘Total Models in Category ’”, “Total Models in Category score” and “Recommendation Score”.

### Color Mapping
By analyzing the CSV data, it is found that the value of “TotalModelsbyPublisherinSubcategory” is mainly concentrated between 0 and 6, resulting in the score of ratio being distributed in the first half of the range. In order to avoid the visual impact of too much color concentration, a more refined color division was used, dividing the color into 20 gradients from red to blue. With the scaleThreshold method in the D3 library, a segmented threshold scale was created. By setting the threshold breakpoint, the score segments can be accurately mapped to the corresponding color intervals, thereby achieving a matching of scores and colors.

### Hierarchical data construction
First, construct the hierarchical data by iterating through “Category_L0”, “Category_L1”, or “Category_L2” in the csv file. At each level, check whether the current category node exists in “children”. If it does not exist, create a new node and add it to the “children” array. At the same time, update current level to point to   process the next level. If the data record contains publisher information, create a new hierarchical node and assign the relevant information about the publisher from the csv. Finally, add a “ModelName” node at the end of the hierarchy and include the relevant attributes. So, the entire radial tree contains four layers: the first layer: "Category", the second layer: "SubCategory", the third layer: "Model_Publisher", and the final layer “Model_Name”. Next, use "d3.hierarchy" in the D3.js library to convert the data into a tree structure that is usable by D3.js, recursively collapse non-top-level nodes, that is, category and subcategory nodes, implement hierarchical interaction functions in publisher and modelname, and use "d3.tree" in D3.js for visual layout.

### Legend, Nodes, Links style processing
Coloring nodes and links is a more critical step. The colors used are set in the color mapping. The idea is to use the color between root-category according to the “Total Models in Category score”, between category-subcategory based on the “the score of Ratio to 'Total Models in Sub category' to 'Total Models in Category '“; and ‘the score of Ratio to ’Total Models by Publisher in Subcategory‘ to ’Total Models in Subcategory'” is used to color the subcategory-publisher relationship, as well as “Recommendation Score” for the publisher-modelName relationship. During the interaction process, clicking on a node will display the score data for each level, which is used to color the relationship. At the same time, the link is also assigned a corresponding score color range.

### Information Display of the pop-up window
Other information about the node data, such as followers, tags, likes, etc., is displayed in a pop-up window that appears when the mouse hovers over the node.



![Interactive Radial Tree with 20 Color Intervals](https://github.com/user-attachments/assets/14d08f86-c1a8-47f6-aae9-a91e10d113cc)

