## LeetCode

题目来源：力扣（LeetCode）

链接：https://leetcode-cn.com

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. 两数之和
* 题目描述：给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那两个整数，并返回他们的数组下标。<br>
你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。
```javascript
// Map
var twoSum = function (nums, target) {
    let map = new Map();
    for (let i = 0; i < nums.length; i++) {
        let k = target - nums[i];
        if (map.has(k)) {
            return new Array(map.get(k), i);
        } else {
            map.set(nums[i], i);
        }
    }
    return [];
};
```

2. 两数相加
* 题目描述：给出两个非空的链表用来表示两个非负的整数。其中，它们各自的位数是按照逆序的方式存储的，并且它们的每个节点只能存储一位数字。<br>
如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。<br>
您可以假设除了数字 0 之外，这两个数都不会以 0 开头。
```javascript
/* function ListNode(val) {
    this.val = val;
    this.next = null;
} */

// 双指针
var addTwoNumbers = function (l1, l2) {
    let l3 = new ListNode(0);
    let p = l1, q = l2, k = l3;
    let add = 0;
    while (p != null || q != null) {
        let sum = (p != null ? p.val : 0) + (q != null ? q.val : 0) + add;
        add = sum >= 10 ? 1 : 0;
        k.next = new ListNode(sum % 10);
        p != null && (p = p.next);
        q != null && (q = q.next);
        k = k.next;
    }
    add != 0 && (k.next = new ListNode(add));
    return l3.next;
};
```

3. 无重复字符的最长子串
* 题目描述：给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。
```javascript
var lengthOfLongestSubstring = function (s) {
    let left = 0, right = 0, max_len = 0;
    let map = new Map();
    while (right < s.length) {
        let c = s.charAt(right);
        if (map.has(c)) {
            left = Math.max(left, map.get(c));
        }
        max_len = Math.max(max_len, right - left + 1);
        map.set(c, ++right);
    }
    return max_len;
};
```

4. 寻找两个正序数组的中位数
* 题目描述：给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。<br>
请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。<br>
你可以假设 nums1 和 nums2 不会同时为空。
```javascript
// 1.合并有序数组 O(m + n)
var findMedianSortedArrays = function (nums1, nums2) {
    let res = sort(nums1, nums2);
    let r = res.length, left = Math.floor((r - 1) / 2), right = Math.floor(r / 2);
    return (res[left] + res[right]) / 2;
};

var sort = function (nums1, nums2) {
    let res = [];
    while (nums1.length !== 0 && nums2.length !== 0) {
        if (nums1[0] < nums2[0]) {
            res.push(nums1[0]);
            nums1.splice(0, 1);
        } else {
            res.push(nums2[0]);
            nums2.splice(0, 1);
        }
    }
    if (nums1.length !== 0) {
        res = res.concat(nums1);
    }
    if (nums2.length !== 0) {
        res = res.concat(nums2);
    }
    return res;
}

// 2.二分查找
```

5. 最长回文子串
* 题目描述：给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。
```javascript
// 中心扩散法
var longestPalindrome = function (s) {
    let max_len = 0;
    let res = new String();
    for (let i = 0; i < s.length; i++) {
        let s1 = expand(s, i, i), s2 = expand(s, i, i + 1);
        let s3 = s1.length >= s2.length ? s1 : s2;
        if (s3.length > max_len) {
            max_len = s3.length;
            res = s3;
        }
    }
    return res;
};

// 以索引i、j为中心向外扩散形成的回文串
var expand = function (s, i, j) {
    while (i >= 0 && j < s.length && s.charAt(i) == s.charAt(j)) {
        i--;
        j++;
    }
    return s.substring(i + 1, j);
}
```

6. Z 字形变换
* 题目描述：将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。（略）
```javascript
var convert = function (s, numRows) {
    let arr = [];
    for (let i = 0; i < numRows; i++) {
        arr[i] = [];
    }
    for (let i = 0; i < s.length; i++) {
        // k为索引i的字符所在行数
        let k = i % (numRows === 1 ? 1 : (numRows - 1) * 2);
        if (k > numRows - 1) {
            k = (numRows - 1) * 2 - k;
        }
        arr[k].push(s.charAt(i));
    }
    let res = [];
    for (let i = 0; i < arr.length; i++) {
        res = res.concat(arr[i]);
    }
    return res.join('');
};
```

