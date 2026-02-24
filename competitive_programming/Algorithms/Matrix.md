## Flattening matrix

Also called mapping a matrix between dimensions, this is a concept that can be used to traverse a matrix in a 1D or 2D array.
- 2D index -> 1D index
- 1D index -> 2D index

This operation is possible because it is how arrays are actually stored in memory.

Assume 4 x 4 matrix:

``` 
Row 0 → elements 0,1,2,3
Row 1 → elements 4,5,6,7
Row 2 → elements 8,9,10,11
Row 3 → elements 12,13,14,15
```

You can traverse with a nested for traversing row and columns, but you can apply this concept and just traversing the matrix as if it were an array.

Just for instance, we are going to say that we want to access to the element ***9***, in coordinates it'll be `(2,1)` and in index it is translate as 9 (0-based indexing)
### Convert (row, col) -> 1D index

Formula:
	index = row * cols + col

```
index = 2 * 4 + 1
index = 8 + 1
index = 9
```

# Convert 1D index -> (row, col)
Formula:
	row = index // cols
	col = index % cols

```
row = 9 // 4 = 2
col = 9 % 4 = 1
```

## Why this matters?
This "perspective" of matrices can help us to implement efficient algorithms. 
Here is a list of what you can do with this concept:
- Binary search on matrices
- Memory layout in C
- DP on grids
- Competitive programming tricks.
