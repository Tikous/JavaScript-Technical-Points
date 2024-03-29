How to optimize the critical render path?

To complete the first rendering as quickly as possible, we need to minimize the following three variable factors:

(1) The number of key resources.

(2) Critical path length.

(3) The number of key bytes.

Key resources are those that could block the webpage from rendering initially. The fewer such resources, the lesser the workload on the browser, and consequently, the lesser the demand on the CPU and other resources. Similarly, the critical path length is affected by the dependency graph between all key resources and their byte sizes: some resources can only be downloaded after the previous resource has been processed, and the larger the resource, the more round trips required to download. Finally, the fewer critical bytes a browser needs to download, the faster it can process the content and get it on the screen. To reduce the number of bytes, we can reduce the number of resources (remove them or make them non-critical), and compress and optimize each resource to ensure that the transfer size is minimized.
The general steps for optimizing the critical render paths are as follows:

(1) Analyze and describe the characteristics of the critical path: number of resources, bytes count, and length.

(2) Maximally reduce the number of critical resources: eliminate them, delay their download, mark them as asynchronous, etc.

(3) Optimize the key byte number to shorten the download time (round trip).

(4) Optimize the loading sequence of the remaining key resources: It's necessary to download all key assets as early as possible to shorten the length of the critical path.