# leetcode144-binaryStack


iteration:

    class Solution:
        def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:

            stack = []
            output = []
            if root:
                stack.append(root)            // 第一个root
            while stack:                  // 当stack存在
                root = stack.pop()            // 每次pop出来的都是新的parent
                output.append(root.val)       // +到要看的集里
                if root.right:                // 有右边的值，+到 stack里
                    stack.append(root.right)  
                if root.left:                 // 有左边的值， +到stack里
                    stack.append(root.left)

            return output
            
            所以提取的时候先出来左边，再来右边。左边的变成下一个root，往下run
            
 
 recursion：
