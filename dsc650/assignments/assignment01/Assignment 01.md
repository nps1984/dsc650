---
title: Assignment 1
subtitle: Computer performance, reliability, and scalability calculation
author: Jane Doe
---

## 1.2 

#### a. Data Sizes

| Data Item                                  | Size per Item | 
|--------------------------------------------|--------------:|
| 128 character message.                     |      128 Bytes|
| 1024x768 PNG image                         |       1.5 MB  |
| 1024x768 RAW image                         |        30 MB  | 
| HD (1080p) HEVC Video (15 minutes)         |     4,260 MB  |
| HD (1080p) Uncompressed Video (15 minutes) |   106,200 MB  |
| 4K UHD HEVC Video (15 minutes)             |    15,000 MB  |
| 4k UHD Uncompressed Video (15 minutes)     | 1,215,000 MB  |
| Human Genome (Uncompressed)                |       200 GB  |

### a. Data Sizes Sources
Assuming we are talking about  standard ASCII characters, each character is 1 byte (7 bits with an empty 8th bit).  
This means that a 128 character message is 128 bytes. (https://en.wikipedia.org/wiki/ASCII)

Assuming 16 bits per pixel, with no ancillary chunks and no compression, there are 50,528,256 bits in the    
PNG (1024*768*16) which equates to 6MB 12,582,912M bits /  8 (bytes) / 1024 (kb) / 1024 (mb)  

RAW photo size 30MB (https://www.captureone.com/en/resources/get-started/raw-photo-editing)  
HD Uncompressed (http://aframe.com/blog/2013/05/what-4k-ultra-hd-means-for-video-producers/#:~:text=If%20we%20do%20the%20somewhat,at%20full%20uncompressed%20workprint%20quality.%E2%80%9D)  
 and http://www.fastvideoindexer.com/articles/VideoSizes/VideoSize.htm
4K UHD HEVC Video: Downloaded file from http://jell.yfish.us/. 30 second video at bitrate 140mbps was 500M.  
4K UHD Uncompressed (http://aframe.com/blog/2013/05/what-4k-ultra-hd-means-for-video-producers/#:~:text=If%20we%20do%20the%20somewhat,at%20full%20uncompressed%20workprint%20quality.%E2%80%9D)  
Human Genome (https://medium.com/precision-medicine/how-big-is-the-human-genome-e90caa3409b0)  


#### b. Scaling

|                                           | Size     | # HD | 
|-------------------------------------------|---------:|-----:|
| Daily Twitter Tweets (Uncompressed)       | 60GB     |   3  |
| Daily Twitter Tweets (Snappy Compressed)  | 35GB     |   3  |
| Daily Instagram Photos                    | 107TB    |  33  |
| Daily YouTube Videos                      | 12PB     |3787  |
| Yearly Twitter Tweets (Uncompressed)      | 21TB     |   7  |
| Yearly Twitter Tweets (Snappy Compressed) | 12TB     |   4  |
| Yearly Instagram Photos                   | 38PB     |11674 |
| Yearly YouTube Videos                     | 4EB      |1,258,292|

Tweets Uncompressed: (500,000,000 * 128)/1024/1024/1024  
Tweets Compressed: ((500,000,000 * 128)/1.7)/1024/1024/1024  
For tweets, storage requirements is only 1 HD, but I assume with HDFS and storing 3 copies we are storing them on separate drives    
Instagram Photos: (75,000,000 * 1.5MB)/1024/1024  
Youtube Videos: 24*60*500=720,000 hours of video  
       1 hour of video = 17,040MB  
       (720,000*17,040)/1024/1024/1024=11.4PB

#### c. Reliability
|                                    | # HD | # Failures |
|------------------------------------|-----:|-----------:|
| Twitter Tweets (Uncompressed)      | 7    |    1       |
| Twitter Tweets (Snappy Compressed) | 4    |    1       |
| Instagram Photos                   | 11674|   95       |
| YouTube Videos                     | 1,258,292   | 10,193     |

Using an annualized failure rate of .81

#### d. Latency

|                           | One Way Latency      |
|---------------------------|---------------------:|
| Los Angeles to Amsterdam  | 139 ms                 |
| Low Earth Orbit Satellite | 16 ms                 |
| Geostationary Satellite   | 140 ms                 |
| Earth to the Moon         | 1200 ms                 |
| Earth to Mars             | 20 minutes            | 

https://wondernetwork.com/pings/Los%20Angeles/Amsterdam

https://www.washingtonpost.com/business/why-low-earth-orbit-satellites-are-the-new-space-race/2020/07/10/51ef1ff8-c2bb-11ea-8908-68a2b9eae9e0_story.html

Geostationary: https://en.wikipedia.org/wiki/Satellite_Internet_access#Geostationary_orbits  
Far side of the horizon round trip is about 280, so one way is half, so about 140ms

https://en.wikipedia.org/wiki/Earth%E2%80%93Moon%E2%80%93Earth_communication#:~:text=Echo%20delay%20and%20time%20spread,-Radio%20waves%20propagate&text=Propagation%20time%20to%20the%20Moon,milliseconds%20of%20wave%20travel%20time.

https://www.quora.com/What-is-the-latency-in-communication-from-earth-to-Mars-and-how-could-it-be-improved#:~:text=Short%20answer%20%3A%20it%20depends%20on,at%20the%20speed%20of%20light.