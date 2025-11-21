
# EX 2B Jump Game using Greedy Algorithm.
## DATE: 03-09-2025
## AIM:
To write a Java program to for given constraints.
You are given an array of integers. Each number represents the maximum number of steps you can jump forward from that position.

You start from the first element (index 0). 
Write a program to find the minimum number of jumps required to reach the last index of the array.

If it is not possible to reach the end, return -1.
## Algorithm
1. Start  
2. Read the integer `n` (size of the array) and input `n` elements into array `nums`.  
3. If the array is empty, return `-1`. If it has only one element, return `0` (no jumps needed).  
4. Initialize variables:  
   - `jumps = 0` → counts the number of jumps made.  
   - `currentEnd = 0` → the farthest index reachable with the current number of jumps.  
   - `farthest = 0` → the farthest index reachable overall so far.  
5. Loop through the array from index `0` to `nums.length - 2`:  
   - Update `farthest = max(farthest, i + nums[i])`.  
   - If the current index `i` equals `currentEnd`, increment `jumps` and set `currentEnd = farthest`.  
   - If `currentEnd` reaches or exceeds the last index, return `jumps` (we can reach the end).  
   - If `i >= farthest`, return `-1` (cannot move further).  
6. After the loop, if the end is not reached, return `-1`.  
7. Print the minimum number of jumps required to reach the end of the array.  
8. End  
   

## Program:
```
/*
Developed by: Dilip Kumar R
Register Number: 212222040037
*/
import java.util.Scanner;

public class MinJumpToEnd {

    
    public static int minimumJumps(int[] nums) {
        if (nums == null || nums.length == 0) return -1;
        if (nums.length == 1) return 0; 

        int jumps = 0;
        int currentEnd = 0;
        int farthest = 0;

        for (int i = 0; i < nums.length - 1; i++) {
            farthest = Math.max(farthest, i + nums[i]);

          
            if (i == currentEnd) {
                jumps++;
                currentEnd = farthest;

                if (currentEnd >= nums.length - 1) {
                    return jumps; 
                }
            }

            if (i >= farthest) { 
                return -1;
            }
        }

        return -1; 
    }

    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] nums = new int[n];

        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }

        System.out.println("Minimum jumps to reach last index: " + minimumJumps(nums));
    }
}

```

## Output:

<img width="1105" height="445" alt="image" src="https://github.com/user-attachments/assets/9643b55b-9541-4bcd-9ac7-9b4a1b21ceef" />


## Result:
The program successfully implemented and the expected output is verified.
