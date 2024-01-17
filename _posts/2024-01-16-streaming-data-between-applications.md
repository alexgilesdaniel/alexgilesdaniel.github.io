---
layout: post
author: Alex Daniel
tags: [portfolio sample, software, programming example]
---

One of my proudest accomplishments at National Instruments was developing a multimodal approach to documentation. Prior to my joining on with NI, the LabVIEW documentation contained screenshots of programming examples, but they were few, and the team didn’t have a standardized format for explaining them in detail. In my documentation, I used numbered callouts to describe the flow of data through LabVIEW applications, as seen in the adapted excerpt below.

Read the full topic [here](https://www.ni.com/docs/en-US/bundle/labview/page/streaming-data-between-applications.html). The featured application is one that I developed.

---

## Streaming Data between Applications

The following figure shows an example of using the Network Streams functions to stream data between two applications on different computers.

![Network Streams Programming Example](/assets/images/NS_streaming data.gif)

The following events occur in the previous figure.

1. The Create Network Stream Writer Endpoint function creates a writer endpoint on Computer 1, and the Create Network Stream Reader Endpoint function creates a reader endpoint on Computer 2. 
2. The writer endpoint establishes a connection with the reader endpoint using the endpoint URL of the reader endpoint.
3. Within the Writer Loop, the Write Single Element to Stream function continuously writes the value of the iteration i terminal of the While Loop to the stream. 
4. Within the Reader Loop, the Read Single Element from Stream function continuously reads the stream. 
5. Data streams continuously until the user clicks the Stop button on Computer 1.
6. The Flush Stream function transfers all remaining data to the reader endpoint.
7. The Destroy Stream Endpoint function destroys the writer endpoint.
8. The reader endpoint receives an error due to disconnection, and data flow exits the While Loop.
9. The Destroy Stream Endpoint function destroys the reader endpoint, which destroys the stream.


---
{: data-content="footnotes"}
