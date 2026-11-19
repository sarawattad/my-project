Degree level: Bachelor’s

# Project proposal

## 1. The problem and goal

**The problem and goal in my project:**

A processor cache holds a small number of memory blocks. When the requested block is absent, the processor has to fetch it from a slower level of memory. If the cache is full, a replacement rule chooses which block to remove. I want to study a case where this choice is difficult: a program repeatedly reads a few blocks, scans a long list once, then returns to those first blocks. The scan can push all of them out.

I will compare my rules with Least Recently Used (LRU), which removes the block whose last access was furthest in the past. My measure will be the percentage of accesses that miss the cache. Each rule will start with an empty cache of the same capacity and process the same accesses in order. A rule can use only information available at the time of the decision.

## 2. The simulator

**The simulator in my project:**

I plan to build a small Python simulator that can run on my laptop. It will read a JSON file containing the capacity in blocks, a sequence of requested block IDs, and the replacement rule to test. For each access, it will record whether the block was present and which block, if any, it removed. It will report the hit count, miss count, and miss percentage. Before testing new rules, I will compare its output with a short sequence I can trace by hand.

## 3. The agent's role

**The agent in my project:**

The language-model agent will review the simulator’s log after a run and propose one change to the replacement rule. For example, if a scan pushes out blocks that are needed again soon afterward, the agent might suggest evicting a block seen only once before evicting one used repeatedly. It will rerun the same workload and check whether the change reduced misses. The cache capacity and input sequence will stay fixed during each comparison.

A simple program can test a list of predefined rules and select the best one. What I want to test is whether an agent can use a specific pattern of misses to propose a useful rule beyond that list. My open question is whether the proposed rule still performs well on new access sequences that the agent did not see while developing it.

## Explain your project to someone outside your field

**My project in simple words:**

Imagine working at a small desk with room for only a few books. You use two reference books throughout the day, but then you briefly consult a stack of other books. By the time you finish, both reference books are back on the shelf, and you have to fetch them again.

My simulator will replay a list of book requests and count the trips to the shelf under different rules for clearing the desk. An AI assistant will look at which decisions led to extra trips and suggest a different rule. I will test its suggestion on a fresh list to see whether it helps even when the order of requests changes.
