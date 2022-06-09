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
    Create a matrix from a C++ vector V of vectors, each vector is a row of the matrix
      MLMatrix M(V);
    Create a matrix from an array A of size s, the content of the matrix is the same as the array's
      MLMatrix M(A, s);
    Create a constant vector
      MLMatrix M(value, rows);
    Create identity matrix
      Id (size);


## Operations

Operators are overloaded.

### Assign

You can assign a vector (std::vector) or an array to a matrix:

```
float x[3] = {1, 2, 3};
MLMatrix<float> M(x, 3); // assigns the array to the matrix

std::vector<float> v;
v.assign(x, x+3);        // copies the array into the vector
MLMatrix<float> U(v);    // assigns the vector to the matrix
MLMatrix<float> X = v;   // this works also
```

No need to tell the dimensions, it's automatic!

### Matrix operations

- Addition, substraction, mulitplication of matrices

```
M = A + B;
M *= C;
```

- Matrix and scalar operations: `M = A * 2;`
- Matrix vector multiplication: `M = A * V;`
- Matrix transposition: `M = A.transpose();`
- Hadamard (point wise) product: `M = A.Hadamard(B);`

### Vector operations

Here vectors are matrices of size (rows, 1).

- Dot product (of vectors defined as MLMatrix):

```
  std::vector<int> v1 = {1, 2, 3};
  std::vector<int> v2 = {4, 5, 6};
  MLMatrix<int> mv1(3, 1, 0);
  mv1 = v1;
  MLMatrix<int> mv2(3, 1, 0);
  mv2 = v2;
  int P = mv1.MdotProd(mv2, true);
```

- Dot product of `std::vector`: `X = dotProd(V1, V2, true)`

For both operations, the last argument (optional) is a boolean: if set to `true` it prevents `NaN` or overflows.

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

- Number of rows: `M.get_rows()`
- Number of comumns: `M.get_cols()`

### Norms

- L0 norm: `int L0 = M.L0norm();`
- L1 norm: `float L1 = M.L1norm();`
- L2 norm: `float L2 = M.L2norm();`

### Special values

- Mean: `float mean = M.mean();`
- Standard deviation: `float stdev = M.stdev(mean);`
- Min value: `float val = M.min();`
- Max value: `float val = M.max();`
- Min index: `M.indexMin(index_rows, index_cols)`
- Max index: `M.indexMax(index_rows, index_cols)`
- Sign: `M.sign()` creates a matrix of the same size with +1s or -1s depending on the sign of its elements
- Mean absolute value of a row: `float mean = M.meanRow(rowNumber);`

### Random matrix

To create a random matrix with normal distribution (mean, standard deviation):

```
MLMatrix<float> M(3, 3, 0);
M.randomNormal(1, 2);
```

Now M has mean = 1 and standard deviation = 2.

### Extraction / removal

- Extract a row: `row(number)`

```MLMatrix<float> M(5, 5, 0, 1); // random values between 0 and 1
MLMatrix<float> R(5, 1);
R = M.row(3);
```

- Extract a column: `col(number)`
- Sub matrix: `subMatrix(row_from, row_number, col_from, col_number)`
- Remove a row: `M.removeRow(rowNumber);`
- Remove a column: `M.removeCol(colNumber);`

## Display a matrix

To display only the size: `M.printSize();`

To display the entire matrix: `M.print();`

## Misc utilities

### Random change

To apply a random change to the values of a matrix: `M.randomChange(amplitude)` where amplitude is the 'percentage' of change.
`M.randomChange(0.1)` multiplies all the elements of M by a random number between 0.9 and 1.1 (up to + or - 10%).

### Clip & scale

- `M.clipToZero(threshold)` forces all elements less or equal to threshold to 0
- `M.clipMin(threshold)` forces all elements whose absolute value is less than threshold to threshold
- `M.clipMax(threshold)` forces all elements whose absolute value is higher than threshold to threshold
- `A = M.normScale(value);` scales the L2 norm of M to the passed value and creates a new matrix
- `M.normScale2(value)` only scales the matrix so that its L2 norm is eual to `value`

## Check

- Check if a row is full of 0s: `M.zeroRow(rowNumber)`
- Check if a column is full of 0s: `M.zeroCol(colNumber)`
- Count the number of 0s in a row: `M.countZeroRow(rowNumber)`
- Count the number of 0s in a column: `M.countZeroCol(colNumber)`

## Set values

- Set a row to all 0s: `M.setZeroCol(rowNumber)`
- Set a column to all 0s: `M.setZeroRow(colNumber)`
- Set a row to a constant value: `M.setRow(rowNumber, value)`
- Set a column to a constant value: `M.setcol(colNumber, value)`
- Replace a row with values from a 1D matrix: `M.setRowMat(rowNumber, Matrix1D)`
- Replace a column with values from a 1D matrix: `M.setColMat(colNumber, Matrix1D)`
