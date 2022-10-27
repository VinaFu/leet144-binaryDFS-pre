# leetcode144-binaryStack


# iterative:

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
            
            key points:
            1) 所以提取的时候先出来左边，再来右边。左边的变成下一个root，往下run 
            2) 注意if里面是先放在stack里面，然后root=stack.pop()是在帮忙提取里面的值 
            
            
# Iterative- Simple:
     
        stack = [root]                    // 起始值为第一个root
        res = []
        
        while stack:
            cur = stack.pop()            // 每次拿出的值，加在res里面
            
            if cur:
                res.append(cur.val)      // 反正每次加cur.val
                stack.append(cur.right)
                stack.append(cur.left)
                
        return res
            
 
# recursion - simple：

        class Solution:
            def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:

                if not root:
                    return []

                return [root.val] + self.preorderTraversal(root.left) + self.preorderTraversal(root.right)
                
                这里的recursion是以一个三角形为单位：
                            root
                          /      \
                     root.left  root.right
                
                那么走到root.left的时候，重新跑一遍本程序，而此时的root = root.left
                            root（root.left above）
                          /      \
                     root.left  root.right
                   
                所以这个是dfv, 也是preorder。
                
                          
# recursion - 初学者：

                def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        
                    output = []
                    self.dfs(root, output)      // 这个功能我们写在下面
                    return output

                def dfs(self, root, output):   // 新定义的跑左跑右
                    if root:
                        output.append(root.val)   // 结果加上root.val
                        self.dfs(root.left, output)  //左边加到output后面？？？
                        self.dfs(root.right, output)

