# Reservoir Sampling

## Problem

Given a stream of data, we need to select k elements randomly and make sure that each element has the same possibility of been chosen.

## Solution

**Reservoir Sampling Algorithm**

First of all, we will have a reservoir of size k. For the first k elements in the stream, we store them in the reservoir directly. Starting from the k +1 element with an index of i (starting from 0), we will choose a random integer j between [0, i], if the random integer falls between [0, k), then we will store it in our reservoir at the index j, otherwise we just discard it. At the end of the stream, the elements remain at the reservoir are our samplings.

**Proof of Correctness**

We need to proof that for each element:

$$
\begin{aligned}
P(selected) &= 
P_1(enters \space reservoir) \times P_2(not \space been \space swapped \space by \space other \space element) \\&= \frac{k}{N} \end{aligned}
$$

$$
\because P_1(i)=\left\{
\begin{aligned}
& 1 & i \in [0, k) \\
& \frac{k}{i + 1} & i \in [k, N) \\
\end{aligned}
\right.

$$

$$
P_2(i)=\left\{
\begin{aligned}
& \frac{k}{k + 1} \times \frac{k + 1}{k + 2} \times \cdots \frac{N - 1}{N} = \frac{k}{N} & i \in [0, k) \\
& \frac{i + 1}{i + 2} \times \frac{i + 2}{i + 3} \times \cdots \frac{N - 1}{N} = \frac{i + 1}{N} & i \in [k, N) \\
\end{aligned}
\right.

$$

$$
\therefore \text{for every i, } P(selected) = P_1 \times P_2 = \frac{k}{N}
$$

### Questions:

[**Leetcode 382 Linked List Random Node**](https://leetcode.com/problems/linked-list-random-node/description/)

```jsx
class Solution {
    private ListNode head = null;
    private Random randn = null;

    public Solution(ListNode head) {
        this.head = head;
        this.randn = new Random();
    }
    
    public int getRandom() {
        int res = 0;
        int cnt = 0;
        ListNode curNode = head;
        while (curNode != null) {
            if (randn.nextInt(++cnt) == 0) {
                res = curNode.val;
            }
            curNode = curNode.next;
        }
        return res;
    }
}
```