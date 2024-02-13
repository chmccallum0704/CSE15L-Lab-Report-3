# Lab 3: Bugs and Commands (Week 5)
Caitlin McCallum
## Part 1: Bugs

### Failure Inducing Input

#### i. Junit - ArrayTests.java
```
  @Test 
	public void testReverseInPlace2() {
    int[] input1 = { 3, 2, 1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{1, 2, 3}, input1);
}
```
#### ii. Associated Code - ArrayExamples.java
```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
```
### Successful Input
#### i. Junit - ArrayTests.java
```
@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
 ```
#### ii. Associated Code - ArrayExamples.java
```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
```
### The Symptom

