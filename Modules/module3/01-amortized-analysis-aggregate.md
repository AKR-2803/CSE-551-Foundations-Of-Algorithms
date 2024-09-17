## Amortized Time Calculation: Example with Dynamic Array

To calculate **amortized time**, we spread the total cost of all operations over each individual operation, even if some of them are expensive. This helps understand the average cost per operation over a sequence of operations.

#### What is the cost?
- **Worst-case cost**: Cost of a single operation in the worst scenario.
- **Amortized cost**: Average cost per operation over a series of operations.

### Calculating Amortized Time:

1. **Cost of Single Operations:**
   - Appending a new element when there's space is **O(1)**.
   - When resizing is required (array is full), the cost of resizing is **O(n)**, where \(n\) is the current array size.

2. **Calculating Total Cost (Aggregate Analysis):**
   Let's analyze what happens when we append elements one by one:

| **Element** | **Operation** | **Cost to Append** | **Resizing Cost** |
|-------------|--------------------|--------------------|-------------------|
| 1           | Normal Append      | 1                  | 0                 |
| 2           | Resize + Append    | 1                  | 1 (copying 1 element) |
| 3           | Normal Append      | 1                  | 0                 |
| 4           | Resize + Append    | 1                  | 2 (copying 2 elements) |
| 5           | Normal Append      | 1                  | 0                 |
| 6           | Normal Append      | 1                  | 0                 |
| 7           | Normal Append      | 1                  | 0                 |
| 8           | Resize + Append    | 1                  | 4 (copying 4 elements) |
| 9           | Normal Append      | 1                  | 0                 |
| 10          | Normal Append      | 1                  | 0                 |

- **Normal Append**: When there is no need for resizing, the cost is O(1).
- **Resize + Append**: When resizing occurs, the cost includes both resizing and appending. The resizing cost depends on the number of elements copied.


- **Total Cost** for appending 10 elements = Sum of all individual costs
    - Normal appends: (10 * O(1) = 10)
    - Resizing costs: Copying elements during resizing (1 + 2 + 4 = 7)
    - Thus, the total cost = 10 (normal appends) + 7 (resizing) = 17.

3. **Amortized cost per operation** = `Total Cost / No. of Operations = 17/10 = 1.7`, which is a constant 
4. **Amortized Time**:  **O(1)** per append operation.

### Conclusion:
- **Worst-case time** for a single append: **O(n)** (during resizing).
- **Amortized time** for multiple operations: **O(1)** per append, because the cost of resizing is distributed over many cheap operations.