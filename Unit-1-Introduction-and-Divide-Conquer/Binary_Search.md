# Binary Search

## 1. Introduction

Searching is the process of finding a particular element in a collection of
data. Binary search is one of the most efficient searching techniques, but it
can be applied only when the data is arranged in sorted order.

Unlike linear search, which checks elements one by one, binary search compares
the search key with the middle element and eliminates half of the search space
after every comparison.

## 2. Definition

Binary search is a divide-and-conquer searching algorithm that finds a target
element in a sorted array by repeatedly dividing the search interval into two
halves.

## 3. Detailed Explanation

Suppose an array contains elements in ascending order. The algorithm maintains
three values:

- `low`: starting index of the current search range
- `high`: ending index of the current search range
- `mid`: middle index of the current search range

The target is compared with the element at `mid`.

- If `arr[mid]` equals the target, the search is successful.
- If the target is greater than `arr[mid]`, the left half is discarded.
- If the target is smaller than `arr[mid]`, the right half is discarded.
- The process continues until the element is found or the range becomes empty.

## 4. Preconditions

Binary search requires:

1. The elements must be stored in an array or similar indexed structure.
2. The array must be sorted.
3. The elements must be comparable.

## 5. Formula

The middle index is calculated as:

\[
mid = low + \frac{high-low}{2}
\]

This form is preferred in programs because it reduces the possibility of integer
overflow compared with:

\[
mid = \frac{low+high}{2}
\]

## 6. Recurrence Relation

For every step, binary search operates on half of the previous input:

\[
T(n) = T\left(\frac{n}{2}\right) + c
\]

where `c` represents the constant-time comparison and index operations.

Solving the recurrence gives:

\[
T(n) = O(\log n)
\]

## 7. Algorithm

### Algorithm: Binary Search

**Input:** A sorted array `A` containing `n` elements and a search key `K`  
**Output:** The index of `K`, if present; otherwise, report unsuccessful search

1. Start.
2. Set `low = 0`.
3. Set `high = n - 1`.
4. Repeat while `low <= high`:
   1. Calculate `mid = low + (high - low) / 2`.
   2. If `A[mid] == K`, return `mid`.
   3. If `A[mid] < K`, set `low = mid + 1`.
   4. Otherwise, set `high = mid - 1`.
5. If `low > high`, report that the element is not present.
6. Stop.

## 8. Worked Example

Consider the sorted array:

```text
A =[1][2][3]
```

Search key:

```text
K = 50
```

| Step | Low | High | Mid | A[Mid] | Action |
|---|---:|---:|---:|---:|---|
| 1 | 0 | 6 | 3 | 40 | `50 > 40`, search right half |
| 2 | 4 | 6 | 5 | 60 | `50 < 60`, search left half |
| 3 | 4 | 4 | 4 | 50 | Element found |

The element is found at index `4`, which is position `5` in one-based numbering.

## 9. C Program

```c
#include <stdio.h>

// Function to search for a key using binary search
int binarySearch(int arr[], int n, int key) {
    int low = 0;
    int high = n - 1;

    // Continue until the search range becomes empty
    while (low <= high) {
        // Calculate the middle index
        int mid = low + (high - low) / 2;

        // If the middle element is the required key, return its index
        if (arr[mid] == key) {
            return mid;
        }

        // If the key is greater, search in the right half
        if (arr[mid] < key) {
            low = mid + 1;
        }

        // If the key is smaller, search in the left half
        else {
            high = mid - 1;
        }
    }

    // Return -1 if the key is not found
    return -1;
}

int main() {
    int arr;
    int n, key, i;
    int result;

    printf("Enter the number of elements: ");
    scanf("%d", &n);

    printf("Enter %d elements in sorted order:\n", n);
    for (i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    printf("Enter the element to search: ");
    scanf("%d", &key);

    result = binarySearch(arr, n, key);

    if (result == -1) {
        printf("Element not found.\n");
    } else {
        printf("Element found at index %d.\n", result);
        printf("Element found at position %d.\n", result + 1);
    }

    return 0;
}
```

## 10. Sample Input

```text
Enter the number of elements: 7
Enter 7 elements in sorted order:
10 20 30 40 50 60 70
Enter the element to search: 50
```

## 11. Sample Output

```text
Element found at index 4.
Element found at position 5.
```

## 12. Complexity Analysis

### Best Case

The key is found during the first comparison, when it is the middle element.

\[
T(n) = O(1)
\]

### Average Case

The algorithm continues to divide the array into halves.

\[
T(n) = O(\log n)
\]

### Worst Case

The key is found after the maximum number of divisions or is not present.

\[
T(n) = O(\log n)
\]

### Space Complexity

The iterative algorithm uses only a fixed number of variables.

\[
S(n) = O(1)
\]

## 13. Advantages

- Faster than linear search for large sorted arrays.
- Reduces the search space by half after every comparison.
- Has logarithmic worst-case time complexity.
- Requires only constant extra space in its iterative form.
- Easy to implement and analyze.

## 14. Limitations

- The array must be sorted before searching.
- Maintaining sorted order can be costly when frequent insertions occur.
- It is less suitable for linked lists because linked lists do not provide direct
  indexed access.
- Sorting the data first may not be worthwhile if only one search is required.

## 15. Applications

Binary search is used in:

- Searching names in sorted records.
- Finding values in sorted databases.
- Dictionary and contact-list searches.
- Searching files and indexes.
- Finding boundaries or ranges in numerical data.
- Solving optimization problems using binary-search-on-answer techniques.

## 16. Conclusion

Binary search is an efficient divide-and-conquer algorithm for searching sorted
data. By eliminating half of the search space after every comparison, it achieves
`O(log n)` worst-case time complexity and is significantly faster than linear
search for large collections.

## 17. Practice Questions

1. Implement binary search using recursion.
2. Modify the program to find the first occurrence of a repeated element.
3. Modify the program to find the last occurrence of a repeated element.
4. Compare binary search with linear search.
5. Explain why binary search cannot be directly applied to an unsorted array.
