#Tree

트리([[Tree]]) 중에서 가장 널리 사용되는 트리 자료구조는 이진 트리와 이진 탐색 트리([[Binary Search Tree]])이다. 이진 트리는 왼쪽, 오른쪽, 최대 2개의 자식을 갖는 단순한 형채로, 다진 트리에 비해 훨씬 간결하다.
>대체로 트리라고 하면 특별한 경우가 아닌 이상, 대부분 이진트리를 일컫는다.

# 이진 트리의 유형
- **정 이진 트리** : 모든 노드가 0개 또는 2개의 자식 노드를 가진다.
- **완전 이진 트리** : 마지막 레벨을 제외하고 모든 레벨이 완전히 채워져 있으며, 마지막 레벨의 모든 노드는 가장 왼쪽에 위치한다.
- **포화 이진 트리** : 모든 노드가 2개의 자식 노드를 가지고 있으며, 모든 리프 노드가 동일한 깊이 또는 레벨을 갖는다.
# 이진 트리의 최대 깊이
이진 트리의 깊이는 BFS로 구할 수 있다.
BFS는 재귀가 아닌 반복 구조로 풀이할 수 있다. 추가로, DFS는 스택, BFS는 큐를 사용해서 구현한다.
```python
def max_depth(self, root: TreeNode) -> int:
	queue = collections.deque([root])
	depth = 0
	
	while queue:
		...
	return depth
```
>`dequeue` 자료형을 사용하면 이중 연결 리스트로 구성되어 있기 때문에 큐와 스택 연산을 모두 자유롭게 활용할 수 있으며, 양방향 모두 *O(1)*에 추출할 수 있다,
```python
import collections


class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def max_depth(self, root: TreeNode) -> int:
    if root is None:
        return 0

    queue = collections.deque([root])
    depth = 0

    while queue:
        depth += 1
        for _ in range(len(queue)):
            cur_root = queue.popleft()
            if cur_root.left:
                queue.append(cur_root.left)
            if cur_root.right:
                queue.append(cur_root.right)
    return depth
```
