# Duplicate Zeros

<img width="746" alt="Screen Shot 2019-10-01 at 11 51 49 AM" src="https://user-images.githubusercontent.com/46575719/65978523-dc355280-e441-11e9-82e6-95c7fa8dd126.png">

#### My Answer:
(Not working...)

```java
class Solution {
    public void duplicateZeros(int[] arr) {
       
        LinkedList<Integer> q = new LinkedList<Integer>();

        for(int i = 0; i < arr.length; i++) {
            if(arr[i] == 0) {
                
                q.add(arr[i++]);
                System.out.print(i);
                if(i<arr.length){
                    arr[i] = 0;
                } else {
                    break;
                }
                while(!q.isEmpty()&& i < arr.length){
                    arr[i++] = q.poll();
                }
                        
            } else {
                while(!q.isEmpty()&&i < arr.length){
                    q.add(arr[i]);
                    arr[i++] = q.poll();
                }
                
            }  
        }
    }
}
```

Solution: Two Pointers

```java
    public void duplicateZeros(int[] arr) {
        int countZero = 0;
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == 0) countZero++;
        }
        int len = arr.length + countZero;
        //We just need O(1) space if we scan from back
        //i point to the original array, j point to the new location
        for (int i = arr.length - 1, j = len - 1; i < j; i--, j--) {
            if (arr[i] != 0) {
                if (j < arr.length) arr[j] = arr[i];
            } else {
                if (j < arr.length) arr[j] = arr[i];
                j--;
                if (j < arr.length) arr[j] = arr[i]; //copy twice when hit '0'
            }
        }
    }
```
Another Solution from Discussion: <br />
First, go left to right and count how many shifts (sh) we can fit in our array. <br />
Then, go right to left and move items; if it's zero - duplicate it and decrement the shift.

```java
public void duplicateZeros(int[] a) {
  int i = 0, sh = 0;
  for (i = 0; sh + i < a.length; ++i) sh += a[i] == 0 ? 1 : 0;
  for (i = i - 1; sh > 0; --i) {
    if (i + sh < a.length) a[i + sh] = a[i];
    if (a[i] == 0) a[i + --sh] = a[i];
  }
}
```

