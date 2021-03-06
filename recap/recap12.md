1. Tree
  - Computing Depth and Height
    * Depth
      ```java
      public int depth(Position<E> p) {
        if (isRoot(p)) return 0;
        return 1 + depth(parent(p));
      }
      ```
    * Height
      ```java
      public int height(Position<E> p) {
        int h = 0;
        for (Position<E> c: child(p)) {
          h = Math.max(h, 1 + height(c));
        }
        return h;
      }
      ```
  - Binary Tree
    * A binary tree is **proper** if each node has either zero or two children
    * Inorder Traversal Iteratively
      ```java
      public class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        TreeNode(int x) { val = x; }
      }
      ```
      ```
      /**
       * Store candidates in a stack
       * Store children from right to left
       * Store null if no left or right
       * Maintain a roots stack
       */
      while candidates is not empty:
        r = candisates.pop()
        if r is null:
          roots.pop() and add it to the result 
        else:
          if r has children:
            roots.push() and candidates.push()
          else:
            result.push(r)
            roots.pop() and add it to the result 
      ```

2. Priority Queue
  - Implementation
    * Entry
      ```java
      public interface Entry<K, V> {
        K getKey();
        V get Value();
      }
      ```
      ```java
      public interface PriorityQueue<K, V> {
        int size();
        boolean isEmpty();
        Entry<K,V> insert(K key, V value) throws IllegalArgumentException;
        Entry<K,V> min();
        Entry<K,V> removeMin();
      }
      ```
        * Comparable vs Comparator
          * Comparable follows **natural ordering**, `a.compareTo(b)`
          * Comparator follows some notion other than their natural ordering, e.g. which string is shorter, `compare(a, b)`
    * Comparators and the Priority Queue ADT
      ```java
      /**
       * Allow a default priority queue to instead rely on the natural ordering for the given keys 
       * Assuming those keys come from a comparable class
       */
       public class DefaultComparator<E> implements Comparator<E> {
         public int compare(E a, E b) throws ClassCastException {
           return ((Comparable<E>) a).compareTo(b);
         }
       }
      ```
    * Binary Heap
      * ArrayList representation
        ```java
        protected int parent(int j) { return (j−1) / 2; }
        protected int left(int j) { return 2*j + 1; }
        protected int right(int j) { return 2*j + 2; }
        protected boolean hasLeft(int j) { return left(j) < heap.size(); }
        protected boolean hasRight(int j) { return right(j) < heap.size(); }
        
        protected void upheap(int j) {
          while (j > 0) {
            int p = parent(j);
            if (compare(heap.get(j), heap.get(p)) >= 0) break;
            swap(j, p);
            j = p;
          }
        }
        
        protected void downheap(int j) {
          while (hasLeft(j)) {
            int leftIndex = left(j);
            int smallChildIndex = leftIndex;
            if (hasRight(j)) {
              int rightIndex = right(j);
              if (compare(heap.get(leftIndex), heap.get(rightIndex)) > 0) {
                smallChildIndex = rightIndex;
              }
            }
            if (compare(heap.get(j), heap.get(smallChildIndex)) < 0) break;
            swap(j, smallChildIndex);
            j = smallChildIndex;
          }
        }
        ```
      * Construct a heap, _O(N)_
        ```java
        /* Constructor */
        public HeapPriorityQueue(K[] keys, V[] values) {
          super();
          for (int j=0; j < Math.min(keys.length, values.length); j++) {
            heap.add(new PQEntry<>(keys[j], values[j]));
          }
          heapify();
        }
        
        protected void heapify() {
          int startIndex = parent(size()−1);
          for (int i = startIndex; i >= 0; i--) {
            downheap(i);
          }
        }
        ```
      
     
