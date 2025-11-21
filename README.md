
# EX 2A Assign Cookies using Greedy Algorithm. 
## DATE: 01-09-2025
## AIM:
To Write a Java program for the following Constraints.
Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.

Each child i has a greed factor g[i], which is the minimum size of a cookie that the child will be content with; and each cookie j has a size s[j]. If s[j] >= g[i], we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximise the number of your content children and output the maximum number.

## Algorithm
1. Start  
2. Read the number of children `n` and input their greed factors into array `g`.  
3. Read the number of cookies `m` and input their sizes into array `s`.  
4. Sort both arrays `g` (children’s greed) and `s` (cookie sizes) in ascending order.  
5. Initialize three variables:  
   - `i = 0` → pointer for children  
   - `j = 0` → pointer for cookies  
   - `count = 0` → to count satisfied children  
6. While both `i < g.length` and `j < s.length`:  
   - If `s[j] >= g[i]`, assign the cookie to the child: increment both `i` and `j`, and increment `count`.  
   - Else, increment `j` to check the next cookie.  
7. When the loop ends, `count` holds the maximum number of satisfied children.  
8. Print the value of `count`.  
9. End  
   

## Program:
```
/*
Developed by: Dilip Kumar R
Register Number:  212222040037
*/

import java.util.*;

public class AssignCookies {

    public static int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        
        int i = 0;
        int j = 0;
        int count = 0;
        
        while (i < g.length && j < s.length) {
            if (s[j] >= g[i]) {
                count++;
                i++;
                j++;
            } else {
                j++;
            }
        }
        
        return count;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] g = new int[n];
        for (int i = 0; i < n; i++) g[i] = sc.nextInt();
        
        int m = sc.nextInt();
        int[] s = new int[m];
        for (int i = 0; i < m; i++) s[i] = sc.nextInt();
        
        System.out.println(findContentChildren(g, s));
    }
}

```

## Output:

<img width="649" height="469" alt="image" src="https://github.com/user-attachments/assets/7c99b307-ae12-415e-b466-f1d82522c440" />


## Result:
The program successfully implemented and the expected output is verified.. 



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



# EX 2C Job Sequencing using Greedy Approach
## DATE : 05-09-2025
## AIM:
To write a Java program to for given constraints.
Given an integer array nums and an integer k, return the number of pairs (i, j) where i < j such that |nums[i] - nums[j]| == k.

The value of |x| is defined as:

x if x >= 0.
-x if x < 0.You're given N jobs, each with:

A unique jobId

A deadline (by which it must be completed)

A profit (earned only if completed on or before the deadline)

Each job:

Takes exactly 1 unit of time

Only one job can be done at a time

Your goal is to maximize total profit while completing the maximum number of jobs possible within their deadlines.

## Algorithm
1. Start  
2. Read the integer `n` (number of jobs).  
3. For each job, input three values — `id`, `deadline`, and `profit` — and store them in an array of `Job` objects.  
4. Sort the jobs in **descending order of profit** using a custom comparator.  
5. Find the maximum deadline among all jobs to determine the total number of available time slots.  
6. Create a boolean array `slot[]` of size `maxDeadline + 1` to track which time slots are filled.  
7. Initialize `totalProfit = 0` and `countJobs = 0`.  
8. For each job in the sorted list:  
   - Check from its deadline down to 1 to find a free slot.  
   - If a free slot is found, mark it as occupied (`slot[j] = true`).  
   - Add the job’s profit to `totalProfit` and increment `countJobs`.  
9. After scheduling all possible jobs, return the total number of jobs done (`countJobs`) and the total profit (`totalProfit`).  
10. Print both values.  
11. End  
  

## Program:
```
/*
Developed by: Dilip Kumar R
Register Number:  212222040037
*/
import java.util.*;

public class JobScheduling {

    static class Job {
        int id, deadline, profit;

        Job(int id, int deadline, int profit) {
            this.id = id;
            this.deadline = deadline;
            this.profit = profit;
        }
    }

    public static int[] jobScheduling(Job[] jobs, int n) {
        Arrays.sort(jobs, (a, b) -> b.profit - a.profit);

        int maxDeadline = 0;
        for (Job job : jobs) {
            maxDeadline = Math.max(maxDeadline, job.deadline);
        }

        boolean[] slot = new boolean[maxDeadline + 1];
        int totalProfit = 0;
        int countJobs = 0;

        for (Job job : jobs) {
            for (int j = job.deadline; j > 0; j--) {
                if (!slot[j]) {
                    slot[j] = true;
                    totalProfit += job.profit;
                    countJobs++;
                    break;
                }
            }
        }

        return new int[]{countJobs, totalProfit};
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        Job[] jobs = new Job[n];

        for (int i = 0; i < n; i++) {
            int id = sc.nextInt();
            int deadline = sc.nextInt();
            int profit = sc.nextInt();
            jobs[i] = new Job(id, deadline, profit);
        }

        int[] result = jobScheduling(jobs, n);
        System.out.println(result[0] + " " + result[1]);
    }
}

```

## Output:

<img width="821" height="551" alt="image" src="https://github.com/user-attachments/assets/e59960d0-7182-4f2a-bead-6f588a1329ba" />


## Result:
The program successfully implemented and the expected output is verified.


