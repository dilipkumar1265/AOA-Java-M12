
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
