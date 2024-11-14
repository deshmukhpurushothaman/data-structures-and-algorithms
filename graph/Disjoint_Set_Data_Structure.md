# Disjoint Set Data Structure

The **Disjoint Set Union (DSU)** or **Union-Find** is a data structure that keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets. It supports two key operations:

1. **Find**: Determine which subset a particular element is in.
2. **Union**: Join two subsets into a single subset.

## Optimizations

- **Union by Rank/Size**: Optimizes the union operation by attaching smaller trees under the root of larger trees to keep the tree flat.
- **Path Compression**: Optimizes the find operation by making nodes on the path point directly to the root, flattening the structure.

---

## Code Implementation (JavaScript)

### Union-Find with Union by Rank and Path Compression

```javascript
class DisjointSet {
  constructor(n) {
    this.parent = Array.from({ length: n }, (_, i) => i);
    this.rank = new Array(n).fill(0);
  }

  find(node) {
    if (this.parent[node] !== node) {
      // Path compression
      this.parent[node] = this.find(this.parent[node]);
    }
    return this.parent[node];
  }

  union(x, y) {
    const rootX = this.find(x);
    const rootY = this.find(y);

    if (rootX !== rootY) {
      // Union by rank
      if (this.rank[rootX] < this.rank[rootY]) {
        this.parent[rootX] = rootY;
      } else if (this.rank[rootX] > this.rank[rootY]) {
        this.parent[rootY] = rootX;
      } else {
        this.parent[rootY] = rootX;
        this.rank[rootX]++;
      }
    }
  }
}

// Example usage
const ds = new DisjointSet(7);
ds.union(0, 1);
ds.union(1, 2);
ds.union(3, 4);
ds.union(4, 5);
ds.union(5, 6);

console.log(ds.find(0)); // Output: Root of 0's set (compressed path)
console.log(ds.find(6)); // Output: Root of 6's set (compressed path)
```

### Union-Find with Union by Size and Path Compression

In this variation, we use the size of the sets to determine which tree becomes the root during union.

```javascript
class DisjointSetSize {
  constructor(n) {
    this.parent = Array.from({ length: n }, (_, i) => i);
    this.size = new Array(n).fill(1);
  }

  find(node) {
    if (this.parent[node] !== node) {
      // Path compression
      this.parent[node] = this.find(this.parent[node]);
    }
    return this.parent[node];
  }

  union(x, y) {
    const rootX = this.find(x);
    const rootY = this.find(y);

    if (rootX !== rootY) {
      // Union by size
      if (this.size[rootX] < this.size[rootY]) {
        this.parent[rootX] = rootY;
        this.size[rootY] += this.size[rootX];
      } else {
        this.parent[rootY] = rootX;
        this.size[rootX] += this.size[rootY];
      }
    }
  }
}

// Example usage
const dsSize = new DisjointSetSize(7);
dsSize.union(0, 1);
dsSize.union(1, 2);
dsSize.union(3, 4);
dsSize.union(4, 5);
dsSize.union(5, 6);

console.log(dsSize.find(0)); // Output: Root of 0's set (compressed path)
console.log(dsSize.find(6)); // Output: Root of 6's set (compressed path)
```

---

## Explanation

### Path Compression

- When calling `find()`, we make the node point directly to the root of its set, reducing the tree's height.
- This ensures that subsequent queries for the same node are faster.

### Union by Rank/Size

- **Union by Rank:** Attach smaller ranked trees under the root of larger ranked trees.
- **Union by Size:** Attach smaller-sized sets under larger-sized sets.
- This optimization prevents the tree from becoming too tall, maintaining efficient `O(log N)` operations.

## Complexity

- **Time Complexity:** Near constant time, often referred to as **amortized O(α(N))**, where α is the inverse Ackermann function (very slow-growing and nearly constant for practical purposes).
- **Space Complexity:** **O(N)** for storing parent and rank/size arrays.
