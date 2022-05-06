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
