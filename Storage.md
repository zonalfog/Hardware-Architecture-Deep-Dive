# Storage Technical Deep Dive: SSDs, HDDs & NVMe Technology



This document explores the evolution of permanent data storage, focusing on the architectural shift from mechanical platters to high-speed Flash memory and the protocols that drive them.



---



## 1. Performance Metrics: Throughput vs. IOPS



To understand storage speed, we must look at two different types of performance:



*   **Sequential Speed (MB/s):** How fast large, continuous files (like videos) are moved.

*   **IOPS (Input/Output Operations Per Second):** How many tiny, individual data requests the drive can handle per second. This dictates system responsiveness.

&#x20;   *   **HDD:** ~80–120 IOPS (limited by physical head movement).

&#x20;   *   **SATA SSD:** ~100,000 IOPS.

&#x20;   *   **NVMe SSD:** 1,500,000+ IOPS.

*   **Impact:** High IOPS are why an OS boots in seconds on an SSD while taking minutes on an HDD.



---



## 2. Hard Disk Drives (HDD): Mechanical Precision



*   **HDD Capacity:** Ideal for mass storage (up to 20TB+).

*   **HDD Speed (RPM):** Common speeds are **5400 RPM** and **7200 RPM**. Higher RPM reduces the "seek time" for the read/write head.

*   **HDD Cache:** A small DRAM buffer (64MB–512MB) that smooths out data bursts.



---



## 3. Solid State Drives (SSD): The "Brain" and Durability



Unlike HDDs, SSDs are managed by a dedicated processor called the **Controller**.



*   **The Controller:** Handles **Wear Leveling** (distributing data evenly to prevent cell death) and **Garbage Collection** (cleaning up deleted blocks to maintain speed).

*   **Durability (TBW - Terabytes Written):** Flash cells wear out over time. TBW indicates the total amount of data you can write before the drive becomes unreliable. 

*   **Cell Types (SLC, MLC, TLC, QLC):** Lower bit-per-cell counts (like SLC) offer much higher TBW and speed but at a higher cost.



---



## 4. Storage Protocols: NVMe vs. SATA (AHCI)



*   **SATA (AHCI):** Designed for HDDs. Limited to a single command queue of **32 commands**. Max speed capped at \~560 MB/s.

*   **NVMe (PCIe):** Designed for Flash. Supports **65,536 queues\*\*, each with **65,536 commands**. This architecture is the foundation for high IOPS and parallel processing.



---



## 5. DirectStorage: The Bridge to the GPU



DirectStorage connects `Storage.md`, `Motherboard.md`, and `GPU.md`.

*   **The Path:** Data bypasses the CPU and flows directly from the **NVMe SSD to the GPU**.

*   **Result:** The GPU uses its parallel cores for decompression, enabling instant load times and more detailed open-world environments.



---



## 6. Technical Interaction (Summary)

**HDDs** provide bulk **Capacity** but are limited by mechanical **IOPS**. **SSDs** use a **Controller** to manage high-speed NAND Flash. The **NVMe protocol** unlocks the true potential of this flash via PCIe, while **TBW** defines the drive's lifespan. Finally, **DirectStorage** allows the **GPU** to harness this speed directly, removing the CPU from the data-loading bottleneck.



