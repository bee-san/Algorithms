# Binary Trees

## Preorder Traversal

Pre-order traversal is to visit the root first. Then traverse the left subtree. Finally, traverse the right subtree.

Basically, visits its current node before its child node \(hence pre-order\)

Pre-order is implemented as a **queue** in iterative.

Used to create a copy of the tree or get prefix traversal.

[Queues](https://www.notion.so/Queues-d13db071cec84bafb019b1e5bd15dd53)

```text
fn preOrderTrav(TreeNode Node){
	if node != None:
		visit(node);
		preOrderTrav(node.left)
		preOrderTrav(node.right)
}
```

## In-order traversal

In-order traversal is to traverse the left subtree first. Then visit the root. Finally, traverse the right subtree.

In-order is implemented as a **stack** in iterative.

When performed on a binary search tree, it **visits the nodes in ascending order** \(hence the name in-order\)

[Stacks](https://www.notion.so/Stacks-c925d73b270d460288c7b00ce2b18a06)

```text
fn inOrderTrav(TreeNode node){
	if node != None:
		inOrderTrav(node.left)
		visit(node)
		inOrderTrav(node.right)
}
```

## Post Order

Visits current node after its child nodes \(post-order, as it does its node post\)

In a post order, the root is always visited last.

Used to delete trees or postfix expression.

```text
fn postTrav(TreeNode node){
	postTrav(node.left)
	postTrav(node.right)
	visit(node)
}
```

