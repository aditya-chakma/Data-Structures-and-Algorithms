# Union-Find (Disjoint Set Union)

The **Union-Find** data structure, also known as **Disjoint Set Union (DSU)** or **Merge-Find**, is a data structure that manages a collection of disjoint sets. It efficiently handles operations like finding the set to which an element belongs, merging two sets, and determining the number of connected components in a graph. These operations are typically performed in near-constant time, making Union-Find a powerful tool for many algorithms, particularly in graph theory.

## Base Class

The base class for the Union-Find data structure includes an array called `parent`, which keeps track of the parent (or representative) of each element. Initially, each element is its own parent, meaning each element is in its own set. The base class is defined as follows:

```Java
class DSU {

    private int[] parents;  // Array to store the parent of each element
    private int components;  // Number of disjoint sets (components)

    public DSU(int n) {
        this.components = n;  // Initially, each element is its own component
        this.parents = new int[n];

        for (int i = 0; i < n; i++) {
            this.parents[i] = i;  // Each element is its own parent initially
        }
    }
}
```

## Basic Operations

The Union-Find data structure supports the following basic operations:

- **Find(element)**: Finds the root (or representative) of the set containing the given element.
- **Union(element1, element2)**: Merges the sets containing the two elements.
- **Components()**: Returns the number of disjoint sets (components) in the data structure.

### Find(int el)

The `find` operation determines the root of the set containing the element `el`. This is done by recursively following the parent pointers until the root is reached.

```Java
public int find(int el) {
    if (parents[el] == el) {
        return el;  // If the element is its own parent, it is the root
    }

    return find(parents[el]);  // Recursively find the root
}
```

### Union(int el1, int el2)

The `union` operation merges the sets containing `el1` and `el2`. This is done by finding the roots of both elements and making one root the parent of the other. If the two elements are already in the same set, no action is taken.

```Java
public void union(int el1, int el2) {
    int parent1 = find(el1);  // Find the root of el1
    int parent2 = find(el2);  // Find the root of el2

    parents[parent1] = parents[parent2];  // Merge the sets

    if (parent1 != parent2) {
        components -= 1;  // Decrease the number of components if the sets were different
    }
}
```

### Components()

This method returns the current number of disjoint sets (components) in the data structure.

```Java
public int components() {
    return components;
}
```

### Examples

**Initial state:** Imagine we have a set of 5 elements, initially all disjoint (in their own sets). The `parent` array would look like this. This would represent each element pointing to itself:

```
parents:

0   1   2   3   4
|   |   |   |   |
0   1   2   3   4
```

**Union Operations**

Let's perform some `union` operations:

1. **Union(0, 1)**: We merge the sets containing elements 0 and 1. Let's say we make 1 the parent of 0.

   ```
   parents:

   0   1   2   3   4
   |   |   |   |   |
   1   1   2   3   4
   ```

2. **Union(2, 3)**: Merge sets containing 2 and 3, making 3 the parent of 2.

   ```
   parents:

   0   1   2   3   4
   |   |   |   |   |
   1   1   3   3   4
   ```

3. **Union(1, 3)**: Merge the sets containing 1 and 3. We can make 3 the parent of 1.

   ```
   parents:

   0   1   2   3   4
   |   |   |   |   |
   1   3   3   3   4
   ```

**Find Operation**

Now, if we perform `find(0)`, it will traverse through the parent pointers: 0 -> 1 -> 3. Therefore, `find(0)` returns 3, which is the root of the set containing 0. In worst case it would result in `O(n)` operations.

**Path Compression**

If we use path compression, after `find(0)`, the `parent` array would be optimized `O(1)`:

```
parents:

0   1   2   3   4
|   |   |   |   |
3   3   3   3   4
```

Now, 0 directly points to the root of its set.

**Union by Rank**

Union by rank helps keep the tree balanced. In our example, if we had used union by rank, the tree might have looked different, ensuring no element is too far from its root.

