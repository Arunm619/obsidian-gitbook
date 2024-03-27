
As well as knowing the [memory usage of common Java objects](https://www.javamex.com/tutorials/memory/) such as strings, dates, HashMaps etc, it is sometimes useful to be able to calculate the memory usage of arbitrary objects, given the fields and references they contain. The information given on this page will generally apply to JVMs based on OpenJDK using default parameters and are likely to be typical. It is important to note that strictly speaking, however, they could vary from one JVM to another.

## General formula for calculating memory usage of Java objects

In general, the heap memory used by a Java object in Hotspot consists of:

- an **object header**, consisting of a few bytes of "housekeeping" information;
- memory for **primitive fields**, according to their size (see below);
- memory for **reference fields** (4 bytes each);
- **padding**: potentially a few "wasted" unused bytes after the object data, to make every object start at an address that is a convenient multiple of bytes and reduce the number of bits required to represent a pointer to an object.

### Sizes of primitive types

In case you're not familiar with the byte size of the different Java primitive data types, here is the complete list:

| Java primitive type | Bytes required for Java primitive |
| ---- | ---- |
| boolean | 1 |
| byte | 1 |
| char | 2 |
| short | 2 |
| int | 4 |
| float | 4 |
| long | 8 |
| double | 8 |

You may have expected a boolean to take up a single bit, or an eighth of a byte, especially if an object had 8 boolean fields. In practice, for efficiency, the JVM will allocate a whole byte to each boolean. (This also means that the [space taken up by a boolean array](https://www.javamex.com/tutorials/memory/) will be eight times greater than the theoretical requirement!)

## Object overhead for "housekeeping" information

Instances of an object on the Java heap don't just take up memory for their actual fields. Inevitably, they also require some "housekeeping" information, such as recording an object's class, ID and status flags such as whether the object is currently reachable, currently synchronization-locked etc.

In Hotspot, the following generally holds:

- a normal object requires **12 bytes** of "housekeeping" space (note that this was 8 bytes in earlier JVMs);
- **arrays require 16 bytes** (the same as a normal object, plus 4 bytes for the array length).

## Object size granularity (alignment)

In Hotspot, every object occupies a number of bytes that is a **multiple of 8**. With default settings, if the number of bytes required by an object for its header and fields is not a multiple 8, then you **round up to the next multiple of 8**. In recent JVMs, the so-called **object alignment** is a tunable parameter (because the number of bits of alignment do not need to be specified in address offsets, the alignment also determines the overall size of heap that can be addressed).

The 8-byte object alignment rule in Java means, for example, that:

- a bare Object takes up 16 bytes (12 bytes of housekeeping aligned to the next 8-byte boundaryt);
- an object with one int field (including a boxed Integer) will also take up 16 bytes;
- an object with one long field (including a Java Date) will take up 24 bytes: 12 bytes of header, 8 bytes of data, then 4 bytes of padding to round up to an 8-byte boundary;
- an instance with _eight_ boolean fields will also take up 24 bytes: 12 for the header, 8 for the booleans, plus 4 bytes of padding.

The [table of memory usage of typical Java objects](https://www.javamex.com/tutorials/memory/) presented in our introduction was derived from empirical measurement, and generally reflects the observations above.


----
### Memory usage of some typical Java objects

Given the above observations, the table below gives typical memory usage in bytes for various common types of Java object such as dates and strings:

|Java object type|Memory usage|Observations|
|---|---|---|
|Integer|16 bytes|A boxed int (Integer) will take 16 bytes when object overhead is taken in to account. (This will generally be the minimum amount of memory that any Java object will take up.)|
|Long|24 bytes|Theoretically, a long requires 4 more bytes compared to an int. But because object sizes will typically be aligned to 8 bytes, a boxed Long will generally take up 24 bytes compared to 16 bytes for an Integer.|
|Date|24 bytes||
|java.sql.Date|24 bytes||
|LocalDate|24 bytes||
|LocalDateTime|48 bytes||
|Calendar (=GregorianCalendar)|560 bytes|Beware of storing large numbers of Calendar instances: they are not a compact format for storing dates/times.|
|String (16 chars)|56 bytes|Strings that only contain characters in the single-byte range 0-255 can be stored compactly as one byte per character. (But prior to Java 9, 2 bytes per character will be required.)|
|String (16 chars, Unicode)|104 bytes|Strings that contain characters outside the single-byte range will be stored in Unicode format, generally 2 bytes per character.|
|StringBuilder (100 char capacity)|144 bytes|StringBuilders will start off requiring 1 byte per character of capacity plus overhead, but will be "expanded" to require 2 bytes per character when the first out-of-range character is added.|
|EnumSet|32 bytes|Valid for typical enums with 64 possible values or less; note that you could technically use an 8-byte long to store this information!|
|byte[] with 1024 elements|1040 bytes|The additional 16 bytes are the overhead of storing object housekeeping information and the array length.|
|boolean[] with 1024 elements|1040 bytes|Note how wasteful boolean arrays are because they use 1 byte to store 1 bit of information!|
|BitSet(1024)|168 bytes|A BitSet is a much more memory compact way of storing an array of bits in Java. Note that for a small bit set, there is still a non-negligible overhead (168 bytes compared to the theoretical size of 128 bytes to store 1024 bits).|
|HashMap of 100 ints mapped to ints|~6.75 KB|The object overhead of boxed integers plus the 'bucket' objects internal to HashMap mean that almost ten times as much space is required over the theoretical amount of information stored (200 ints = 800 bytes).|