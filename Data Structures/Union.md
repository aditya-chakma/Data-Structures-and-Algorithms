# Union Find

In computer science the **Union Find** or **Disjoint Set Union** or **Merge Find** data structure, is a Data structure that stores a collection of disjoin sets. Equivalently it stores a partion of a set into disjoint sets. This data structure allows us to find quickly if two elements belong to the same set, number of connected components in a graph and merge two sets into a single set. All in `O(1)`.

## Base Class

Let's define the base class first.

The base class contains an array of size `n` named `parent`, representing the parent of a set of nodes. This parent is the representator of a set. Each set is identified by a prent node. Initially the parent array is initialized with each node's number. Meaning each node is a separate component. The base class is definded as bellow:

```Java
class DSU {

    private int[] parents;
    private int components;

    public DSU(int n) {
        this.components = n;
        this.parents = new int[n];

        for (int i = 0; i < n; i++) {
            this.parents[i] = i;
        }
    }

}
```

## Basic methods

The DSU data structure provides some basic features.

- [Find(element)](#findint-el). Finds the parent of the element.
- [Union(element1, element2)](#unionint-el1-int-el2). Unions/Merges the two elements or simply say, puts them into the same set
- Components(). Returns the number of components in the constructed graph.

### Find(int el)

Finds the parent for an element.

```Java
public int find(int el) {
    if (parents[el] == el) {
        return el;
    }

    return find(parents[el]);
}
```

### Union(int el1, int el2)

Unions two elements into a single set. Each element set is represented by their parents. In order to merge element1 and element2, we set parent of element1 as parent of element2.

```Java
public void Union(int el1, int el2) {
    int parent1 = find(el1);
    int parent2 = find(el2);

    parents[parent1] = parents[parent2];

    if (parent1 != parent2) {
        components -= 1;
    }
}
```

### Components()

Return the number of componenets in the representing graph.

```Java
public int components() {
    return components;
}
```

## Can we do better?

### Path compression

```Java
public int find(int el) {
    if (parents[el] == el) {
        return el;
    }

    return parents[el] = find(parents[el]);
}
```

## Rank

```Java
class Union
```
