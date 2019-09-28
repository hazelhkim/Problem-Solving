# Fibonacci

 
<img width="675" alt="Screen Shot 2019-09-28 at 8 12 56 AM" src="https://user-images.githubusercontent.com/46575719/65816296-d7656a00-e1c7-11e9-89e2-8d6b98c0aa2c.png">


#### My Answer:

```java
class Solution {
    public int fib(int N) {
        if(N==0) return 0;
        if(N==1) return 1;
        
        return fib(N-1) + fib(N-2);
    }
}
```

## Other Solutions:

#### Solution 1. Iterative

Time complexity: O(n)
Space complexity: O(1)

```java
class Solution 
{
    public int fib(int N)
    {
        if(N <= 1)
            return N;
        
		int a = 0, b = 1;
		
		while(N-- > 1)
		{
			int sum = a + b;
			a = b;
			b = sum;
		}
        return b;
    }
}
```

#### Solution 2. Recursive

Time complexity: O(2^n) , since T(n) = T(n-1) + T(n-2) is an exponential time
Space complexity: O(n) , space for recursive function call stack

```java
class Solution 
{
    public int fib(int N)
    {
        if(N <= 1)
            return N;
        else
            return fib(N - 1) + fib(N - 2);
    }
}
```

#### Solution 3. Dynamic Programming - Top Down Approach

Time complexity: O(n)
Space complexity: O(n)

```java
class Solution 
{
    int[] fib_cache = new int[31];
	
	public int fib(int N)
    {
        if(N <= 1)
            return N;
        else if(fib_cache[N] != 0)
            return fib_cache[N];
		else 
            return fib_cache[N] = fib(N - 1) + fib(N - 2);
    }
}
```

#### Solution 4. Dynamic Programming - Bottom Up Approach

Time complexity: O(n)
Space complexity: O(n)

```java
class Solution 
{
    public int fib(int N)
    {
        if(N <= 1)
            return N;

		int[] fib_cache = new int[N + 1];
		fib_cache[1] = 1;

		for(int i = 2; i <= N; i++)
		{
			fib_cache[i] = fib_cache[i - 1] + fib_cache[i - 2];
		}
		return fib_cache[N];
    }
}
```

