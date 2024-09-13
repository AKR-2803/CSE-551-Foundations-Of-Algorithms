## Scheduling to Minimize Lateness

#### Algorithm used to minimize lateness when a single resource processes one job at a time.

| Problem                                                                                                 | 
|---------------------------------------------------------------------------------------------------------| 
| <img src="./images/01-minimise-lateness-02.png" alt="Minimise-Lateness-Image" width="450" height="210"> |
[Image Source](https://stumash.github.io/Algorithm_Notes/greedy/intervals/min_late.png)

### Notations
- t<sub>j</sub>: time taken by job `j` to complete
- d<sub>j</sub>: due time of job `j`
- s<sub>j</sub>: start time of job `j`
- f<sub>j</sub>: finish time of job `j`
___
### What is **l<sub>j</sub> = max(0, f<sub>j</sub> - d<sub>j</sub>)**?

- Lateness is how much the job finishes later than its due time.
- Case I: Job finished before the due time
  - If a job had due time d<sub>j</sub> = 8, but finished at f<sub>j</sub> = 2, lateness `l = 2 - 8 = -6`. This negative value means the job finished within the due time, so `l = 0`.
- Case II: Job finished after the due time
  - If a job had due time d<sub>j</sub> = 8, but finished at f<sub>j</sub> = 11, lateness `l = 11 - 8 = 3`. The job was 3 units late, so lateness `l = 3`.
- Therefore, to handle both cases concisely, we use l<sub>j</sub> = max(0, f<sub>j</sub> - d<sub>j</sub>).
  - If the difference is negative (Case I), `l = max(0, negative_value) = 0`
  - If the difference is positive (Case II), `l = max(0, positive_value) = positive_value`
___
### Our aim is to minimize lateness. Let's brainstorm.
- Clearly, allocating jobs randomly won't help. We need some criteria to order the jobs.
- What criteria should we set?
- We have two factors: time taken and due time.
- Maybe, we can use these two criteria to order the jobs:
  - **Criteria 1**: by time taken [priority to the job that takes less time t<sub>j</sub>]
  - **Criteria 2**: by deadline [priority to the job with the earliest deadline d<sub>j</sub>]
- Another factor we can consider is the difference between due time d<sub>j</sub> and time taken t<sub>j</sub>, called "slack time".
- SLACK TIME: The time a job can wait without being late.
- For example, **Job-2** has t<sub>j</sub> = 8, d<sub>j</sub> = 2. `Slack time = 8 - 2 = 6`. This means Job-2 can wait until time `t = 6` before being scheduled without incurring lateness.
- Slack time can be another criterion to order jobs:
  - **Criteria 3**: by slack time [priority to the job with less slack time]

| Slack Times for Example                                                                                   | 
|-----------------------------------------------------------------------------------------------------------| 
| <img src="./images/01-minimise-lateness-01.jpg" alt="Interval-Scheduling-Image" width="600" height="150"> |

___

### Checking Criteria 1: By Time Taken

The following counterexample shows that this approach fails. If we prioritize time taken, we get:

|                | 1   | 2   |
|----------------|-----|-----|
| t<sub>j</sub>  | 1   | 10  |
| d<sub>j</sub>  | 100 | 10  |

| `l = 1` for Criteria 1, but it could have been better, i.e. `l = 0`                                       | 
|-----------------------------------------------------------------------------------------------------------| 
| <img src="./images/01-minimise-lateness-03.jpg" alt="Interval-Scheduling-Image" width="500" height="150"> |

___
### Checking Criteria 3: By Slack Time

The following counterexample shows that this approach fails. If we prioritize slack time, we get:

|                | 1 | 2   |
|----------------|---|-----|
| t<sub>j</sub>  | 1 | 10  |
| d<sub>j</sub>  | 2 | 10  |

| `l = 11` for Criteria 3, but it could have been better, i.e. `l = 2`                                      | 
|-----------------------------------------------------------------------------------------------------------| 
| <img src="./images/01-minimise-lateness-04.jpg" alt="Interval-Scheduling-Image" width="500" height="150"> |

___
### Checking Criteria 2: By Due Time

- This approach works best because it prioritizes due time, the main factor responsible for lateness.
- Running the previous examples with this criterion will yield optimal results.
- By addressing due time early, we can minimize overall lateness.
- However, be cautious: while this greedy approach seems reasonable locally, it may not always guarantee a globally optimal solution!
