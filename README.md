# Experiment 4: Gauss Elimination Method  

## Part 2: Solving a Linear System using Gauss Elimination  

### Problem Statement  
Solve the following system of equations using **Gauss Elimination Method**:  

\[
10x + 8y - 3z + u = 16
\]
\[
2x + 10y + z - 4u = 9
\]
\[
3x - 4y + 10z + u = 10
\]
\[
2x + 2y - 3z + 10u = 11
\]

### MATLAB Code  
```matlab
function x = gauss_elimination(A)
    [n, m] = size(A);
    
    if m ~= n+1
        error('Invalid Augmented Matrix');
    end
    
    for i = 1:n
        [~, p] = max(abs(A(i:n, i)));
        p = p + i - 1;
        
        if A(p, i) == 0
            error('No unique solution exists');
        end
        
        if p ~= i
            A([i, p], :) = A([p, i], :);
        end
        
        for j = i+1:n
            m = A(j, i) / A(i, i);
            A(j, :) = A(j, :) - m * A(i, :);
        end
    end

    x = zeros(n, 1);
    for i = n:-1:1
        x(i) = (A(i, end) - A(i, i+1:n) * x(i+1:n)) / A(i, i);
    end
    
    disp('Solution:');
    disp(x);
end

A = [10 8 -3 1 16;
     2 10 1 -4 9;
     3 -4 10 1 10;
     2 2 -3 10 11];

gauss_elimination(A);
