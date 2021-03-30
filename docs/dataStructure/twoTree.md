# 二叉树

[参考资料](http://www.conardli.top/docs/dataStructure/)
##  基本操作
- 第n层的节点数最多为2n个节点
- n层二叉树最多有20+...+2n=2n+1-1个节点
- 第一个非叶子节点：length/2
- 一个节点的孩子节点：2n、2n+1

### 基本结构
插入，遍历，深度
```js
function Node(data, left, right) {
    this.data = data;
    this.left = left;
    this.right = right;
}

Node.prototype = {
    show: function () {
        console.log(this.data);
    }
}

function Tree() {
    this.root = null;
}

Tree.prototype = {
    insert: function (data) {
        var node = new Node(data, null, null);
        if (!this.root) {
            this.root = node;
            return;
        }
        var current = this.root;
        var parent = null;
        while (current) {
            parent = current;
            if (data < parent.data) {
                current = current.left;
                if (!current) {
                    parent.left = node;
                    return;
                }
            } else {
                current = current.right;
                if (!current) {
                    parent.right = node;
                    return;
                }
            }

        }
    },
    preOrder: function (node) {
        if (node) {
            node.show();
            this.preOrder(node.left);
            this.preOrder(node.right);
        }
    },
    middleOrder: function (node) {
        if (node) {
            this.middleOrder(node.left);
            node.show();
            this.middleOrder(node.right);
        }
    },
    laterOrder: function (node) {
        if (node) {
            this.laterOrder(node.left);
            this.laterOrder(node.right);
            node.show();
        }
    },
    getMin: function () {
        var current = this.root;
        while(current){
            if(!current.left){
                return current;
            }
            current = current.left;
        }
    },
    getMax: function () {
        var current = this.root;
        while(current){
            if(!current.right){
                return current;
            }
            current = current.right;
        }
    },
    getDeep: function (node,deep) {
        deep = deep || 0;
        if(node == null){
            return deep;
        }
        deep++;
        var dleft = this.getDeep(node.left,deep);
        var dright = this.getDeep(node.right,deep);
        return Math.max(dleft,dright);
    }
}
```
```js
    var t = new Tree();
    t.insert(3);
    t.insert(8);
    t.insert(1);
    t.insert(2);
    t.insert(5);
    t.insert(7);
    t.insert(6);
    t.insert(0);
    console.log(t);
    // t.middleOrder(t.root);
    console.log(t.getMin(), t.getMax());
    console.log(t.getDeep(t.root, 0));
    console.log(t.getNode(5,t.root));
```
### 树查找
```js
    getNode: function (data, node) {
        if (node) {
            if (data === node.data) {
                return node;
            } else if (data < node.data) {
                return this.getNode(data,node.left);
            } else {
                return this.getNode(data,node.right);
            }
        } else {
            return null;
        }
    }
```
### 二分查找
二分查找的条件是必须是有序的线性表。

和线性表的中点值进行比较，如果小就继续在小的序列中查找，如此递归直到找到相同的值。
```js
    function binarySearch(data, arr, start, end) {
        if (start > end) {
            return -1;
        }
        var mid = Math.floor((end + start) / 2);
        if (data == arr[mid]) {
            return mid;
        } else if (data < arr[mid]) {
            return binarySearch(data, arr, start, mid - 1);
        } else {
            return binarySearch(data, arr, mid + 1, end);
        }
    }
    var arr = [0, 1, 1, 1, 1, 1, 4, 6, 7, 8]
    console.log(binarySearch(1, arr, 0, arr.length-1));
```

## 中序遍历
```js
    var inorderTraversal = function (root, array = []) {
      if (root) {
        inorderTraversal(root.left, array);
        array.push(root.val);
        inorderTraversal(root.right, array);
      }
      return array;
    };
```
## 前序遍历
```js
    var preorderTraversal = function (root, array = []) {
      if (root) {
        array.push(root.val);
        preorderTraversal(root.left, array);
        preorderTraversal(root.right, array);
      }
      return array;
    };
```
## 后序遍历
```js
    var postorderTraversal = function (root, array = []) {
      if (root) {
        postorderTraversal(root.left, array);
        postorderTraversal(root.right, array);
        array.push(root.val);
      }
      return array;
    };
```





