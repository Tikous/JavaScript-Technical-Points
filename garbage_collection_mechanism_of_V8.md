V8 implements precise garbage collection (GC), utilising a generational garbage collection mechanism. Therefore, V8 divides the memory (heap) into new generation and old generation.

(1) New generation algorithm

Scavenge GC algorithm is used for objects that typically have a short lifespan in the new generation.

In the new generation space, the memory space is divided into two parts, namely From space and To space. Within these two spaces, one is actively used while the other remains idle. Newly allocated objects are placed into the From space, and when the From space is full, the new generation GC starts. The algorithm checks for objects that are alive in the From space and copies them into the To space, and destroys them if they are dead. When the copy is complete, the From space and To space are exchanged, and the GC is finished.

(2) Old generation algorithm

The objects in the old generation generally live for a long time and have a large number. Two algorithms are used, namely, the marker clearing algorithm and the marker compression algorithm.

Let's talk about when objects appear in the old generation space:

Whether the new generation object has already been through the Scavenge algorithm once, and if so, the object will be moved from the new generation space to the old generation space.

The objects in the To space account for more than 25% of the size. In this case, objects are moved from the new generation space to the old generation space in order not to affect memory allocation.

The space in the old generation is very complex, and there are several Spaces as follows
```javascript
enum AllocationSpace {
  // TODO(v8:7464): Actually map this space's memory as read-only.
  RO_SPACE,    // Invariant object space
  NEW_SPACE,   // New generation space for GC replication algorithms
  OLD_SPACE,   // Old generation resident object space
  CODE_SPACE,  // old code object space
  MAP_SPACE,   // Old map object
  LO_SPACE,    // Old generation large space objects
  NEW_LO_SPACE,  // New generation of large space objects
  FIRST_SPACE = RO_SPACE,
  LAST_SPACE = NEW_LO_SPACE,
  FIRST_GROWABLE_PAGED_SPACE = OLD_SPACE,
  LAST_GROWABLE_PAGED_SPACE = MAP_SPACE
};
```
In the old generation, the tag-clearing algorithm is started first in the following cases:

● When a space is not partitioned

● Description The number of objects in the space exceeds a certain limit

● Space does not guarantee that objects in the new generation will move to the old generation

In this phase, all objects in the heap are traversed, live objects are marked, and when the marking is complete, all unmarked objects are destroyed. When tagging large pairs of memory, it can take several hundred milliseconds to complete a tag. This can lead to some performance issues. To address this issue, in 2011, V8 switched from stop-the-world flags to incremental flags. During incremental markup, GC breaks down the markup work into smaller modules, allowing the JS application logic to execute in between modules for a while, so as not to let the application stall. But in 2018, there was another major breakthrough in GC technology called concurrent markup. This technique allows GC to scan and tag objects while allowing JS to run.

After objects are cleared, the heap memory will be fragmented. When the fragment exceeds a certain limit, the compression algorithm will be started. During compression, live objects are moved to one end until all objects have been moved and then the unwanted memory is cleaned up.

