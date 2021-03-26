---
title: "Java 12 is here!"
permalink: /2019/03/java-12-is-here.html
published: true
---

Java has switched to a 6-month release cycle, which means you don't have to wait 3 years for a major Java upgrade. It also means less and manageable changes in each major release. Java 12 has been released recently. Here is a brief overview of new features.

### Switch Expressions
We all use switch statements, and we know how much it simplifies coding. But still, it required having a break statement after every case expression. As a guy who makes a lot of careless mitsakes, missing break statement after a case is one of the mistakes I make a lot.

```java
switch(month) {
   case 1 : 
      monthStr = "January";
      break;
   case 2 : 
      monthStr = "February";
      break;
   case 3 : 
      monthStr = "March";
      break;
   case 4 : 
      monthStr = "April";
      break;
}
```

Now with [switch expressions](http://openjdk.java.net/jeps/325), the switch block is going to look much cleaner and robust.
```java
String monthStr = switch(month) {
   case 1 -> "January";
   case 2 -> "February";
   case 3 -> "March";
   case 4 -> "April";
}
```

### Shenandoah Garbage Collector
Java's GC (Garbage Collector) is responsible for removing unused objects from memory. Java does this by pausing the application for a while, which is not desirable by real-time applications. With the [Shenandoah algorithm](http://openjdk.java.net/jeps/189), pause times are significantly reduced. This is still an experimental feature which means you have to enable it manually for it to work.

GC is one of the most debated features in Java since it is known to affect the performance of the application unpredictably. It is good to know that Java is putting in more effort to solve these issues. Java 11 which was released in last September had introduced ZGC, a low-latency GC.

### Improvements to G1 GC
G1 GC was introduced in Java 7. In Java 12, G1 GC comes with minor improvements. 

[Abortable Mixed Collections](http://openjdk.java.net/jeps/344) aims to prevent long pause time during garbage collection. It does this by carrying out GC process incrementally so that it can be aborted when pause time exceeds the target time.

[Promptly Return Unused Committed Memory from G1](http://openjdk.java.net/jeps/346) aims to return unused heap memory to the operating system. G1 GC periodically analyzes how much heap memory is used by the application and returns the rest to the OS.
