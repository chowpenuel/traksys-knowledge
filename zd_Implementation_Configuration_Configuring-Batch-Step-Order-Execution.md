# Configuring Batch Step Order Execution

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360039430654-Configuring-Batch-Step-Order-Execution*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies to | TrakSYS 10+

### **Summary**

Recipe Step Definitions are configured with a specific Start and End Sequence. The Sequence number is an arbitrary integer that represents the order in which the Recipe Step Definition starts and ends in relation to the other Recipe Step Definitions for the Recipe. This document provides a conceptual overview of batch step execution as well as several examples to illustrate its configuration variations. 

### **Preliminaries**

#### Expected Batch Step Execution

A Batch Step is recorded as expected if the Recipe Step for the Function Definition exists and **both** of the following statements are true:

  1. The current Step’s Start Sequence is less than or equal to the minimum Start Sequence of the Expected Steps that haven’t started.
  2. The current Step’s Start Sequence is less than or equal to the minimum End Sequence of the Expected Steps that haven’t ended.



_Note: The Recipe configuration here is not normal and used specifically to demonstrate the statements presented above._

For the following Recipe:

**Recipe Step** |  **Start**  
**Sequence** |  **End**  
**Sequence** | **FunctionDefName** | **FunctionDefID**  
---|---|---|---|---  
33 | 1 | 1 | A | 13  
34 | 2 | 6 | B | 14  
35 | 3 | 7 | C | 15  
  
The following Batch Step records are created on Job start:

**ID** | **Start Time** | **End Time** |  **Start**  
**Sequence** |  **End**  
**Sequence** | **IsExpected** | **FunctionDefID**  
---|---|---|---|---|---|---  
45 | NULL | NULL | 1 | 1 | 1 | 13  
46 | NULL | NULL | 2 | 6 | 1 | 14  
47 | NULL | NULL | 3 | 7 | 1 | 15  
  
The step execution will be as follows:

_Function Definition "A" runs_

  1. The Batch engine checks for an Expected Record for "A" – **An Expected Step Record Exists**.
  2. The engine then checks the Batch Step Record’s Start Sequence against the other pending Expected Batch Steps. In this case, 1 is less than the 2 (the lowest Start Sequence for Batch Steps with ID 46 and 47).
  3. The engine now checks the Batch Step Record’s Start Sequence against the other un-ended (active or not active) Expected Steps’ End Sequences. In this case, 1 is less than 6 (the lowest End Sequence for Batch Steps 46 and 47), **so the** **Step runs as expected**.



_Function Definition "A" ends_

_Function Definition "B" runs_

  1. The Batch engine checks for an Expected Record for B – **An Expected Step Record Exists**.
  2. The engine then checks the Batch Step Record’s Start Sequence against the other pending Expected Steps’ Start Sequences. In this case, 2 is less than 3 (the lowest start sequence for Batch ID 47).
  3. The engine now checks the Batch Step Record’s Start Sequence against the other un-ended (active or not active) Expected Steps’ End Sequences. In this case, 2 is less than 7, **so the Step runs as expected**.  




_Function Definition "C" runs while "B" is still running_

  1. The Batch engine checks for an Expected Step Record for C – **An Expected Step Record Exists**.
  2. The engine then checks the Batch Step Record’s Start Sequence against the other pending Expected Steps’ Start sequences. In this case, 3 is the only Start Sequence left. Since there is nothing left to compare to, it passes the first condition of expected execution (statement 1 above).
  3. The engine now checks the Batch Step Record’s Start Sequence against the other un-ended (active or not active) Expected Steps’ End Sequences. In this case, 3 is less than 6 (the lowest end sequence for Batch Step ID 46), **so the Step runs as expected**.  




Below is a visualization of the Function Definitions run on the Batch Job. As shown, A executes first, and C begins to execute while B is still running.

![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360052060774)

As each Function Definition starts and ends, the corresponding Batch Step records are updated. The Batch Step records are as follows once the Job ends.

