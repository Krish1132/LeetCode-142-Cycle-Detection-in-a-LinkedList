# Licked List Cycle

### Problem - 

We are given the head of a LinkedList.</br>
Part 1 &rarr; We need to find whether there exists a cycle in a LinkedList</br>
Part 2 &rarr; If a cycle exists we have to return the position at which the cycle starts</br>
</br>
Definition of the Singly LinkedList class - 
```
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) {
      val = x;
      next = null;
    }
}
```

---

### Algorithm -

__Floyd's Cycle-Finding Algorithm__ &rarr; Also known as Floyd's Tortoise-Hare algorithm is an algorithm which is used to detect if a cycle exists in a LinkedList. In this algorithm, there are two pointers which moves at two different speeds while traversing the LinkedList. One pointer moves with normal speed, that is, it traverses the LinkedList one node at a time, called the <strong>tortoise or the slow pointer</strong>. The other pointer, moves at twice the speed, that is, it skips one node between each traversal and jumps to the next node, is called the <strong>hare or the fast pointer</strong>.</br>There are two possibilites that can happen:</br>
<ol>
<li>The hare pointer eventually stops traversing and reaches the end of the list, in which case, there is no cycle in the LinkedList.</li>
<li>The hare and the tortoise pointer meets at a node which means a loop is present in the LinkedList.</li>
</ol>
</br>

*detectCycle()*</br>
Step 1 - Start
Step 2 - Declare the variables tortoise, hare of type *ListNode* and initialize them to head.
Step 3 - Declare a variable temp of type *ListNode* and initialize it to head to store the original reference to the head of the LinkedList.
Step 4 - As long as there are atleast two nodes in front of the hare pointer in the LinkedList, do the following - 
<ul>
<li>Increment tortoise pointer to point to the next node and hare pointer to point to the node next to the next node.</li>
<li>If we find a loop, (that is, tortoise = hare) we trace the path from the head of the Linked List as follows - </li>
</br>
while tortoise $\neq$ temp, increment tortoise and temp to point to the next node in the list. Return temp when temp = tortoise.
<li>If the program control successfully passes through the while loop that signifies that either hare.next.next = null or hare.next = null, return null as there is no cycle in the LinkedList.</li>
</ul>

### JAVA logic to solve the problem -


```

public ListNode detectCycle(ListNode head) {
    if(head == null || head.next == null) return null;
    ListNode hare = head, tortoise = head, temp = head;
    while(hare.next != null && hare.next.next != null){
        tortoise = tortoise.next;
        hare = hare.next.next;
        if(hare == tortoise){
            while(temp != tortoise){
                tortoise = tortoise.next;
                temp = temp.next;
            }
            return temp;
        }
    }
    return null;
}

```



Lets take the example of a LinkedList - 

![image](https://user-images.githubusercontent.com/92263569/190052348-f882d976-9193-4a41-853d-40d0bb1824ef.png)

In the above example, the loop starts at position 1 (assuming 0-based indexing).


<pre>
              
Initially,
              
                   &larr; &larr; &larr; &larr; &larr;
                  &darr;        &uarr;
              3 &rarr; 2 &rarr; 0 &rarr; -4</br>
              &uarr;
              hare(h), tortoise(t), temp(tmp)
              
              hare.next != null && hare.next.next != null and t $/neq$ h, therefore, loop continues
              
              3 &rarr; 2 &rarr; 0 &rarr; -4</br>
              &uarr;   &uarr;   &uarr;
             tmp  t   h
            
              hare.next != null && hare.next.next != null and t $/neq$ h, therefore, loop continues
              
              3 &rarr; 2 &rarr; 0 &rarr; -4</br>
              &uarr;   &uarr;   &uarr;
             tmp  h   t
            
              hare.next != null && hare.next.next != null and t $/neq$ h, therefore, loop continues
              
              3 &rarr; 2 &rarr; 0 &rarr; -4</br>
              &uarr;            &uarr;
             tmp         h, t
             
             h = t &rarr; cycle detected!
             
             Increment tmp and t as long as tmp $/ned$ t
             
              3 &rarr; 2 &rarr; 0 &rarr; -4</br>
                  &uarr;
                tmp, t
             
             tmp = t &rarr; cycle starting point found, return tmp.
</pre>
