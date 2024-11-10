# min-of-max-subarrays

def min_of_max_in_subarrays(arr, k):
    # This deque will store indices of array elements
    # The elements are maintained in decreasing order of values
    dq = deque()
    max_in_subarrays = []

    # Process the first k elements and initialize the deque
    for i in range(k):
        # Remove elements that are smaller than the current element from the end
        while dq and arr[dq[-1]] <= arr[i]:
            dq.pop()
        dq.append(i)

    # Process the rest of the elements
    for i in range(k, len(arr)):
        # Append the max of the current window (front of deque)
        max_in_subarrays.append(arr[dq[0]])

        # Remove indices that are out of this window
        while dq and dq[0] <= i - k:
            dq.popleft()

        # Remove elements smaller than the current element from the end
        while dq and arr[dq[-1]] <= arr[i]:
            dq.pop()
        dq.append(i)

    # Add the maximum for the last window
    max_in_subarrays.append(arr[dq[0]])

    # Return the minimum of the maximums in all subarrays
    return min(max_in_subarrays)

# Sample Input
k = 3
arr = [3, 1, 4, 1, 5, 9]
# Output the result
print(min_of_max_in_subarrays(arr, k))  # Expected output: 4