7. 整数反转
* 题目描述：给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。
```javascript
var reverse = function (x) {
    let s = x < 0 ? false : true;
    let res = new Number();
    x = Math.abs(x);
    while (x != 0) {
        let p = x % 10;
        res = res * 10 + p;
        x = Math.floor(x / 10);
    }
    res = s ? res : -res;
    return res >= (2 ** 31) || res < -(2 ** 31) ? 0 : res;
};
```

8. 字符串转换整数
* 题目描述：请你来实现一个 atoi 函数，使其能将字符串转换成整数。<br>
首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。（略）<br>
在任何情况下，若函数不能进行有效的转换时，请返回 0 。
```javascript
// 正则表达式
var myAtoi = function (str) {
    let res = str.trim().match(/^[-+]?\d+/);
    if (res === null) {
        return 0;
    } else {
        let num = new Number(res[0]);
        const max = (2 ** 31) - 1, min = -(2 ** 31);
        return num > max ? max : (num < min ? min : num);
    }
};
```

9. 回文数
* 题目描述：判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。
```javascript
var isPalindrome = function (x) {
    let s = x.toString();
    return s.split('').reverse().join('') === s;
};
```

10. 正则表达式匹配
* 题目描述：给你一个字符串 s 和一个字符规律 p，请你来实现一个支持 '.' 和 '*' 的正则表达式匹配。
```javascript
// 1.match
var isMatch = function (s, p) {
    let res = s.match(p);
    return res !== null && res[0] === s;
};

// 2.test
var isMatch = function (s, p) {
    return new RegExp('^' + p + '$').test(s);
};

// 3.动态规划
```

11. 乘最多水的容器
* 题目描述：给定 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。<br>
说明：你不能倾斜容器，且 n 的值至少为 2。
```javascript
// 双指针
var maxArea = function (height) {
    let i = 0, j = height.length - 1;
    let max_area = 0;
    while (i < j) {
        max_area = Math.max(max_area, (j - i) * Math.min(height[i], height[j]));
        if (height[i] < height[j]) {
            i++;
        } else {
            j--;
        }
    }
    return max_area;
};
```

12. 整数转罗马数字
* 题目描述：罗马数字包含以下七种字符： I， V， X， L，C，D 和 M。（略）<br>
给定一个整数，将其转为罗马数字。输入确保在 1 到 3999 的范围内。
```javascript
// 递归
var ones = ['I', 'II', 'III', 'IV', 'V', 'VI', 'VII', 'VIII', 'IX']; // 个位
var tens = ['X', 'XX', 'XXX', 'XL', 'L', 'LX', 'LXX', 'LXXX', 'XC']; // 十位
var hundreds = ['C', 'CC', 'CCC', 'CD', 'D', 'DC', 'DCC', 'DCCC', 'CM']; // 百位
var thousands = ['M', 'MM', 'MMM'];   // 千位

var intToRoman = function (num) {
    if (num >= 1000) {
        return thousands[Math.floor(num / 1000) - 1] + intToRoman(num % 1000);
    } else if (num >= 100) {
        return hundreds[Math.floor(num / 100) - 1] + intToRoman(num % 100);
    } else if (num >= 10) {
        return tens[Math.floor(num / 10) - 1] + intToRoman(num % 10);
    } else if (num >= 1) {
        return ones[num - 1];
    } else {
        return "";
    }
};
```

13. 罗马数字转整数
* 题目描述：罗马数字包含以下七种字符: I， V， X， L，C，D 和 M。（略）<br>
给定一个罗马数字，将其转换成整数。输入确保在 1 到 3999 的范围内。
```javascript
var K = ['I', 'V', 'X', 'L', 'C', 'D', 'M']; // 字符
var V = [1, 5, 10, 50, 100, 500, 1000]; // 数值

var romanToInt = function (s) {
    let index = 0, res = 0;
    while (index < s.length) {
        let left = K.indexOf(s[index]), right = index < s.length - 1 ? K.indexOf(s[index + 1]) : -1;
        if (left < right) {
            res += V[right] - V[left];
            index += 2;
        } else {
            res += V[left];
            index++;
        }
    }
    return res;
};
```

