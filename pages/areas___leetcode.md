- [191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/) #card
  card-last-interval:: 116.07
  card-repeats:: 5
  card-ease-factor:: 3
  card-next-schedule:: 2024-06-03T03:25:34.377Z
  card-last-reviewed:: 2024-02-08T02:25:34.378Z
  card-last-score:: 5
	- reading: [Hamming weight](https://en.wikipedia.org/wiki/Hamming_weight) ,popcount
	- ``` c#
	  public class Solution {
	      //4 bytes (32 bits)
	      public int HammingWeight(uint n) {
	          uint one = 1;
	          int cnt = 0;
	          for(int i=0; i <32; ++i){
	            // or cnt += ((n >> i) & 1
	            if( ((n >> i) & 1) ==1 ){
	                ++ cnt;
	            }
	          }
	          return cnt;
	      }
	  }
	  ```