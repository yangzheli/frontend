## LeetCode

题目来源：力扣（LeetCode）

链接：https://leetcode-cn.com

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. 两数之和
* 问题描述：给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那两个整数，并返回他们的数组下标。<br>
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
* 问题描述：给出两个非空的链表用来表示两个非负的整数。其中，它们各自的位数是按照逆序的方式存储的，并且它们的每个节点只能存储一位数字。<br>
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

4. 寻找两个正序数组的中位数

5. 最长回文子串
* 问题描述：给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。
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

7. 整数反转
* 问题描述：给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。
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