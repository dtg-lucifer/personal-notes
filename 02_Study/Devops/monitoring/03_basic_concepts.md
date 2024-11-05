### Metrics
>A ***metric*** is a characteristics of a system being measured
>***Syntax*** - `<metric_name>{<label_name>=<label_value>}`

### Label
> A ***Label*** is a key/value pair that defines a certains attribute of a metric

### Types of metrics

1. ***Counter***: Value can only increase or be reset to zero
	***Syntax*** - `https_requests_total{method="GET", status="200"} = 100`
2. ***Guage***: Value can increase / decrease at will
	***Syntax*** - `temperature_celcius{location="office"} = 25.5`
3. ***Histogram***: Sample of observed values over time arranged onto chunks, this exports multiple time series
	1. ***Cumulative counters***
		***Syntax*** - `<basename>_bucket{le="<upper inclusive boud>}`
	2. ***The total count***
		***Syntax*** - `<basename>_sum`
	3. ***The count of observed events:*** 
		***Syntax*** - `<basename>_count`
	
	***Example***:
```
request_duration_seconds_bucket{le="0.1"} = 30
request_duration_seconds_bucket{le="1.0"} = 100
request_duration_seconds_bucket{le="+Inf"} = 150
request_duration_seconds_sum = 15.5
request_duration_seconds_count = 150
```

4. ***Summaries:*** Similar to histogram, but they include quantiles over the time period

### Time series
> A stream of timestamped values
> `{(t1,y1), (t2.y2), ..., (tn,yn)}`
> 
> **t$i$** represents the time of the **$i$th** observation
> **y$i$** represents the value of the time series at the time **t$i$**

### Scraping 
> Scraping is the process of collecting metrics
> ***Instance***: The target you scrape metrics from
> ***Job***: A scrape collection of instances that serve the same purpose

## Components of prometheus

***Server:*** Reponsible for collecting, storing, and querying metrics
***Targets***: Entities that prometheus monitors by scraping metrics from them.
***Exporters:*** export metrics in a way prometheus can understand
***Alertmanager***: handles alert sent bya prometheus
***Storage:*** prometheus uses a local storage solution for storing its metrics