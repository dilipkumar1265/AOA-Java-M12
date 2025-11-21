
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
