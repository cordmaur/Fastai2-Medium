# Fastai2-Medium
Repository with the code (notebooks) and data (training patches) for the medium stories covering Fastai 2.

Notebook `01_Create_Datablock.ipynb` has the code for <b>How to create a DataBlock for Multispectral Satellite Image Segmentation with the Fastai-v2 library (part 1)</b> story (https://medium.com/@cordmaur/how-to-create-a-datablock-for-multispectral-satellite-image-segmentation-with-the-fastai-v2-bc5e82f4eb5).
```mermaid

---
title: RTSPY Component Diagram
---
flowchart TD
 subgraph Refinitiv["Refinitiv Server"]
        WS["WebSocket Interface"]
  end
 subgraph Processor["<b>Processor</b>"]
    direction TB
        RC["Read Chunks"]
        AC["Archive Chunks"]
        Z["Zip Scheduler"]
        PM["Process Messages"]
        Fork@{shape: fork}
  end
    RC --> Fork
    R["Redis"]
    Fork --> PM & AC
    WS -- Receive msg chunks --> L["<b>Listener</b>"]
    L -- Authenticate --> WS
    L -- Flush to Redis --> R
    PM -- Save tick data
    (Trade, Bid, Ask) --> R
    R -- Retrieve the chunks --> RC
    AC -- Archive in txt files --> F["File System<br>chunk_YYYY-MM-DD.txt"]
    Z -- Daily scheduler --> F
    Z@{ shape: subproc}
    R@{ shape: cyl}
    F@{ shape: docs}

```

``` mermaid
---
title: RTSPY Component Diagram
---
flowchart TD
 subgraph Refinitiv["Refinitiv Server"]
        WS["WebSocket Interface"]
  end
 subgraph Processor["<b>Processor</b>"]
    direction TB
        RC["Read Chunks"]
        AC["Archive Chunks"]
        Z["Zip Scheduler"]
        PM["Process Messages"]
  end

    RC --> PM
    PM --> AC
    R["Redis"]
    WS -- Receive msg chunks --> L["<b>Listener</b>"]
    L -- Authenticate --> WS
    L -- Flush to Redis --> R
    PM -- Save tick data
    (Trade, Bid, Ask) --> R
    R -- Retrieve the chunks --> RC
    AC -- Archive in txt files --> F["File System<br>chunk_YYYY-MM-DD.txt"]
    Z -- Daily scheduler --> F
    Z@{ shape: subproc}
    R@{ shape: cyl}
    F@{ shape: docs}
```
