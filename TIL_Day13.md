# 수업 내용 복습
## python을 활용한 알고리즘(Stack, Queue, and Heap)

1. 232. Implement Queue using Stacks

```python

class MyQueue:
    def __init__(self):
        self.Stack1 = []
        self.Stack2 = []
        233
    def push(self, x: int) -> None:
        self.Stack1.append(x)
        
    def pop(self) -> int:
        # Stack1에서 pop하여 Stack2에 쌓기 (뒤집어서 들어감)
        while len(self.Stack1) > 0:
            self.Stack2.append(self.Stack1.pop())
        returnValue = self.Stack2.pop()

        # 새로 입력되는 push를 고려하면 stack1으로 원상복귀해야함
        while len(self.Stack2) > 0:
            self.Stack1.append(self.Stack2.pop())
        return returnValue
    
    def peek(self) -> int:
        while len(self.Stack1) > 0:
            self.Stack2.append(self.Stack1.pop())
        returnValue = self.Stack2[ len(self.Stack2) -1 ]
        while len(self.Stack2) > 0:
            self.Stack1.append(self.Stack2.pop())
        return returnValue
    
    def empty(self) -> bool:
        return len(self.Stack1) == 0
```

2. 20. Valid Parentheses

```python
class Solution:
    def isValid(self, s: str) -> bool:
        s = list(s)
        print(s)
        
        list_open = []
        
        for i in s:
            if i in ["{", "[", "("]:
                list_open.append(i)

            else:
                if len(list_open) == 0:
                    return False # 오픈 괄호가 아무것도 없는 거니까 이미 짝이 안맞아서
                if list_open[-1] == "(" and i == ")":
                    list_open.pop()
                elif list_open[-1] == "{" and i == "}":
                    list_open.pop()
                elif list_open[-1] == "[" and i == "]":
                    list_open.pop()
                else:
                    return False
        if len(list_open) > 0: # 오픈 괄호가 하나 이상 남아 있음. 클로즈 괄호가 남아 있는 건 신경 쓸 필요 없음. 위에 else에서 False return하니까.
            return False
        return True # 쌍이 다 맞았을 때
```

3. 23. Merge k Sorted Lists
   
```python
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        Myheap = []
        
        for i in lists: # lists에 있는 요소들을 Myheap이라는 리스트에 heappush로 넣음
            while i:
                heapq.heappush(Myheap, i.val)
                i = i.next
        
        AnswerNode = ListNode(0, None) # 빈 listnode 생성
        
        Pointer = AnswerNode # Pointer 생성 및 AnswerNode로 지정
        
        while len(Myheap) != 0:
            Pointer.next = ListNode(heapq.heappop(Myheap), None) # pointer.next를 Myheap의 최소값으로 이동. 반복하면 다음 최소값으로 한칸씩 이동
            Pointer = Pointer.next
            
        return AnswerNode.next # 처음 값인 0 제외하고 나머지 출력
```