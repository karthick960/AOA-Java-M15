
# EX 5A 0/1 Knapsack Problem - Branch&Bound 
## DATE:7/11/2025
## AIM:
To Write a Java program to solve 0/1 Knapsack problem using Branch and Bound Approach.
You are heading a college entrepreneurship cell that can invest in up to N student‑startups.

For each startup i you know: cost[i]  — the amount (in ₹ lakh) required to join the showcase profit[i] — the estimated profit (in ₹ lakh) you’ll gain if it succeeds You have a total budget of B ₹ lakh. Pick a subset of startups so that the sum of costs ≤ B and the sum of profits is maximised.

Because N can be as large as 50, a plain exhaustive search (2^N) is too slow.

The recommended approach is Branch & Bound with a fractional‑knapsack upper bound (but any algorithm that meets the constraints is accepted). 

Input Format

N

B

cost[1] cost[2] … cost[N]

profit[1] profit[2] … profit[N]

1 ≤ N ≤ 50

1 ≤ B ≤ 1 000 000

1 ≤ cost[i], profit[i] ≤ 10 000 

Output Format

maxProfit

For example:




## Algorithm
1.Sort items in decreasing order of profit-to-cost ratio to maximize pruning efficiency.
2.Use a recursive DFS that tries two choices for each item: include it or exclude it.
3.Track the current cost and profit; if cost exceeds the budget, stop exploring that branch.
4.Compute an upper bound using fractional knapsack; if the bound ≤ current best, prune the branch.
5.Explore remaining promising branches and update the global best profit whenever a better solution is found.   

## Program:
```
/*
Knapsack Problem - Branch&Bound 
Developed by: Karthick k
Register Number:212222040070
*/
import java.util.*;

public class StartupShowcaseOptimizer {

    static int N, B;
    static int[] c, p;
    static int best = 0;

    static double bound(int idx, int cw, int cv) {
        if (cw > B) return 0;
        double ub = cv;
        int rem = B - cw;
        for (int i = idx; i < N; i++) {
            if (c[i] <= rem) {
                rem -= c[i];
                ub += p[i];
            } else {
                ub += (double) p[i] * rem / c[i];
                break;
            }
        }
        return ub;
    }

    static void dfs(int idx, int cw, int cv) {
        if (cw > B) return;
        if (idx == N) {
            if (cv > best) best = cv;
            return;
        }
        if (bound(idx, cw, cv) <= best) return;
        dfs(idx + 1, cw + c[idx], cv + p[idx]);
        dfs(idx + 1, cw, cv);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();
        B = sc.nextInt();
        int[] cost = new int[N];
        int[] prof = new int[N];
        for (int i = 0; i < N; i++) cost[i] = sc.nextInt();
        for (int i = 0; i < N; i++) prof[i] = sc.nextInt();
        sc.close();

        Integer[] idx = new Integer[N];
        Arrays.setAll(idx, i -> i);
        Arrays.sort(idx, Comparator.comparingDouble(i -> -(double) prof[i] / cost[i]));

        c = new int[N];
        p = new int[N];
        for (int i = 0; i < N; i++) {
            c[i] = cost[idx[i]];
            p[i] = prof[idx[i]];
        }

        dfs(0, 0, 0);
        System.out.println(best);
    }
}

```

## Output:
<img width="846" height="260" alt="image" src="https://github.com/user-attachments/assets/60110d9f-5133-4627-a397-9edceccd3e82" />



## Result:
The program successfully solved 0/1 Knapsack problem using branch & bound and output is verified. 