**ID** | **Start Time** | **End Time** |  **Start**  
**Sequence** |  **End**  
**Sequence** | **IsExpected** | **FunctionDefID**  
---|---|---|---|---|---|---  
45 | 08:31:00 | 08:31:25 | 1 | 1 | 1 | 13  
46 | 08:31:30 | 08:31:50 | 2 | 6 | 1 | 14  
47 | 08:31:40 | 08:32:00 | 3 | 7 | 1 | 15  
  
### **Procedure**

The following set of examples are a guide for configuring Recipe execution in a specific manner.

#### Executing Batch Steps Sequentially

The following recipe configuration executes sequentially:

**Recipe Step** |  **Start**  
**Sequence** |  **End**  
**Sequence** | **FunctionDefName** | **FunctionDefID**  
---|---|---|---|---  
36 | 1 | 1 | A | 23  
37 | 2 | 2 | B | 24  
38 | 3 | 3 | C | 25  
39 | 4 | 4 | D | 26  
40 | 5 | 5 | A | 23  
  
In this configuration: 

  * A is a prerequisite for B
  * B is a prerequisite for C (A needs to end first)
  * C is a prerequisite for D (A and B need to end first)
  * D is a prerequisite for A (A, B and C need to end first)
  * A runs twice



The following is an example of a typical expected run of the Batch:

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360054217353)

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
33 | 18 | 08:38:00 | 08:38:25 | 1 | 1 | 23 | 1  
34 | 18 | 08:38:30 | 08:38:55 | 2 | 2 | 24 | 1  
35 | 18 | 08:39:00 | 08:39:25 | 3 | 3 | 25 | 1  
36 | 18 | 08:39:30 | 08:39:55 | 4 | 4 | 26 | 1  
37 | 18 | 08:40:00 | 08:40:25 | 5 | 5 | 23 | 1  
  
The following is an alternate execution of the same recipe configured above. D initially runs unexpectedly at 8:32:11 because its prerequisite, C, needs to end first. From Preliminaries statement 2, D cannot start expectedly because its Start Sequence of 4 is greater than 3, which is the minimum End Sequence of all un-ended steps.

_Note: Blue indicates an Expected Step and Grey indicates an Unexpected Step_

![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360054219273)

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
45 | 19 | 08:31:00 | 08:31:25 | 1 | 1 | 23 | 1  
46 | 19 | 08:31:30 | 08:31:55 | 2 | 2 | 24 | 1  
47 | 19 | 08:32:00 | 08:32:26 | 3 | 3 | 25 | 1  
48 | 19 | 08:32:11 | 08:32:31 | 3 | 3 | 26 | 0  
49 | 19 | 08:32:41 | 08:33:06 | 4 | 4 | 26 | 1  
50 | 19 | 08:33:11 | 08:33:36 | 5 | 5 | 23 | 1  
  
No matter how many times Function Definitions are started/stopped, the Steps will never start expectedly until all prerequisites have ended. In the scenario below, B, C, and D are run 3 times while A is still executing. Since B’s Start Sequence is _**greater than**_ A’s End Sequence, they run unexpectedly.

_Note: Blue indicates an Expected Step and Grey indicates an Unexpected Step_

_![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/360053349574)_

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
56 | 20 | 08:34:11 | 08:35:22 | 1 | 1 | 23 | 1  
57 | 20 | 08:34:11 | 08:34:36 | 1 | 1 | 24 | 0  
58 | 20 | 08:34:11 | 08:34:36 | 1 | 1 | 25 | 0  
59 | 20 | 08:34:11 | 08:34:36 | 1 | 1 | 26 | 0  
60 | 20 | 08:34:41 | 08:35:06 | 1 | 1 | 24 | 0  
61 | 20 | 08:34:41 | 08:35:06 | 1 | 1 | 25 | 0  
62 | 20 | 08:34:41 | 08:35:06 | 1 | 1 | 26 | 0  
63 | 20 | 08:35:11 | 08:35:36 | 1 | 1 | 24 | 0  
64 | 20 | 08:35:11 | 08:35:36 | 1 | 1 | 25 | 0  
65 | 20 | 08:35:11 | 08:35:36 | 1 | 1 | 26 | 0  
66 | 20 | 08:35:41 | 08:36:06 | 2 | 2 | 24 | 1  
67 | 20 | 08:36:11 | 08:36:36 | 3 | 3 | 25 | 1  
68 | 20 | 08:36:41 | 08:37:06 | 4 | 4 | 26 | 1  
69 | 20 | 08:37:11 | 08:37:36 | 5 | 5 | 23 | 1  
  
