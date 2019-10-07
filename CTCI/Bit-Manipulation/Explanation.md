# Bit Manipulation

- Bit manipulation is used in a variety of problems. 
  - Sometimes, the question explicitly calls for bit manipulation. 
  - Other times, it's simply a useful technique to optimize your code. 
  
- Should be comfortable doing bit manipulation by hand, as well as with code.
  - It's easy to make little mistakes.
  
 ### Bit Manipulation By Hand
 
- The items in the third column can be solved manually or with "tricks" (described below). For simplicity, assume that these are four-bit numbers.
- If you get confused, work them through as a base 10 number. You can then apply the same process to a binary number.
- Remember that ^ indicates an XOR, and ~ is a NOT (negation).
 
  - 0110 + 0010 = 1000 
  - 0011 + 0010 = 0101 
  - 0110 + 0110 = 1100
      - 0110 + 0110 is equivalent to 0110 * 2, which is equivalent to shifting 0110 left by 1.
  - 0110 - 0011 = 0101 
  - 1000 - 0110 = 0010 
  - 0011 * 0101 = 1111 
  - 0011 * 0011 = 1001
  - 0100 * 0011 = 1100 
    - 0100 equals 4, and multiplying by 4 is just left shifting by 2. So we shift 0011 left by 2 to get 1100.
  - 1101 >> 2 = 0011 <br />
  - 1101 ^ 0101 = 1000 <br />
  - 1101 ^ (~1101) = 1111 <br />
    - Think about this operation bit by bit. If you XOR a bit with its own negated value, you will always get 1. Therefore, the solution a^(~a) will be a sequene of 1s. 
  - 1011 & (~0 << 2) = 1000 
    - ~0 is a sequence of 1s, so ~0<<2 is 1s followed by two 0s. ANDing that with another value will clear the last two bits of the value.
  
### Bit Facts and Tricks
  
The following expressions are useful in bit manipulation. Don't just memorize them, though; think deeply about why each of these is true. <br />
( "1s" and "0s" to indicate a sequence of 1s or 0s, respectively.)
  
  - x ^ 0s = x 
  - x ^ 1s = ~x 
  - x ^ x = 0 
  
  - x & 0s = 0 
  - x & 1s = x 
  - x & x = x 
 
  
  - x | 0s = x   
  - x | 1s = 1s 
  - x | x = x 
  
To understand these expressions, recall that these operations occur bit-by-bit, with what's happening on one bit never impacting the other bits. This means that if one of the above statements is true for a single bit, then it's true for a sequence of bits.
  
### Two's Complement and Negative Numbers
  
- Computers typically store integers in two's complement representation.
- A positive number is represented as itself while a negative number is represented as the two's complement of its absolute value (with a 1 in its sign bit to indicate that a negative value).
- The two's complement of an N-bit number (where N is the number of bits used for the number, excluding the sign bit) is the complement of the number with respect to 2^N.
    - Let's look at the 4-bit integer - 3 as an example. If it's a 4-bit number, we have one bit for the sign and three bits for the value. We want the complement with respect to 2^3, which is 8. The complement of 3 (the abso- lute value of - 3) with respect to 8 is 5. 5 in binary is 1131. Therefore, -3 in binary as a 4-bit number is 1101, with the first bit being the sign bit.
      - In other words, the binary representation of -K (negative K) as a N-bit number is concat (1,  2^(N• 1) - K).
      - Another way to look at this is that we invert the bits in the positive representation and then add 1. 3 is 011 in binary. Flip the bits to get 100, add 1 to get 101, then prepend the sign bit (1) to get 1101.

- In a four-bit integer, this would look like the following:

<img width="438" alt="Screen Shot 2019-10-07 at 1 34 42 AM" src="https://user-images.githubusercontent.com/46575719/66287170-a5789580-e8a2-11e9-8a9b-9d57e0656c7f.png">

- Observe that the absolute values of the integers on the left and right always sum to 23, and that the binary values on the left and right sides are identical, other than the sign bit. Why is that?

  
### Arithmetic vs. Local Right Shift
There are two types of right shift operators.
  1) The arithmetic right shift essentially divides by two. 
  2) The logical right shift does what we would visually see as shifting the bits. This is best seen on a negative number.
  
