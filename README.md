# Matrix-maths-for-ESP32-and-AI
Matrix maths for ESP32 and AI

This library was developed with utility functions useful in my MLP library.

# List of methods
## Constructors
    Create an empty matrix (container)
      MLMatrix M();
    Create a constant matrix, size rows, cols, value is zero by default
      MLMatrix M(rows, cols, value);
    Create a random matrix, values between min and max
      MLMatrix M(rows, cols, min, max);
    Create a new matrix, copied from another one
      MLMatrix M(A);
    Create a new matrix, same size as another one, filled with a constant value
      MLMatrix M(A, value);
    Create a matrix from a C++ vector V, the content of the matrix is the same as the vector's
      MLMatrix M(V);
    Create a constant vector
      MLMatrix M(value, rows);
    Create identity matrix
      Id (size);
      
## Operations
Operators are overloaded.
### Assign
You can assign a vector (std::vector) or an array to a matrix
```
float x[3] = {1, 2, 3};
MLMatrix<float> M(3, 1, 0);
M = x;
```

### Matrix operations
* Addition, substraction, mulitplication of matrices
```
M = A + B;
M *= C;
```
* Matrix and scalar operations: `M = A * 2;`
* Matrix vector multiplication: `M = A * V;`
* Matrix transposition: `M = A.transpose();`
* Hadamard (point wise) product: `M = A.Hadamard(B);`

### Vector operations
Here vectors are matrices of size (rows, 1).
* Dot product: 
```
  std::vector<int> v1 = {1, 2, 3};
  std::vector<int> v2 = {4, 5, 6};
  MLMatrix<int> mv1(3, 1, 0);
  mv1 = v1;
  MLMatrix<int> mv2(3, 1, 0);
  mv2 = v2;
  int P = mv1.MdotProd(mv2, true);
```
The second argument (optional) is a boolean: if set to `true` it prevents `NaN` or overflows.

### Comparison
Comparison operators are : `==`, `!=`, `<` and `>=`. The 2 first operators return a boolean value, the others return a boolean matrix.

## Accessing elements
Access elements of a matrix using parenthesis:
```
MLMatrix<float> M(3, 3, -1, 1); // random matrix
Serial.println(M(1,2));
float x = M(0,0);
M(2,1) = 3;
```

## Utilities
### Dimensions
* Number of rows: `M.get_rows()`
* Number of comumns: `M.get_cols()`

### Norms
* L0 norm: `int L0 = M.L0norm();`
* L1 norm: `float L1 = M.L1norm();`
* L2 norm: `float L2 = M.L2norm();`

### Special values
* Mean: `float mean = M.mean();`
* Standard deviation: `float stdev = M.stdev(mean);`
* Min value: `float val = M.min();`
* Max value: `float val = M.max();`
* Min index: `M.indexMin(index_rows, index_cols)`
* Max index: `M.indexMax(index_rows, index_cols)`

### Extraction
* Extract a row: `row(number)`
```MLMatrix<float> M(5, 5, 0, 1); // random values between 0 and 1
MLMatrix<float> R(5, 1);
R = M.row(3);
```
* Extract a column: `col(number)`
* Sub matrix: `subMatrix(row_from, row_number, col_from, col_number)`

## Display a matrix
To display only the size: `M.printSize();`
To display the entire matrix: `M.print();`

