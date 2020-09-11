## LeetCode

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

题目来源：力扣（LeetCode）

链接：https://leetcode-cn.com

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。