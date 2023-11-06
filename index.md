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

**grep commands:** all found from https://www.geeksforgeeks.org/grep-command-in-unixlinux/#

-c

grep -c "insert string here" textFile.txt


