# Gauss Elimination Method in MATLAB

This MATLAB code solves a system of linear equations using the Gauss elimination method with partial pivoting.

## Code

```matlab
A = [10, 8, -3, 1, 16;
      2, 10, 1, -4, 9;
      3, -4, 10, 1, 10;
      2, 2, -3, 10, 11];
n = 4;

for i = 1:n-1
    [max_val, pivot_row] = max(abs(A(i:n, i)));
    pivot_row = pivot_row + i - 1;
    if pivot_row ~= i
        A([i, pivot_row], :) = A([pivot_row, i], :);
    end
    if A(i, i) == 0
        error('No unique solution exists.');
    end
    for j = i+1:n
        factor = A(j, i) / A(i, i);
        A(j, :) = A(j, :) - factor * A(i, :);
    end
end

if A(n, n) == 0
    error('No unique solution exists.');
end

x = zeros(n, 1);
x(n) = A(n, n+1) / A(n, n);
for i = n-1:-1:1
    x(i) = (A(i, n+1) - A(i, i+1:n) * x(i+1:n)) / A(i, i);
end

disp('The solution is:');
disp(x);