14. 最长公共前缀
* 题目描述：编写一个函数来查找字符串数组中的最长公共前缀。<br>
如果不存在公共前缀，返回空字符串 ""。
```javascript
// 分治法
var longestCommonPrefix = function (strs) {
    if (strs.length === 0) {
        return "";
    }
    return divide(strs, 0, strs.length - 1);
};

var divide = function longestCommonPrefix(strs, l, r) {
    if (l === r) {
        return strs[l];
    }
    let mid = l + Math.floor((r - l) / 2);
    let left = divide(strs, l, mid);
    let right = divide(strs, mid + 1, r);
    return commonPrefix(left, right);
}

// 两个单词的公共前缀
var commonPrefix = function (left, right) {
    let index = 0;
    while (index < left.length && index < right.length) {
        if (left.charAt(index) !== right.charAt(index)) {
            return left.substring(0, index);
        }
        index++;
    }
    return left.substring(0, index);
}
```

15. 三数之和
* 题目描述：给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。<br>
注意：答案中不可以包含重复的三元组。
```javascript
// O(n^2)
var threeSum = function (nums) {
    let res = [];
    nums.sort(function (a, b) {
        return a - b;
    });
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] > 0) {  // 三个大于0的数相加和一定大于0
            break;
        }
        if (i > 0 && nums[i] === nums[i - 1]) { // 去重
            continue;
        }
        let left = i + 1, right = nums.length - 1, target = -nums[i];
        while (left < right) {
            if (nums[left] + nums[right] === target) {
                res.push([nums[i], nums[left], nums[right]]);
                left++;
                right--;
                while (left < right && nums[left] === nums[left - 1]) {
                    left++;
                }
                while (left < right && nums[right] === nums[right + 1]) {
                    right--;
                }
            } else if (nums[left] + nums[right] < target) {
                left++;
            } else {
                right--;
            }
        }
    }
    return res;
}
```

16. 最接近的三数之和

17. 电话号码的字母组合
* 题目描述：给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。<br>
给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。
```javascript
// 递归
var map = { '2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl', '6': 'mno', '7': 'pqrs', '8': 'tuv', '9': 'wxyz' };

var letterCombinations = function (digits) {
    if (digits.length === 0) {
        return [];
    }
    return recurse(digits, [], 0);
};

var recurse = function (digits, res, index) {
    if (index === digits.length - 1) {
        return map[digits[index]].split('');
    }
    let arr = recurse(digits, res, index + 1);
    let str = map[digits[index]];
    for (let i = 0; i < str.length; i++) {
        let newArr = [];
        for (let j = 0; j < arr.length; j++) {
            newArr.push(str.charAt(i) + arr[j]);
        }
        res = res.concat(newArr);
    }
    return res;
}
```

18. 四数之和

19. 删除链表的倒数第N个节点
* 题目描述：给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。
```javascript
// 1.两趟遍历
var removeNthFromEnd = function (head, n) {
    let dummy = new ListNode(0);  // 哑节点
    dummy.next = head;
    let p = dummy;
    let len = 0;
    while (p != null) {
        p = p.next;
        len++;
    }
    len = len - n;
    p = dummy;
    while (len > 1) {
        p = p.next;
        len--;
    }
    p.next = p.next.next;
    return dummy.next;
};

// 2.双指针 一趟遍历
var removeNthFromEnd = function (head, n) {
    let dummy = new ListNode(0);  // 哑节点
    dummy.next = head;
    let p = dummy, q = dummy;
    while (n > 0) {
        p = p.next;
        n--;
    }
    while (p.next != null) {
        p = p.next;
        q = q.next;
    }
    q.next = q.next.next;
    return dummy.next;
};
```

20. 有效的括号
* 题目描述：给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。<br>
注意空字符串可被认为是有效字符串。
```javascript
var isValid = function (s) {
    let arr = [];
    let map = { ')': '(', '}': '{', ']': '[' };
    for (let i = 0; i < s.length; i++) {
        let c = s.charAt(i);
        if (c === '(' || c === '{' || c === '[') {
            arr.push(c);
        } else if ((arr.length === 0) || arr[arr.length - 1] !== map[c]) {
            return false;
        } else {
            arr.pop();
        }
    }
    return arr.length === 0;
};
```