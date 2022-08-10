# 수업 내용 복습
## python을 활용한 알고리즘(Leetcode_linked list)

1. 234. Palindrome Linked List
```python
V1.

class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        head_list = []
        #linked list를 순회하면서 list로 만들어줌.
        while head:
            head_list.append(head.val) # 첫번째 value인 1을 append하는데 
            print(head_list)
            head = head.next #더한다음에 다음값으로 넘어가기.
            print(head)
        return head_list == head_list[::-1]


V2.

class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        PointerNode = head
        myList = list()
        while PointerNode: #위에 처럼 head를 직접 쓰는 것이 아니라 포인터를 활용할 수 있는데(head.prev가 지워지지 않게 하기 위해서), 이 문제를 새로운 리스트를 만드는 것이니까 그냥 head를 써도 submit은 됨.  
            myList.append(PointerNode.val)
            PointerNode = PointerNode.next
        return myList == list(reversed(myList))

```

2. 21. Merge Two Sorted Lists

```python
# pointer의 작동 원리에 대해서 잘 이해가 안감. 다시 살펴볼 것!
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        Header = ListNode(0, None)
        Pointer = Header
  
        while list1 and list2:
            if list1.val < list2.val:
                Pointer.next = ListNode(list1.val,None)
                print(Pointer)
                Pointer = Pointer.next
                list1 = list1.next
            else: 
                Pointer.next = ListNode(list2.val, None)
                Pointer = Pointer.next
                list2 = list2.next
                
        #List1이 List2보다 길이가 길 때
        while list1:
                Pointer.next = ListNode(list1.val,None)
                Pointer = Pointer.next
                list1 = list1.next

        while list2:
                Pointer.next = ListNode(list2.val,None)
                Pointer = Pointer.next
                list2 = list2.next
 
        return Header.next
```


3. 206. Reverse Linked List
```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        Prev = None # 시작 -> null 위치
        Pointer = head # 시작 -> 1위치
        while Pointer:
            Next = Pointer.next # Twopoint # 시작 -> 2
            Pointer.next = Prev # Prev설정 # 2에 위치한 pointer.next를 prev로 변경.
            Prev = Pointer # Prev설정 #  
            Pointer = Next #Twopoint # 
        return Prev #여기는 prev를 리턴....head를 하면?
        
        # null - 1 - 2 - 3 - null
        # next = current.next
        # current.next = prev
        # prev = current
        # curr
        
        # 여기서 next와 prev는 어떤 밸류가 아니라 그냥 위치. 인덱스와 같은 것?
        # 21번보다는 오히려 더 이해는 되는 것 같은데 이 문제를 포함해서 linked list에 대해 더 공부해야겠다.
```