# 수업 내용 복습
## python 활용 알고리즘(Leetcode_Tree traversal)

1. 589. N-ary Tree Preorder Traversal
```python
Version 1

class Solution:
    def DFS(self, Node):
        if not Node:
            return
        print(Node.val)
        self.Answer.append(Node.val)
        for child in Node.children:
            self.DFS(child)
    def preorder(self, root: 'Node') -> List[int]:
        self.Answer = []
        self.DFS(root)
        return self.Answer

Version 2

class Solution:
    def preorder(self, root: 'Node') -> List[int]:
        output = []
        
        def dfs(node):
            if not node: return
            output.append(node.val)
            for c in node.children:
                dfs(c) 
                
        dfs(root)
        
        return output

# v1과 다르게 v2에서는 변수 앞에 self를 붙이지 않는데, 이렇게 했을 경우 다른 함수에서 접근할 수 없음. 또한, 함수가 한번 실행된 후 변수는 사라짐

# dfs함수를 재귀적으로 활용
```
2. 590. N-ary Tree Postorder Traversal
```python
Version 1
# 589의 V1과 append식의 위치만 다름. 위에서는 DFS함수를 호출하면서 넣은 child 값이 append가 이미 되어 상위 노드부터 들어가지만, 아래 식에서는 DFS 재귀함수를 실행한 후의 value를 append하여 맨 아래 child부터 추가됨

class Solution:
    def DFS(self, Node):
        if not Node:
            return
        for child in Node.children:
            self.DFS(child)
        print(Node.val)
        self.Answer.append(Node.val)
    def postorder(self, root: 'Node') -> List[int]:
        self.Answer = []
        self.DFS(root)
        return self.Answer

Version 2

class Solution:
    def postorder(self, root: 'Node') -> List[int]:
        
        if not root:
            return []

        result = []
        
        for child in root.children:
            result.extend(self.postorder(child)) # extend를 이때 해줌으로써 5,6부터 입력
            
        print(result)
        # 맨 상위 노드 밸류를 더해주기
        return result + [root.val]
# V1이 V2보다 빠름
```