#### A logical shift 
  - In a logical shift, we shift the bits and put a 0 in the most sifgnificant bit. 
  - It is indicated with a >>> operator.
  - On a 8-bit integer (where the sign bit is the most significant bit), this would look like the image below.
  - The sign bit is indicated with a gray background.
 
  <img width="319" alt="Screen Shot 2019-10-07 at 1 36 07 AM" src="https://user-images.githubusercontent.com/46575719/66287221-d789f780-e8a2-11e9-9804-46ddd0348a93.png">
  
  - In an arithmetic right shift, we shift values to the right but fill in the new bits with the value of the sign bit.
This has the effect of (roughly) dividing by two. It is indicated by a >>operator.

<img width="314" alt="Screen Shot 2019-10-07 at 1 36 22 AM" src="https://user-images.githubusercontent.com/46575719/66287230-dfe23280-e8a2-11e9-9031-4fcc72d08d72.png">

```java
int repeatedArithmeticShift(int x, int count) {
  for(int i = 0; i < count; i++) {
    x >>= 1; //Arithmetic shift by 1
  }
  return x;
}

int repeatedLogicalShift(int x, int count) {
  for(int i = 0; i < count; i++) {
    x >>>= 1; // Logical shift by 1
  }
  return x;
}
```
- With the logical shift, we would get e because we are shifting a zero into the most significant bit repeatedly.
- With the arithmetic shift, we would get -1 because we are shifting a one into the most significant bit repeatedly. A sequence of allis in a (signed) integer represents -1.

  
### Common Bit Tasks: Getting and Setting
The following operations are very important to know, but do not simply memorize them.
Memorizing leads to mistakes that are important to recover from. 
Rather, understand how to implement these methods, so that you can implement these, and other, bit problems.
  
#### Get Bit
- This method shifts 1 over by i bits, creating a value that looks like 00010000. 
- By performing an AND with num, we clear all bits other than the bit at bit i. 
- Finally, we compare that to 0. If that new value is not zero, then bit i must have a 1. Otherwise, bit i is a 0.
 
```java
boolean getBit(int num, int i){
  return ((num & (1 << i)) != 0; 
}
```
  
#### Set Bit
- SetBit shifts 1 over by i bits, creating a value like 00010000. 
- By performing an OR with num, only the value a bit i will change.
- All other bits of the mask are zero and will not affect num.
  
```java
int setBit(int num, int i){
  return num | (1<<i);
}
```

#### Clear Bit
- This method operates in almost the reverse of setBit. 
- First, we create a number like 11101111 by creating the reverse of it (00010000) and negating it.
- Then, we perform an AND with num. This will clear the ith bit and leave the remainder unchanged.
```java
int clearBit(int num, int i){
  int mask = ~(1<<i);
  return num & mask;
}
```
To clear all bits from the most significant bit through i (inclusive), 
we create a mask with a 1 at the ith bit (1<<i). Then, we subtract 1 from it, giving us a sequence of 0s followed by i 1s.
We then AND our number with this mask to leave just the last i bits. 
```java
int clearBitsMSBthroughI(int num, int i){
  int mask = (1<<i) -1;
  return num & mask;
}
```
To clear all bits from i through 0 (inclusive), we take a sequence of all 1s (which is -1) and shift it left by i + 1 bits.
This gives us a sequence of 1s (in the most significant bits) followed by i 0bits.
```java
int clearBitsIthrough0(int num, int i){
  int mask = (-1<<(i+1));
  return num & mask;
}
```

#### Update Bit
- To set the ith bit to a value v, we first clear the bit at position i by using a mask that looks like 11101111. 
- Then, we shift the intended value, v, left by i bits. This will create a number with bit i equal to v and all other bits equal to 0.
- Finally, we OR these two numbers, updating the ith bit if v is 1 and leaving it as 0 otherwise.
```java
int updateBit(int num, int i, boolean bitIs1){
  int value = bitIs1 ? 1 : 0;
  int mask = ~(1<<i);
  return (num & mask) | (value<<i);
}

```
  
  
