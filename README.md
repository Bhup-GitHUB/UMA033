A = [10, 8, -3, 1, 16;
      2, 10, 1, -4, 9;
      3, -4, 10, 1, 10;
      2, 2, -3, 10, 11];
n = 4;

for k = 1:n-1
    [max_val, max_row] = max(abs(A(k:n, k)));
    max_row = max_row + k - 1;
    if max_row ~= k
        A([k, max_row], :) = A([max_row, k], :);
    end
    for i = k+1:n
        factor = A(i, k) / A(k, k);
        A(i, :) = A(i, :) - factor * A(k, :);
    end
end

x = zeros(n, 1);
x(n) = A(n, n+1) / A(n, n);
for i = n-1:-1:1
    x(i) = (A(i, n+1) - A(i, i+1:n) * x(i+1:n)) / A(i, i);
end

disp('The solution is:');
disp(x);