#### Executing with Independent Prerequisite Steps

**Recipe Step** |  **Start**  
**Sequence** |  **End**  
**Sequence** | **FunctionDefName** | **FunctionDefID**  
---|---|---|---|---  
41 | 1 | 1 | A | 23  
42 | 2 | 2 | B | 24  
43 | 2 | 2 | C | 25  
44 | 3 | 3 | D | 26  
  
In this configuration: 

  * A is a prerequisite for B and C
  * B and C can run independently of each other (A needs to end first)
  * B and C are prerequisites for D (A, B and C need to end first)



This configuration results in B and C running independently because they have the same Start and End Sequences. The following Batch Jobs show different runs that produce the same outcome of only expected steps.

Batch 21

![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/360053370514)

Batch 22

![mceclip4.png](https://portal.parsec-corp.com/hc/article_attachments/360053370554)

Batch 23

![mceclip5.png](https://portal.parsec-corp.com/hc/article_attachments/360054238333)

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
70 | 21 | 08:31:00 | 08:31:25 | 1 | 1 | 23 | 1  
71 | 21 | 08:31:30 | 08:31:55 | 2 | 2 | 24 | 1  
72 | 21 | 08:31:30 | 08:31:55 | 2 | 2 | 25 | 1  
73 | 21 | 08:32:00 | 08:32:25 | 3 | 3 | 26 | 1  
74 | 22 | 08:36:33 | 08:36:58 | 1 | 1 | 23 | 1  
75 | 22 | 08:37:03 | 08:37:28 | 2 | 2 | 24 | 1  
76 | 22 | 08:37:33 | 08:37:58 | 2 | 2 | 25 | 1  
77 | 22 | 08:38:03 | 08:38:28 | 3 | 3 | 26 | 1  
78 | 23 | 08:38:34 | 08:38:59 | 1 | 1 | 23 | 1  
79 | 23 | 08:39:04 | 08:39:29 | 2 | 2 | 25 | 1  
80 | 23 | 08:39:34 | 08:39:59 | 2 | 2 | 24 | 1  
81 | 23 | 08:40:04 | 08:40:29 | 3 | 3 | 26 | 1  
  
In the example below, D is unexpected at 8:33:12 because it fails Preliminaries statement 1 - its Start Sequence is** _greater than_** Step B’s.

_Note: Blue indicates an Expected Step and Grey indicates an Unexpected Step_

_![mceclip6.png](https://portal.parsec-corp.com/hc/article_attachments/360054238733)_

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
82 | 24 | 08:32:31 | 08:32:56 | 1 | 1 | 23 | 1  
83 | 24 | 08:32:57 | 08:33:24 | 2 | 2 | 24 | 1  
84 | 24 | 08:33:12 | 08:33:23 | 2 | 2 | 25 | 0  
85 | 24 | 08:33:29 | 08:33:44 | 2 | 2 | 26 | 1  
86 | 24 | 08:33:49 | 08:34:14 | 3 | 3 | 26 | 1  
  
In the example below, B and C have the same Start and End Sequences, so they can run as expected and independently of each other. They both have A as a prerequisite and are prerequisites for D. D is unexpected because it starts before its prerequisite B has ended (see Preliminaries statement 2).

_Note: Blue indicates an Expected Step and Grey indicates an Unexpected Step_

_![mceclip7.png](https://portal.parsec-corp.com/hc/article_attachments/360054239013)_

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
91 | 25 | 08:34:20 | 08:34:45 | 1 | 1 | 23 | 1  
92 | 25 | 08:34:46 | 08:35:33 | 2 | 2 | 24 | 1  
93 | 25 | 08:35:01 | 08:35:12 | 2 | 2 | 25 | 1  
94 | 25 | 08:35:17 | 08:35:38 | 2 | 2 | 26 | 0  
95 | 25 | NULL | NULL | 3 | 3 | 26 | 1  
  
#### Executing with Prerequisite of a Started Step

**Recipe Step** |  **Start**  
**Sequence** |  **End**  
**Sequence** | **FunctionDefName** | **FunctionDefID**  
---|---|---|---|---  
48 | 1 | 1 | A | 23  
49 | 2 | 4 | B | 24  
50 | 3 | 3 | C | 25  
51 | 5 | 5 | D | 26  
  
In this configuration:

  * A is a prerequisite for B
  * B must start for C to run as expected (A need to end first)
  * B and C are prerequisites for D (A, B and C need to end first)



The above configuration requires B to start before C can run as expected. The following Batch Jobs demonstrate different runs that produce the same outcome of only expected steps.

Batch 26

![mceclip9.png](https://portal.parsec-corp.com/hc/article_attachments/360054239393)

Batch 27

![mceclip10.png](https://portal.parsec-corp.com/hc/article_attachments/360053371574)

Batch 28

![mceclip11.png](https://portal.parsec-corp.com/hc/article_attachments/360054240613)

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
98 | 26 | 08:30:08 | 08:30:33 | 1 | 1 | 23 | 1  
99 | 26 | 08:30:40 | 08:31:07 | 2 | 4 | 24 | 1  
100 | 26 | 08:30:56 | 08:31:12 | 3 | 3 | 25 | 1  
101 | 26 | 08:31:22 | 08:31:47 | 5 | 5 | 26 | 1  
102 | 27 | 08:31:53 | 08:32:18 | 1 | 1 | 23 | 1  
103 | 27 | 08:32:23 | 08:32:48 | 2 | 4 | 24 | 1  
104 | 27 | 08:32:23 | 08:32:48 | 3 | 3 | 25 | 1  
105 | 27 | 08:32:53 | 08:33:18 | 5 | 5 | 26 | 1  
106 | 28 | 08:35:21 | 08:35:46 | 1 | 1 | 23 | 1  
107 | 28 | 08:35:51 | 08:36:16 | 2 | 4 | 24 | 1  
108 | 28 | 08:36:21 | 08:36:46 | 3 | 3 | 25 | 1  
109 | 28 | 08:36:51 | 08:37:16 | 5 | 5 | 26 | 1  
  
The sequence configuration of Recipe Steps is not related to the execution time of Batch Steps. C does not need to end before B just because its sequence values fall in between B’s start and end sequence. D’s prerequisite is essentially that A, B and C, which must all finish before it can start. As seen below, D starts at 8:34:26, and is unexpected because it fails Preliminaries statement 2..

_Note: Blue indicates an Expected Step and Grey indicates an Unexpected Step_

_![mceclip12.png](https://portal.parsec-corp.com/hc/article_attachments/360054240813)_

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
110 | 29 | 08:33:24 | 08:33:49 | 1 | 1 | 23 | 1  
111 | 29 | 08:33:50 | 08:34:21 | 2 | 4 | 24 | 1  
112 | 29 | 08:34:05 | 08:34:41 | 3 | 3 | 25 | 1  
113 | 29 | 08:34:26 | 08:34:41 | 3 | 3 | 26 | 0  
114 | 29 | 08:34:50 | 08:35:15 | 5 | 5 | 26 | 1  
  
#### Executing with Overarching Step

**Recipe Step** |  **Start**  
**Sequence** |  **End**  
**Sequence** | **FunctionDefName** | **FunctionDefID**  
---|---|---|---|---  
55 | 1 | 1 | A | 23  
56 | 2 | 8 | B | 24  
57 | 3 | 3 | C | 25  
58 | 4 | 7 | D | 26  
  
In this configuration:

  * A is a prerequisite for B
  * C’s prerequisite is that B needs to start (and A needs to end)
  * D’s prerequisite is C needs to end and B needs to start (A needs to end)



The Recipe is configured so that D can start as expected while B is still running if C ends. The following Batch Jobs show different runs that produce the same outcome of only expected steps.

Batch 40

![mceclip13.png](https://portal.parsec-corp.com/hc/article_attachments/360054241133)

Batch 41

![mceclip14.png](https://portal.parsec-corp.com/hc/article_attachments/360053372174)

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
121 | 40 | 08:33:08 | 08:33:33 | 1 | 1 | 23 | 1  
122 | 40 | 08:33:34 | 08:34:22 | 2 | 8 | 24 | 1  
123 | 40 | 08:33:46 | 08:34:02 | 3 | 3 | 25 | 1  
124 | 40 | 08:34:07 | 08:34:27 | 4 | 7 | 26 | 1  
125 | 41 | 08:34:33 | 08:34:58 | 1 | 1 | 23 | 1  
126 | 41 | 08:35:03 | 08:35:28 | 2 | 8 | 24 | 1  
127 | 41 | 08:35:33 | 08:35:58 | 3 | 3 | 25 | 1  
128 | 41 | 08:36:03 | 08:36:28 | 4 | 7 | 26 | 1  
  
Even though D’s Sequences fall in between B’s, it will not start as expected until C has finished. As shown below, D’s run is unexpected at 8:32:03 even though it is after B has completed because C still has not ended, failing Preliminaries statement 2.

_Note: Blue indicates an Expected Step and Grey indicates an Unexpected Step_

_![mceclip15.png](https://portal.parsec-corp.com/hc/article_attachments/360054241233)_

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
129 | 42 | 08:31:00 | 08:31:25 | 1 | 1 | 23 | 1  
130 | 42 | 08:31:31 | 08:31:58 | 2 | 8 | 24 | 1  
131 | 42 | 08:31:47 | 08:32:28 | 3 | 3 | 25 | 1  
132 | 42 | 08:32:03 | 08:32:28 | 3 | 3 | 26 | 0  
133 | 42 | 08:32:37 | 08:33:02 | 4 | 7 | 26 | 1  
  
#### Independently Executing Batch Steps

**Recipe Step** |  **Start**  
**Sequence** |  **End**  
**Sequence** | **FunctionDefName** | **FunctionDefID**  
---|---|---|---|---  
59 | 1 | 1 | A | 23  
60 | 1 | 1 | B | 24  
61 | 1 | 1 | C | 25  
62 | 1 | 1 | D | 26  
  
This configuration results in all Function Definitions executing independently of each other, which can result in parallel expected execution. For the following Batch Job, the Function Definitions are started at the same time. The following Batch Jobs are different runs that produce the same outcome of only expected steps.

Batch 42

![mceclip16.png](https://portal.parsec-corp.com/hc/article_attachments/360053372594)

Batch 43

![mceclip18.png](https://portal.parsec-corp.com/hc/article_attachments/360053372654)

Batch 44

![mceclip19.png](https://portal.parsec-corp.com/hc/article_attachments/360054241733)

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
134 | 42 | 08:30:56 | 08:32:00 | 1 | 1 | 23 | 1  
135 | 42 | 08:30:56 | 08:31:28 | 1 | 1 | 24 | 1  
136 | 42 | 08:30:56 | 08:31:44 | 1 | 1 | 25 | 1  
137 | 42 | 08:30:56 | 08:31:12 | 1 | 1 | 26 | 1  
138 | 43 | 08:36:11 | 08:36:36 | 1 | 1 | 23 | 1  
139 | 43 | 08:37:01 | 08:37:26 | 1 | 1 | 24 | 1  
140 | 43 | 08:37:51 | 08:38:16 | 1 | 1 | 25 | 1  
141 | 43 | 08:38:41 | 08:39:06 | 1 | 1 | 26 | 1  
142 | 44 | 08:39:35 | 08:40:00 | 1 | 1 | 23 | 1  
143 | 44 | 08:39:35 | 08:40:00 | 1 | 1 | 24 | 1  
144 | 44 | 08:40:01 | 08:40:25 | 1 | 1 | 25 | 1  
145 | 44 | 08:40:16 | 08:40:33 | 1 | 1 | 26 | 1  
  
This configuration intends for the function definitions to execute only once for the Batch Job. If a Function Definition were to start again, it would be unexpected. In the example below, D is run a second time at 8:34:06, so it is unexpected.

_Note: Blue indicates an Expected Step and Grey indicates an Unexpected Step_

_![mceclip20.png](https://portal.parsec-corp.com/hc/article_attachments/360054241933)_

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
146 | 45 | 08:32:01 | 08:32:26 | 1 | 1 | 26 | 1  
147 | 45 | 08:32:51 | 08:33:16 | 1 | 1 | 24 | 1  
148 | 45 | 08:33:41 | 08:34:31 | 1 | 1 | 25 | 1  
149 | 45 | 08:34:06 | 08:34:56 | 1 | 1 | 26 | 0  
150 | 45 | 08:35:21 | 08:35:46 | 1 | 1 | 23 | 1  
  
**DO NOT DO THIS:** Incorrect Configuration of Sequential Batch Step Execution

**Recipe Step** |  **Start**  
**Sequence** |  **End**  
**Sequence** | **FunctionDefName** | **FunctionDefID**  
---|---|---|---|---  
63 | 1 | 3 | A | 23  
64 | 3 | 5 | B | 24  
65 | 5 | 7 | C | 25  
66 | 7 | 9 | D | 26  
  
For the above configuration:

  * A is a prerequisite Step for C.
  * B is a prerequisite Step for D.
  * A and B can run in the same time interval.
  * C and D can run in the same time interval.
  * B and C can run in the same time interval if A is complete.
  * C and D can run in the same time interval if B is complete.



The general rule is that having a Step’s Start Sequence equal to a prerequisite Step’s End Sequence is usually not the correct configuration, given that it means the Step can start once its prerequisite has also started.

The configuration above can result in multiple outcomes:

Batch 46

![mceclip21.png](https://portal.parsec-corp.com/hc/article_attachments/360054324333)

Batch 47

![mceclip22.png](https://portal.parsec-corp.com/hc/article_attachments/360054324433)

Batch 48

![mceclip23.png](https://portal.parsec-corp.com/hc/article_attachments/360054324493)

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
160 | 46 | 08:30:03 | 08:30:25 | 1 | 2 | 23 | 1  
161 | 46 | 08:30:14 | 08:30:36 | 2 | 3 | 24 | 1  
162 | 46 | 08:30:47 | 08:31:09 | 2 | 4 | 25 | 1  
163 | 46 | 08:30:58 | 08:31:20 | 4 | 5 | 26 | 1  
164 | 47 | 08:33:22 | 08:33:47 | 1 | 2 | 23 | 1  
165 | 47 | 08:33:52 | 08:34:17 | 2 | 3 | 24 | 1  
166 | 47 | 08:34:22 | 08:34:47 | 2 | 4 | 25 | 1  
167 | 47 | 08:34:22 | 08:34:47 | 4 | 5 | 26 | 1  
168 | 48 | 08:34:53 | 08:35:18 | 1 | 2 | 23 | 1  
169 | 48 | 08:35:23 | 08:35:48 | 2 | 3 | 24 | 1  
170 | 48 | 08:35:53 | 08:36:18 | 2 | 4 | 25 | 1  
171 | 48 | 08:36:23 | 08:36:48 | 4 | 5 | 26 | 1  
  
At first glance, it appears from the configuration that B needs to complete before C can start:

_Note: Blue indicates an Expected Step and Grey indicates an Unexpected Step_

_![mceclip24.png](https://portal.parsec-corp.com/hc/article_attachments/360054327933)_

However, the following is what actually happens:

![mceclip25.png](https://portal.parsec-corp.com/hc/article_attachments/360054328113)

Below is the same recipe, but A completes before B starts, allowing B and C to run over the same time interval. This is possible because the End Sequence of B and the Start Sequence of C are equal, passing Preliminaries statement 2. As shown, D will start unexpectedly because its prerequisite B is still running.

![mceclip26.png](https://portal.parsec-corp.com/hc/article_attachments/360053466934)

**Batch Step** | **Batch ID** | **Start Time** | **End Time** | **Start Sequence** | **End Sequence** | **FunctionDefID** | **IsExpected**  
---|---|---|---|---|---|---|---  
171 | 49 | 08:31:25 | 08:31:50 | 1 | 2 | 23 | 1  
172 | 49 | 08:31:51 | 08:32:19 | 2 | 3 | 24 | 1  
173 | 49 | 08:32:02 | 08:32:30 | 2 | 4 | 25 | 1  
174 | 49 | 08:32:08 | 08:32:41 | 2 | 2 | 26 | 0  
175 | 49 | 08:32:51 | 08:33:16 | 4 | 5 | 26 | 1
