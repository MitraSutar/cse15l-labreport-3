**Bug Chosen**
```
// Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
**Bug With Failing Test**
```
@Test
  public void testReversedBetter() {
    int[] input1 = { 6, 666, 6666666 };
    assertArrayEquals(new int[]{ 6666666, 666, 6}, ArrayExamples.reversed(input1));
  }
```
**Bug With Passing Test**
```
@Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }
```
**Associated Code**
```
javac -cp ".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar" *.java
java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore ArrayTests
```
**Symptom**
![Image](labthree1.png)
**Bug Fixed**
```
// Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```
**Why this works**

testReversed is broken because the newArray is never actually modified, so the method just changes all the values of the initial array to 0. This fix works because newArray is modified to be the actual reversal instead of just sitting there, and newArray is returned as the correct output. 

**grep commands:** all information below found from https://www.geeksforgeeks.org/grep-command-in-unixlinux/#

-c

```
grep -c "insert string here" textFile.txt
```
```
$ grep -c "flight" chapter-1.txt
74
```
```
$ grep -c "potato" chapter-12.txt
0
```

This command checks through all the lines in a text file, and displays the number of lines the input string is present in. It can be used as a worse version of ctrl-f, since it only counts lines and not the total number of times something appears. However, if you only need to know the number of lines something occurs in (for example, if some lines are "contaminated" by a string and you only need to know how many lines were affected), this is very useful. 

-v

```
grep -v "insert string here" textFile.txt
```
```
$ grep -v "e" preface.txt



            PREFACE
                27, 2002).
                accountability.
```
```
$ grep -v " " preface.txt

```

This command checks through all the lines in a text file, and displays the lines the input string is NOT present in. It can be used to weed out strings that contain strings you explicitly want to filter out. It can be used as a form of rudimentary censorship to possibly remove all the references to something but still have a legible output.

-l
```
grep -l "insert string here" *
```
```
$ grep -l "we" *
chapter-1.txt
chapter-10.txt
chapter-11.txt
chapter-12.txt
chapter-13.1.txt
chapter-13.2.txt
chapter-13.3.txt
chapter-13.4.txt
chapter-13.5.txt
chapter-2.txt
chapter-3.txt
chapter-5.txt
chapter-6.txt
chapter-7.txt
chapter-8.txt
chapter-9.txt
preface.txt
```
```
$ grep -l "e" *
chapter-1.txt
chapter-10.txt
chapter-11.txt
chapter-12.txt
chapter-13.1.txt
chapter-13.2.txt
chapter-13.3.txt
chapter-13.4.txt
chapter-13.5.txt
chapter-2.txt
chapter-3.txt
chapter-5.txt
chapter-6.txt
chapter-7.txt
chapter-8.txt
chapter-9.txt
preface.txt
```

This command checks through all the files in the current directory, and displays the text files that the input string is present in. This can be useful as the first stage of a sorting system, scanning entire directories instead of having to use grep on every individual text file to see if the input string is present or not. It can be very convenient to cross out entire text files in a quick way. 

-n
```
grep -n "insert string here" textFile.txt
```
```
$ grep -n "we" preface.txt
12:                the United States. The nation was unprepared. How did this happen, and how can we
14:            To answer these questions, the Congress and the President created the National    
17:            Our mandate was sweeping. The law directed us to investigate "facts and circumstances
22:                areas determined relevant by the Commission. In pursuing our mandate, we have 
23:                reviewed more than 2.5 million pages of documents and interviewed more than 1,200
27:                From the outset, we have been committed to share as much of our investigation as we
28:                can with the American people. To that end, we held 19 days of hearings and took
37:                and equal rights for women. It makes no distinction between military and civilian
42:                fault lines within our government-between foreign and domestic intelligence, and
43:                between and within agencies. We learned of the pervasive problems of managing and
46:            At the outset of our work, we said we were looking backward in order to look forward.
48:                positive-an America that is safer, stronger, and wiser. That September day, we came
51:                the long haul, to attack terrorists and prevent their ranks from swelling while at
54:                agencies that prevailed in the great struggles of the twentieth century must work
55:                together in new ways, so that all the instruments of national power can be combined.
56:                Congress needs dramatic change as well to strengthen oversight and focus      
58:            As we complete our final report, we want to begin by thanking our fellow
62:                of our colleagues, as well as our great affection for them.
70:                officials, past and present, who were generous with their time and provided us with
73:                assistance. We owe a huge debt to their investigative labors, painstaking attention
75:                of several previous Commissions, and we thank the Congressional Joint Inquiry, whose
82:                the importance of the work we have undertaken.
83:            We want to note what we have done, and not done. We have endeavored to provide the
84:                most complete account we can of the events of September 11, what happened and why.
85:                This final report is only a summary of what we have done, citing only a fraction of
86:                the sources we have consulted. But in an event of this scale, touching so many
87:                issues and organizations, we are conscious of our limits. We have not interviewed
99:                number of them. We decided consciously to focus on recommendations we believe to be
102:                pause, reflect, and sometimes change our minds as we studied these problems and
```
```
$ grep -n "Lee" preface.txt
106:            Lee H. Hamilton, vice chair
```

This command checks through all the lines in a text file, then displays the lines the input string is present in AND provides the line numbers of those lines. This is useful as it is a fairly good version of ctrl-f, which unlike grep -c tells you exactly where the input string is present in the text files. This makes it easy to find the input strings in the text files themselves, since all you have to do is go to the line number(s) given.
