# MPI Pipeline Pattern Project

## 1. Pattern Selection

### Pattern: Linear Pipeline (Pattern #6)

**Student number:** `61`

**Calculation:**
```
pattern = ((number / 4) % 10) + 1
        = ((61 / 4) % 10) + 1
        = (15 % 10) + 1
        = 5 + 1 = 6
```

**Pattern Description:**
The linear pipeline pattern organizes processes in a chain where data flows sequentially from process 0 to process N-1. Each process performs a specific computational stage and passes the result to the next process in the chain.
This pattern is suitable for problems with natural sequental dependencies.

## 2. Task Selection

## Task: Computing the n-th Derivative of a Function Using Numerical Differentiation

### Mathematical Problem Statement
For a given function f(x) and integer n ≥ 1, compute the value of the n-th derivative at point x₀:
```
f⁽ⁿ⁾(x₀) = dⁿf/dxⁿ at x = x₀
```

### Numerical Method
The second-order central difference formula is used:
```
f'(x) ≈ [f(x+h) - f(x-h)] / (2h)
```
where h is a small differentiation step.

For higher-order derivatives, we apply the recursive scheme:
```
f⁽ᵏ⁾(x) ≈ [f⁽ᵏ⁻¹⁾(x+h) - f⁽ᵏ⁻¹⁾(x-h)] / (2h)
```

### Example
For the function f(x) = x³ + 2x² + 3x + 4:
- f'(x) = 3x² + 4x + 3
- f''(x) = 6x + 4  
- f'''(x) = 6
- f⁽⁴⁾(x) = 0

At x = 1.0:
- f'(1.0) = 3(1)² + 4(1) + 3 = 10.0
- f''(1.0) = 6(1) + 4 = 10.0
- f'''(1.0) = 6.0

### Why This Task is Compatible with the Pipeline Pattern

#### 1. Natural Sequential Dependencies
To compute the 2nd derivative, you first need the 1st derivative. To compute the 3rd derivative, you first need the 2nd derivative. Each computation step depends directly on the previous result.

#### 2. Perfect Process Distribution
```
Process 0: f(x) → f'(x)     (1st derivative)
Process 1: f'(x) → f''(x)   (2nd derivative) 
Process 2: f''(x) → f'''(x) (3rd derivative)
...
Process k: f⁽ᵏ⁾(x) → f⁽ᵏ⁺¹⁾(x) ((k+1)-th derivative)
```

## 3. Data Type

### Selected Data Type: float

**Calculation:**
```
data_type = (number % 4) + 1
          = (61 % 4) + 1
          = 1 + 1 = 2 (float)
```

**Implementation Details:**
- All floating-point calculations use `float` precision
- MPI data type: `MPI_FLOAT`
- Function inputs and outputs are `float` type
- Intermediate results stored as `float`

**Advantages for This Task:**
- Sufficient precision for numerical differentiation
- Lower memory footprint compared to double precision
- Faster computation on many architectures
- Matches the precision requirements of the central difference method

### Implementation Specifics
- **Student Number**: 61
- **MPI Pattern**: #6 (Linear Pipeline)
- **Data Type**: `float`
- **Function**: f(x) = x³ + 2x² + 3x + 4
- **Test Point**: x = 1.0
- **Step Size**: h = 0.0001

This combination provides an excellent demonstration of the pipeline pattern while solving a meaningful mathematical problem with appropriate numerical precision and clear real-world applications in scientific computing.