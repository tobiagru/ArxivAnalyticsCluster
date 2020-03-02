# ArxivAnalyticsCluster
Tool to run analytics on top of papers from arXiv. Provides a dashboard to explore connections between papers and topics. The analytics run inside a spark cluster. The papers are enriched with the microsoft academic graph. 

The tool uses the following programming languages and tools:  
Python: pyspark, dash, ...

## Reproducing / Start
To start the analytics tool and the dashboard you will need a spark cluster or a local version of spark running that pyspark can connect to. The entire application is dockerized and starts with the following commands.
On top all the code can as well be used with a jupyter notebook. In this case it is recommended to start the notebook docker. 

### Dashboard Docker
1.) Build the container
>> ``docker build -t aacd -f Dockerfile.Dashboard ./ArxivAnalyticsCluster``  

2.) Run the dashboard
>> ``docker run -d --rm --name aacd -p 8080:8080 <maybe the ports needed to reach your spark cluster> -e CLUSTERIP=<the ip of you spark cluster> -v ./ArxivAnalyticsCluster/src:/dashboard aacd``
--> If you omit the -e CLUSTERIP environment variable it will use the local version of a spark cluster
--> If you womit the -v mapped folder the app will not persist the data and everything is lost once you kill the container.

3.) Go to the dashboard
>> On your browser open the page 127.0.0.1:8080

4.) Stop the container
>> ``docker kill aacd``

### Notebook Docker
This is basically just an extension of the jupyter/pyspark docker.

1.) Build the container
>> ``docker build -t aacn -f Dockerfile.Notebook ./ArxivAnalyticsCluster``

2.) Run the dashboard
>> ``docker run -d --rm --name aacn -p 8888:8888 ./ArxivAnalyticsCluster/src:/src aacn``

3.) Go to the dashboard
>> ``docker logs aacn`` and retrieve url from the output where it says navigate to http://127.0.0.1:8888/***
>> On your browser open the url you retrieved

4.) Stop the container
>> ``docker kill aacn``

## Architecture
-- Dashboard -- 
Plotly Dash - React based tool to build dashboards
-- Analytics --
Python Pyspark
-- Storage --
...
