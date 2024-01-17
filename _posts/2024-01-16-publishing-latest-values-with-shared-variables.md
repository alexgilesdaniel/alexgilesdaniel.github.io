---
layout: post
author: Alex Daniel
tags: [portfolio sample, software, procedures, revision, networking]
---

Once upon a time, the documentation for LabVIEW’s shared variable API was a mess. User applications weren't behaving as intended, on account of misunderstanding of shared variable technology, and the documentation wasn't helping. Below are excerpts from the content I revised, and further on, you can read some [notes on the writing](#notes-on-the-writing) that explain my changes.

--- 

## Publishing Latest Values with Shared Variables [^1]

A shared variable is a memory space that you can read data from and write data to. You can read and write shared variables on a single computer with single-process shared variables or on multiple computers with network-published shared variables, which publish data over a network using the NI Publish-Subscribe Protocol (NI-PSP). Use shared variables to publish only the latest values in a data set to one or more computers.

In general, you must complete the following tasks to publish latest values with a shared variable:

1. [Create a shared variable.](https://www.ni.com/docs/en-US/bundle/labview/page/creating-shared-variables.html)
2. [Configure the shared variable.](https://www.ni.com/docs/en-US/bundle/labview/page/configuring-shared-variables.html)
3. [Program your applications to read and write the shared variable.](https://www.ni.com/docs/en-US/bundle/labview/page/choosing-a-method-of-reading-and-writing-shared-variables.html)
4. [Make the shared variable available on the network.](https://www.ni.com/docs/en-US/bundle/labview/page/making-shared-variables-available-on-a-network.html)

## Understanding Shared Variable Technology[^2]

Network-published shared variables publish data over a network through a software component called the Shared Variable Engine (SVE). The SVE is installed as a service on your computer when you install LabVIEW, and it manages shared variable updates using a proprietary technology called the NI Publish-Subscribe Protocol (NI-PSP). The term publish-subscribe describes a model of communication where writers, or publishers, do not send data to specific readers, or subscribers. Rather, publishers send updates to a server, in this case the SVE, and subscribers receive those updates from the server.

The following figure uses Shared Variable nodes to demonstrate how the SVE manages shared variable updates with NI-PSP.

![Shared Variable Engine](/assets/images/sveengine.gif)

The following events occur in the previous figure.

1. In Application A, the Random Number (0-1) function writes a random number to the Shared Variable node that corresponds to Variable 1. 
2. The Shared Variable node in Application A sends a request to the SVE to update the value of Variable 1.
3. The SVE approves and sends the new value to the Shared Variable nodes that correspond to Variable 1 in Applications B and C.

In the previous figure, although Computer 1 hosts a writer of Variable 1 in Application A and a reader of Variable 1 in Application B, Application A cannot write a new value directly to Application B. Instead, Application A must send a request to the SVE on Computer 2 to update every application that subscribes to Variable 1. Therefore, the latency involved in these updates makes shared variables ideal for publishing latest values only. To stream data continuously, use network streams.

---

### Notes on the Writing

I made the following key changes to improve this documentation.

* **Revised topic titles to reflect API functionality.** Previously, the topic on shared variable data transfer was called "Sharing Live Data Using Shared Variables." This title implied that shared variables were appropriate for sharing any and all data, but in fact, they were only suited for publishing the latest values in a data set. To appropriately set user expectations, I retitled the topic "Publishing Latest Values with Shared Variables" and made sure to include the last sentence in the first paragraph.
* **Reorganized the table of contents.** Initially, shared variable topics had been thrown under a container called "Networking in LabVIEW," at the same level as topics for other networking protocols. My reorganization has since been reorganized, but I created a parent topic for all networking protocols called [Transferring Data over a Network](transferring-data-over-a-network). Beneath that, [Publishing Shared Latest Values with Shared Variables](https://www.ni.com/docs/en-US/bundle/labview/page/publishing-latest-values-with-shared-variables.html) became a portal for all conceptual and procedural information anyone could need to be successful with shared variables.
* **Illustrated conceptual and procedural information graphically.** With a technology so widely misused, words alone weren't going to cut it. I moved an existing screenshot of an example application to the top of [Reading and Writing Shared Variables Programmatically](https://www.ni.com/docs/en-US/bundle/labview/page/reading-and-writing-shared-variables-programmatically.html) and supplemented it with callouts that described its dataflow. I also created the conceptual graphic in the previous section to describe the behavior and limitations of the shared variable engine.

---
{: data-content="footnotes"}

[^1]: Read the full topic [here](https://www.ni.com/docs/en-US/bundle/labview/page/publishing-latest-values-with-shared-variables.html). It's changed since I wrote it. I intended this topic to be a portal to high-level shared variable tasks, which is why I linked each of the four steps in this topic to essential procedures, but those links have since been removed.
[^2]: Read the full topic [here](https://www.ni.com/docs/en-US/bundle/labview/page/understanding-shared-variable-technology.html).