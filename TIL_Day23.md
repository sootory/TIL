# 수업 내용 복습
## python을 활용한 알고리즘(Leetcode_DFS, BFS)

1. 17번
```python
# 17(DFS)

class Solution:
    
    def DFS(self, Digits, Sequences):
        # DFS로 맨 마지막 leaf에 도달하면 정답에 추가
        if len(Sequences) == self.lenChar: # digits의 길이와 Sequences 리스트에 추가된 조합의 길이가 같을 때(조합이 끝났을 때)/ not Digits로 해도 됨
            self.Answer.append("".join(Sequences)) # 이를 Answer 리스트에 append
            
        # Digits가 남아있다는 뜻 = 아직 DFS가 leaf에 도달하지 않았다는 뜻

        if Digits:
            NewSeq = Digits.pop(0) 
            NewChars = self.Dict[NewSeq] # pop한 값("2" 또는 "3")을 key로 하여, item을 출력.
            for Char in NewChars: # 출력한 item을 for문을 통해 하나씩 리턴
                self.DFS(Digits[:], Sequences + [Char]) # 리턴한 값을("a", "b", "c"...)을 Sequences 리스트에 추가함. 
                #이때, DFS를 실행하며 pop하고 남은 Digits와 값이 추가된 Sequences리스트를 input값으로 함

    def letterCombinations(self, digits: str) -> List[str]:
        if not digits: # example 2처럼 digits 없으면 빈 리스트 리턴
            return []
        
        Digits = list(digits) 
        self.Answer = []
        self.lenChar = len(Digits)

        # Dictionary 생성
        self.Dict = dict({
            '2':list("abc"),
            '3':list("def"),
            '4':list("ghi"),
            '5':list("jkl"),
            '6':list("mno"),
            '7':list("pqrs"),
            '8':list("tuv"),
            '9':list("wxyz")
        })
        
        self.DFS(Digits[:], []) # DFS 함수 실행(digits를 리스트로 변환한 전체값과 빈 Sequences 리스트를 input으로 함)
        return self.Answer
```

2. 938번
```python

v1_BFS(Breadth First Search: 너비 우선 탐색)

class Solution:
    def rangeSumBST(self, root: Optional[TreeNode], low: int, high: int) -> int:
        Answer = 0
        Pointer = root
        Queue = [Pointer]
        while Queue:
            # print([Idx.val for Idx in Queue]) -> root부터 그 다음 깊이(행?) 노드들, 그 다음 그 다음 깊이 노드들 탐색
            Queue_size = len(Queue)
            # 해당 Depth 만큼 pop 하면서 갈 수 있는 하위 Node로 BFS 실행
            for index in range(Queue_size): # while로 해도 됨
                Node = Queue.pop(0)
                if low <= Node.val <= high:
                    Answer += Node.val
                if Node.left:
                    Queue.append(Node.left)
                if Node.right:
                    Queue.append(Node.right)
        return Answer

v2_DFS(Depth First Search: 깊이 우선 탐색)

class Solution:

    def DFS(self, node, low, high):
        if not node:
            return 0
        myReturn = 0  # 초기값 설정
        
        if node.val >= low and node.val <= high:
            myReturn += node.val
        # 가장 깊이 있는 노드(아래 있는)부터 탐색 
        myReturn += self.DFS(node.left,  low, high)
        myReturn += self.DFS(node.right, low, high)

        
        return myReturn
    
    def rangeSumBST(self, root: Optional[TreeNode], low: int, high: int) -> int:
        
        return self.DFS(root, low, high)
```
        
3. DFS와 BFS 비교

- DFS
  - 현재 정점에서 최대한 갈 수 있는 점들까지 탐색한 후 가장 가까운 갈림길로 리턴하여 다시 탐색
  - 모든 노드 방문
  - 검색 속도는 BFS보다 느림
  - 각 경로마다 특징을 저장해둬야 할 떄는 DFS를 사용
  - 스택 또는 재귀함수로 구현

- BFS
  - 현재 정점에서 가까운 노드부터 탐색
  - 큐를 이용해 구현
  - 최단거리를 구해야 할 때는 BFS가 유리