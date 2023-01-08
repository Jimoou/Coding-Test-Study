# Merge Sort(병합정렬)

```python
def merge_sort(A):
    if len(A) < 2:
        return A
    mid = len(A) // 2
    left = merge_sort(A[:mid])
    right = merge_sort(A[mid:])
    merged = []
    left_index = right_index = 0
    while left_index < len(left) and right_index < len(right):
        if left[left_index] < right[right_index]:
            merged.append(left[left_index])
            left_index += 1
        else:
            merged.append(right[right_index])
            right_index += 1
    merged += left[left_index:]
    merged += right[right_index:]
    return merged


if __name__ == '__main__':
    A = [10, 4, 5, 2, 3, 1, 6, 8, 7, 9]
    print(merge_sort(A))
```

```java
import java.util.Arrays;

public class MergeSort {
    public static void main(String[] args) {
        int[] A = {10, 4, 5, 2, 3, 1, 6, 8, 7, 9};
        System.out.println(Arrays.toString(merge_sort(A)));
    }

    public static int[] merge_sort(int[] arr) {
        if (arr.length < 2) {
            return arr;
        }
        int mid = arr.length / 2;
        int[] left = merge_sort(Arrays.copyOfRange(arr, 0, mid));
        int[] right = merge_sort(Arrays.copyOfRange(arr, mid, arr.length));
        int[] merged = new int[arr.length];
        int merged_index = 0;
        int left_index = 0;
        int right_index = 0;

        while (left_index < left.length && right_index < right.length) {
            if (left[left_index] < right[right_index]) {
                merged[merged_index++] = left[left_index++];
            } else {
                merged[merged_index++] = right[right_index++];
            }
        }
        while (left_index < left.length) {
            merged[merged_index++] = left[left_index++];
        }
        while (right_index < right.length) {
            merged[merged_index++] = right[right_index++];
        }
        return merged;
    }
```