These diagrams illustrate the basic working of the Union-Find data structure. The actual implementation with optimizations can lead to more complex tree structures, but the underlying principle remains the same.

Let me know if you would like to explore a specific scenario or optimization in more detail!

## Optimizations

The basic implementation of Union-Find can be optimized to improve its efficiency. Two common optimizations are **path compression** and **union by rank**.

### Path Compression

Path compression is a technique that flattens the structure of the tree during the `find` operation, making future `find` operations faster. This is done by updating the parent of each visited node to point directly to the root.

```Java
public int find(int el) {
    if (parents[el] == el) {
        return el;  // If the element is its own parent, it is the root
    }

    return parents[el] = find(parents[el]);  // Path compression: update parent to root
}
```

### Union by Rank

Union by rank is a technique that ensures that the smaller tree is always attached to the root of the larger tree during a `union` operation. This helps keep the tree balanced, reducing the time complexity of future operations.

```Java
class DSU {

    private int[] parents;
    private int components;
    private int[] rank;  // Array to store the rank (depth) of each set

    public DSU(int n) {
        this.rank = new int[n];
        this.components = n;
        this.parents = new int[n];

        for (int i = 0; i < n; i++) {
            this.parents[i] = i;  // Each element is its own parent initially
        }
    }

    public void union(int el1, int el2) {
        int parent1 = find(el1);  // Find the root of el1
        int parent2 = find(el2);  // Find the root of el2

        if (rank[parent1] > rank[parent2]) {
            parents[parent2] = parents[parent1];  // Attach the smaller tree to the larger one
            rank[parent1] += 1;  // Update the rank

        } else {
            parents[parent1] = parents[parent2];  // Attach the smaller tree to the larger one
            rank[parent2] += 1;  // Update the rank
        }

        if (parent1 != parent2) {
            components -= 1;  // Decrease the number of components if the sets were different
        }
    }
}
```

## Full Implementation

Combining all the optimizations, the full implementation of the Union-Find data structure is as follows:

```Java
class DSU {

    private int[] parents;  // Array to store the parent of each element
    private int components;  // Number of disjoint sets (components)
    private int[] rank;  // Array to store the rank (depth) of each set

    public DSU(int n) {
        this.rank = new int[n];
        this.components = n;
        this.parents = new int[n];

        for (int i = 0; i < n; i++) {
            this.parents[i] = i;  // Each element is its own parent initially
        }
    }

    public int find(int el) {
        if (parents[el] == el) {
            return el;  // If the element is its own parent, it is the root
        }

        return parents[el] = find(parents[el]);  // Path compression: update parent to root
    }

    public void union(int el1, int el2) {
        int parent1 = find(el1);  // Find the root of el1
        int parent2 = find(el2);  // Find the root of el2

        if (rank[parent1] > rank[parent2]) {
            parents[parent2] = parents[parent1];  // Attach the smaller tree to the larger one
            rank[parent1] += 1;  // Update the rank

        } else {
            parents[parent1] = parents[parent2];  // Attach the smaller tree to the larger one
            rank[parent2] += 1;  // Update the rank
        }

        if (parent1 != parent2) {
            components -= 1;  // Decrease the number of components if the sets were different
        }
    }

    public boolean sameSet(int el1, int el2) {
        return find(el1) == find(el2);  // Check if two elements are in the same set
    }

    public int components() {
        return components;  // Return the number of disjoint sets
    }
}
```

## Applications

The Union-Find data structure is widely used in various algorithms, including:

- **Kruskal's algorithm** for finding the minimum spanning tree of a graph.
- **Detecting cycles** in an undirected graph.
- **Connected components** in a graph.
- **Image processing** for labeling connected regions.

## Conclusion

The Union-Find data structure is a powerful tool for managing disjoint sets with efficient operations. By using optimizations like path compression and union by rank, the time complexity of these operations can be reduced to near-constant time, making it suitable for large-scale applications.
