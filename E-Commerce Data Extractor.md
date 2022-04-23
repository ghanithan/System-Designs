# E-commerce Data extractor

## The requirement is to create a web data extractor for e-commerce websites based on the basic product descriptions.

The customer who is essentially a reseller/dealer would provide us with the basic details of the product which is available with them. We must crawl the web and scrap the data from the manufacturer websites and provide them the description that would intern be used in the E-commerce website.

Components:

1.  Web crawler - Phase - 1 - Business logic

2.  Website scrapper - Phase - 1 - Business logic

3.  DB to store the scrapped data - Phase - 1 - Database

4.  Frontend - Phase 1 - UI/UX

5.  Backend - Phase 1 - UI/UX

6.  Analyse the data and provide an insightful description for the product (using NLP and ML) - Phase - 2 


![Image](https://ghanithan.com/System-Designs/E-commerse%20data%20extractor.drawio.svg)


### Web Crawler:
This must be a fast and lightweight web crawler which takes into account the 'Robot.txt' and the rate-limiters into account and crawls the web preferably the Top 5 search results of the keywords or the particular manufacturer site.
	It is expected to crawl to the depth of each link and built a build a tree which looks like the sitemap of the website and their inter-connectivities. We shall call this site-tree
	We shall plan to implement this in GO with concurrency in mind.
	

### Website Scrapper:
This module must scrap the data from the webpages that are in the tree built by the web crawler. The scrapping must happen based on the HTML tags and their DOM hierarchy and collect the data in JSON format. We are essentially extracting the DOM elements into JSON preserving their hierarchy and collecting alt attributes from image tags. This data would then be sent to a document DB.

### DB to store the scrapped data:
We would require a document DB such as **Apache Cassandra** to store the scrapped JSON data along with the site-tree.
	The document DB is chosen because the data structure can be dynamic in the sense that the data need not be saved in fixed row-column format of traditional RDBMS. The advantage of using Apache Cassandra is that it is a multi-master distributed DB with high reliability and more importantly it is open source and requires no license to set up.

### Frontend:
A frontend is required to enter the basic keywords provided by the customer and also to show the result from the DB.
	We shall use a reactive frontend based on Svelte. We are not going to use Server Side rendering, rather we shall follow the JAMstack method, where the front end will be a reactive template and data is filled in them by using API calls to the backend.

### Backend:
Backend is required to handled authentication & authorisation and also maintain the user sessions and fetch & render the data from DB when an API call is made by the Frontend. This shall be written using Fibre framework in GO and a **Redis** database to maintain the user sessions. The user details shall be saved in the Mongo DB.

### Analyse the data and provide an insightful description for the product (using NLP and ML) :
This shall be handled in the phase 2. Current choice of NLP shall be RASA but we need to evaluate other options too.
