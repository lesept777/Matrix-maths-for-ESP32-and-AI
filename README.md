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
    Create a matrix from a C++ vector V, the content of the matrix is the same the same as the vector's
      MLMatrix M(V);
    Create a constant vector
      MLMatrix M(value, rows);
