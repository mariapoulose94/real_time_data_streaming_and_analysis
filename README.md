# Real-time Data Streaming and Analysis

The goal of this project is to develop a  real-time dashboard that captures and visualizes streaming data, and analyses this data for patterns or trends. 

![image](https://github.com/mariapoulose94/real_time_data_streaming_and_analysis/assets/63960112/f39327af-aeb8-40f9-b9b2-adc7cb12c22a)

## Components and Flow of the Project

### Data Producers:

These could be devices, applications, or services generating the streaming data. Examples include IoT devices, social media platforms, web applications, mobile devices, etc. Then, Data from these sources can be pushed to Kinesis Streams.

For this project, we consider Alpha Vantage API as our data producer. 

The Alpha Vantage API offers different types of stock market data, organized into seven categories. Among these, the "Time Series Stock Data APIs" is particularly important for those interested in stock market trends.

The "TIME_SERIES_INTRADAY" part of this API provides detailed stock information that is updated within the day, called intraday data. This means it can give you the stock data not just at the end of each trading day, but also at several points during the day. This data includes:

Open: The price at which the stock started trading at the beginning of the day or a specific time interval within the day.
High: The highest price of the stock during the day or a specific time interval.
Low: The lowest price of the stock during that day or time interval.
Close: The price at which the stock ended trading at the end of the day or time interval.
Volume: The number of shares traded during the day or specific time interval.

The stock symbol we considered is 'IBM'. The rate set is 1 minute.

### Kinesis Data Streams:

This service acts as a buffer and temporary storage mechanism for streaming data. It captures and stores data records in the order they are received.
Data in the stream can be processed in real-time or batch mode. 

We used this service to capture raw data post being fetched from the data producer and after being processed. We used two different Kinesis data streams for these two tasks ('stock_stream_data' and 'stock_sma_stream').

### Lambda:

As data arrives in Kinesis Streams, AWS Lambda can be used to process this data. Lambda functions can filter, transform, aggregate, or enrich the data as needed.
For instance, a Lambda function might analyse a tweet's content for sentiment, extract hashtags, or aggregate metrics like tweet count per minute. 

For this project, we used two lambda functions, one to fetch data from API and push it to a Kinesis data stream, and the other to process the data for visualization purposes and push it to another Kinesis data stream.

The first Lambda function was triggered using EventBridge (triggered at a rate of 1 minute), and the other Lambda fucntion is triggered when the first Kinesis stream starts getting data.

### Elasticsearch:
Elasticsearch is a search and analytics engine that allows for real-time data indexing and querying.Once the data is in Elasticsearch, it can be analysed further, and patterns or trends can be derived. This is particularly useful for large volumes of data where traditional databases might struggle with performance.

### Kibana:
Kibana is a visualisation tool that pairs with Elasticsearch. It allows users to create dashboards that visualise the data stored in Elasticsearch.
For our project, Kibana will serve as the real-time dashboard, showing metrics, graphs, and other visualisations derived from the streaming data.

### Note: 
As of November 2023, OpenSearch is an open-source search engine suite. It's designed for scalability, providing powerful full-text search capabilities and analytics, and is used to develop search applications. OpenSearch is based on Elasticsearch 7.10.2 and Kibana 7.10.2 but has evolved independently since being forked from these versions.

Therefore, we leveraged OpenSearch Service for our project.

You can find the flowchart and the final result i.e. the dashboard attached in this repository.



