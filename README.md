
# Dockerized RedisEdge Real-time Video Analytics + Redis Data Source Plugin for Grafana 
Credits: https://github.com/RedisGears/EdgeRealtimeVideoAnalytics

### Description:

RedisEdge from Redis Labs is a purpose-built, multi-model database for the demanding conditions at the Internet of Things (IoT) edge. It can ingest millions of writes per second with <1ms latency and a very small footprint (<5MB), so it easily resides in constrained compute environments. It can run on a variety of edge devices and sensors ranging from ARM32 to x64-based hardware. RedisEdge bundles open source Redis (version 5 with Redis Streams) with the RedisAI and RedisTimeSeries modules, along with RedisGears for inter-module communication.

RedisEdge bundles Open Source Redis + Redis Streams + Redis Modules. 
- Redis Stream is a new data type introduced with Redis 5.0, which models a log data structure in a more abstract way.
- RedisTimeSeries is a Redis Module adding a Time Series data structure to Redis.
- RedisGears is a serverless engine for transaction, batch and event-driven data processing in Redis. It is a dynamic framework for the execution of functions that, in turn, implement data flows in Redis, while (almost) entirely abstracting the data's distribution and choice of deployment (i.e. stand-alone vs. cluster, OSS vs. Enterprise). Functions can be implemented in different languages, including Python and C APIs .
- RedisAI enables you to run an AI inference engine across your Redis database.


An example of using Redis Streams, RedisGears, RedisAI, and RedisTimeSeries for Real-time Video Analytics (i.e. counting people). 




![demo](https://github.com/collabnix/redisedge-grafana/blob/main/images/grafana_demo.png)

## Overview

This project demonstrates a possible deployment of the RedisEdge stack that provides real-time analytics of video streams.

![RediEdge Stack](images/redisedge_components.png)



Also, this conists of Redis Data Source Plugin for Grafana

![Grafana Dashboard](images/grafana_redis.png)


The following diagram depicts the flows between the system's parts.

![System diagram](images/redisedge.png)

The process is a pipeline of operations that go as follows:
1. A video stream producer adds a captured frame to a Redis Stream.
2. The new frame triggers the execution of a RedisGear that:
    1. Downsamples the frame rate of the input stream, if needed.
    2. Prepares the input frame to the model's requirements.
    3. Calls RedisAI to execute an object recognition model on the frame.
    4. Stores the model's outputs (i.e. people counted and their whereabouts inside the frame) in Redis Stream and TimeSeries.
3. A video web server renders the final image based on real-time data from Redis' Streams.



### The RedisEdge Stack

The RedisEdge stack consists of the latest Redis stable release and select RedisLabs modules intended to be used in Edge computing. For more information refer to [RedisEdge](https://github.com/RedisLabs/redis-edge-docker).




### References & Presentations

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/n605eYJV_Y4/0.jpg)](https://www.youtube.com/watch?v=n605eYJV_Y4)


### Quick Demo

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/7o_dvaY4gyU/0.jpg)](https://www.youtube.com/watch?v=7o_dvaY4gyU)



