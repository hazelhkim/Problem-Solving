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

Solution:
```java
class Solution {
    public void duplicateZeros(int[] arr) {
        int possibleDups = 0;
        int length_ = arr.length - 1;

        // Find the number of zeros to be duplicated
        // Stopping when left points beyond the last element in the original array
        // which would be part of the modified array
        for (int left = 0; left <= length_ - possibleDups; left++) {

            // Count the zeros
            if (arr[left] == 0) {

                // Edge case: This zero can't be duplicated. We have no more space,
                // as left is pointing to the last element which could be included  
                if (left == length_ - possibleDups) {
                    // For this zero we just copy it without duplication.
                    arr[length_] = 0;
                    length_ -= 1;
                    break;
                }
                possibleDups++;
            }
        }

        // Start backwards from the last element which would be part of new array.
        int last = length_ - possibleDups;

        // Copy zero twice, and non zero once.
        for (int i = last; i >= 0; i--) {
            if (arr[i] == 0) {
                arr[i + possibleDups] = 0;
                possibleDups--;
                arr[i + possibleDups] = 0;
            } else {
                arr[i + possibleDups] = arr[i];
            }
        }
    }
}
```


