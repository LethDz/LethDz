## Hi there 👋

<!--
**DungltAPV/DungltAPV** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile. -->

### I am Dzung :trollface:. Currently, I am a time consumer with no purpose :grin:.
### I am a full-stack engineer :D
[My Linkedin](https://www.linkedin.com/in/lethdz)


----------
2 4 3 1 7 -> 7
 - 2 4
 - 4 3
 - 4 3 1 X
 - 7 == 7 OK

2 4 3 1 2 -> 7
	- 2 4
	- 4 3
	- 4 3 1

2 2 3 1 4 -> 6
	- 2 2
	- 2 2 3
	- 2 3 1
	- 3 1 4
	
2 1 1 1 1 -> 5  
	- 2 1
	- 2 1 1
	- 2 1 1 1  OK
	
2 3 1 2 3 4 -> 7
 - 2 3
 - 2 3 1
 - 2 3 1 2
 - 2 3 1 2 3 ->  3 > 2 -> 3 1 2 3
 - 3 1 2 3 4 -> 4 > 3 -> 1 2 3 4
 - 1 2 3 4 -> 7 > 1 + 2 + 3 + 4 -> 2 3 4
 - 2 3 4 -> 7 > 2 + 3  + 4 -> 3 4


class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int indexStart = 0;
        int indexEnd = 1;
        int accumulator = 0;
        int indexTraverse = 0;
        while (indexTraverse < nums.length) {
            if (accumulator == 0) {
                accumulator += nums[indexStart];
                if (accumulator >= target) {
                    return 1;
                }
                accumulator += nums[indexEnd];
                if (accumulator >= target) {
                    return 2;
                }
                continue;
            }

            int adder = nums[indexTraverse];
            if (adder >= target) {
                return 1;
            }

            int temp = accumulator + adder;
            if (temp >= target && accumulator < target) {
                indexEnd = indexTraverse;
                accumulator = accumulator - nums[indexStart] + adder;
                indexStart++;
            }

            if (accumulator >= target) {
                if (indexTraverse < nums.length - 1) {
                    if ((indexEnd - indexStart + 1) == 2) {
                        indexTraverse++;
                        continue;
                    }

                    indexEnd = indexTraverse;
                    accumulator = temp;
                    indexTraverse++;
                    continue;
                } else {
                    if (indexEnd - indexStart + 1 == nums.length) {
                        return 0;
                    }

                    int temp2 = accumulator - nums[indexStart];
                    if (temp2 >= target) {
                        accumulator = accumulator - nums[indexStart];
                        indexStart++;
                        continue;
                    }
                }
            } 
        }

        return indexStart - indexEnd + 1;
    }
}
