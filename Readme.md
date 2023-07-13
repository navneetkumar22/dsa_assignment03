# PPT - DSA Assignment 3

<br/>

## Answer 1:
```js
const threeSumClosest = (nums, target) => {

    nums.sort((a, b) => a - b); // sorting

    const n = nums.length;
    
    // Result
    let closest = nums[0] + nums[1] + nums[n - 1];
    // Loop for each element of the array
    for (let i = 0; i < n - 2; i++) {
        // Left and right pointers
        let j = i + 1;
        let k = n - 1;
       
        // Loop for all other pairs
        while (j < k) {
            let sum = nums[i] + nums[j] + nums[k];
            if (sum <= target) {
                j++;
            } else {
                k--;
            }
            if (Math.abs(closest - target) > Math.abs(sum - target)) {
                closest = sum;
            }
        }
    }
    return closest;
};
```

<br/>

## Answer 2:
```js
const fourSum = (nums, target) => {
    // Resultant list
    const quadruplets = [];
    // Base condition
    if (nums == undefined || nums.length < 4) {
        return quadruplets;
    }
    // Sort the array
    nums.sort((a, b) => a - b);
    // Length of the array
    const n = nums.length;
    // Loop for each element of the array
    for (let i = 0; i < n - 3; i++) {
        // Check for skipping duplicates
        if (i > 0 && nums[i] == nums[i - 1]) {
            continue;
        }
        // Reducing to three sum problem
        for (let j = i + 1; j < n - 2; j++) {
            // Check for skipping duplicates
            if (j != i + 1 && nums[j] == nums[j - 1]) {
                continue;
            }
            // Left and right pointers
            let k = j + 1;
            let l = n - 1;
            // Reducing to two sum problem
            while (k < l) {
                const currentSum = nums[i] + nums[j] + nums[k] + nums[l];
                if (currentSum < target) {
                    k++;
                } else if (currentSum > target) {
                    l--;
                } else {
                    quadruplets.push([nums[i], nums[j], nums[k], nums[l]]);
                    k++;
                    l--;
                    // Check for skipping duplicates
                    while (k < l && nums[k] == nums[k - 1]) {
                        k++;
                    }
                    while (k < l && nums[l] == nums[l + 1]) {
                        l--;
                    }
                }
            }
        }
    }
    return quadruplets;
};
```

<br/>

## Answer 3:
```js
const nextPermutation = (nums) => {
    // Length of the array
    const n = nums.length;
    // Index of the first element that is smaller than
    // the element to its right.
    let index = -1;
    // Loop from right to left
    for (let i = n - 1; i > 0; i--) {
        if (nums[i] > nums[i - 1]) {
            index = i - 1;
            break;
        }
    }
    // Base condition
    if (index === -1) {
        reverse(nums, 0, n - 1);
        return nums;
    }
    let j = n - 1;
    // Again swap from right to left to find first element
    // that is greater than the above find element
    for (let i = n - 1; i >= index + 1; i--) {
        if (nums[i] > nums[index]) {
            j = i;
            break;
        }
    }
    // Swap the elements
    swap(nums, index, j);
    // Reverse the elements from index + 1 to the nums.length
    reverse(nums, index + 1, n - 1);
    return nums;
};

const reverse = (nums, i, j) => {
    while (i < j) {
        swap(nums, i, j);
        i++;
        j--;
    }
};

const swap = (nums, i, index) => {
    const temp = nums[index];
    nums[index] = nums[i];
    nums[i] = temp;
};
```

<br/>

## Answer 4:
```js
const searchTarget = (nums, target) => {
    let left = 0;
    let right = nums.length;

    while (left < right) {
        const middle = Math.floor((left + right) / 2);

        if (nums[middle] < target) {
            left = middle + 1;
        } else {
            right = middle;
        }
    }

    return left;
};
```

<br/>

## Answer 5
```js
const plusOne = (digits) => {
    for (let i = digits.length - 1; i >= 0; i--) {
        digits[i]++;
        if (digits[i] > 9) {
            digits[i] = 0;
        }
        else {
            return digits;
        }
    }
    digits.unshift(1);
    return digits;
};
```

<br/>

## Answer 6:
```js
const singleNumber = (nums) => {
    let map = new Map();
    for (let n of nums) {
        map.set(n, map.get(n) + 1 || 1);
    }
    for (let num of map) {
        if (num[1] === 1) {
            return num[0];
        }
    }
};
```

<br/>

## Answer 7:
```js
const summaryRanges = (nums) => {
    let arr = [];
    let startVal = 0;
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] + 1 !== nums[i + 1] && nums[i] - 1 !== nums[i - 1]) {
            arr.push("" + nums[i]);
        } else if (nums[i] + 1 !== nums[i + 1] && nums[i] - 1 === nums[i - 1]) {
            arr.push("" + startVal + "->" + nums[i])
        } else if (nums[i] + 1 === nums[i + 1] && nums[i] - 1 !== nums[i - 1]) {
            startVal = nums[i]
        }

    }
    return arr;
};
```

<br/>

## Answer 8:
```js
const canAttendMeetings = (intervals) => {
    intervals.sort((a, b) => {
        return a.start > b.start ? 1 : -1;
    });

    for (var i = 1; i < intervals.length; i++) {
        if (intervals[i - 1].end > intervals[i].start) {
            return false;
        }
    }

    return true;
}
```