# EX 2D Pattern Matching using Naive Approach.
## DATE : 07-09-2025

## AIM:
To write a Java program to for given constraints.
Given text string with length n and a pattern with length m, the task is to prints all occurrences of pattern in text.
Note: You may assume that n > m.

Examples: 

Input:  text = "THIS IS A TEST TEXT", pattern = "TEST"
Output: Pattern found at index 10

Input:  text =  "AABAACAADAABAABA", pattern = "AABA"
Output: Pattern found at index 0, Pattern found at index 9, Pattern found at index 12
## Algorithm
1. Start  
2. Read the input string `text` and the `pattern` to be searched.  
3. Find the lengths of both strings:  
   - `n = length of text`  
   - `m = length of pattern`  
4. Loop through the text from index `i = 0` to `i <= n - m`:  
   - For each position `i`, compare every character of the pattern with the corresponding character in the text.  
   - If any character does not match, break out of the inner loop.  
5. If all characters of the pattern match (`j == m`), print the index `i` where the pattern starts in the text.  
6. Continue checking until the end of the text.  
7. End  
 

## Program:
```
/*
Developed by: Dilip Kumar R
Register Number:  212222040037
*/
import java.util.Scanner;

public class NaivePatternSearch {

    public static void search(String text, String pattern) {
        int n = text.length();
        int m = pattern.length();

        for (int i = 0; i <= n - m; i++) {
            int j;
            for (j = 0; j < m; j++) {
                if (text.charAt(i + j) != pattern.charAt(j)) {
                    break;
                }
            }
            if (j == m) {
                System.out.println("Pattern found at index " + i);
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        //System.out.print("Enter the text: ");
        String text = scanner.nextLine();

        //System.out.print("Enter the pattern: ");
        String pattern = scanner.nextLine();

        search(text, pattern);

        scanner.close();
    }
}

```

## Output:

<img width="1042" height="411" alt="image" src="https://github.com/user-attachments/assets/4fbde6a2-3110-4802-8d7e-116d13020d3d" />


## Result:
The program successfully implemented and the expected output is verified.



# EX 2E Pattern Matching using Manacher's Algorithm.
## DATE : 11-09-2025

## AIM:
To write a Java program for the following constraints.
Longest Palindromic Substring
Given a string s, return the longest palindromic substring in s.
using Manacher's Algorithm

## Algorithm
1. Start  
2. Read the input string `s`.  
3. If the string is empty, return an empty result.  
4. Preprocess the string by inserting a special character (e.g., `#`) between each letter and at both ends to handle even-length palindromes uniformly.  
   - Example: `"abba"` → `"#a#b#b#a#"`  
5. Initialize variables:  
   - `p[]` → array to store palindrome radii centered at each position  
   - `center = 0` and `right = 0` → current center and right boundary of the known palindrome  
   - `maxLen = 0` and `centerIndex = 0` → track longest palindrome found so far  
6. For each position `i` in the processed string:  
   - Find the mirror position: `mirror = 2 * center - i`  
   - If `i < right`, set `p[i] = min(right - i, p[mirror])`.  
   - Expand around `i` while characters on both sides match (`t[a] == t[b]`).  
   - Update `p[i]` for every successful expansion.  
7. If `i + p[i] > right`, update `center = i` and `right = i + p[i]`.  
8. If `p[i] > maxLen`, update `maxLen` and `centerIndex`.  
9. Compute the starting index of the palindrome in the original string:  
   - `start = (centerIndex - maxLen) / 2`  
10. Extract and return the substring from `start` to `start + maxLen`.  
11. Print the longest palindromic substring.  
12. End  


## Program:
```
/*
Developed by: Dilip Kumar R
Register Number: 212222040037
*/
import java.util.Scanner;

public class LongestPalindromeManacher {

    public static String longestPalindrome(String s) {
        if (s == null || s.length() == 0) return "";

        StringBuilder t = new StringBuilder();
        t.append('#');
        for (int i = 0; i < s.length(); i++) {
            t.append(s.charAt(i));
            t.append('#');
        }

        int n = t.length();
        int[] p = new int[n];
        int center = 0, right = 0;
        int maxLen = 0, centerIndex = 0;

        for (int i = 0; i < n; i++) {
            int mirror = 2 * center - i;
            if (i < right) {
                p[i] = Math.min(right - i, p[mirror]);
            }

            int a = i + (1 + p[i]);
            int b = i - (1 + p[i]);
            while (a < n && b >= 0 && t.charAt(a) == t.charAt(b)) {
                p[i]++;
                a++;
                b--;
            }

            if (i + p[i] > right) {
                center = i;
                right = i + p[i];
            }

            if (p[i] > maxLen) {
                maxLen = p[i];
                centerIndex = i;
            }
        }

        int start = (centerIndex - maxLen) / 2;
        return s.substring(start, start + maxLen);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String input = sc.nextLine();
        String result = longestPalindrome(input);
        System.out.println("Longest Palindromic Substring: " + result);
        sc.close();
    }
}

```

## Output:

<img width="1266" height="391" alt="image" src="https://github.com/user-attachments/assets/c9ecddb8-7f68-427c-b22f-0149833458aa" />


## Result:
The program successfully implemented and the expected output is verified.
