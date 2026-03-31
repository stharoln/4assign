f = @kjy_202512345_func1;

% 1. 시각화
x_vals = linspace(0, 4, 1000);
y_vals = f(x_vals);

figure;
plot(x_vals, y_vals, 'LineWidth', 2);
grid on; hold on;
xlabel('x axis'); ylabel('f(x)');
title('f(x) = 0.3x - sin(2x) 분석');

root_val = fzero(f, 1.5);
plot(root_val, f(root_val), 'ro', 'MarkerSize', 10, 'DisplayName', 'Root');
fprintf('x=0 이외의 근: %.4f\n', root_val);

% 주어진 조건 설정
h_val = 100;
v0_val = 50;
g_val = 9.81;

% 함수 호출
times = kjy_202512345_func2(h_val, v0_val, g_val);

fprintf('도달 시간 1 (t1): %.4f 초\n', times(1));
fprintf('도달 시간 2 (t2): %.4f 초\n', times(2));

global V
V = 10; % 주어진 부피 10 in^3

f_opt = @kjy_202512345_func3;
[r_opt, A_min] = fminbnd(f_opt, 0.1, 10);
h_opt = (3 * V) / (pi * r_opt^2);

fprintf('최적 반지름 r: %.4f in\n', r_opt);
fprintf('최적 높이 h: %.4f in\n', h_opt);
fprintf('최소 표면적 A: %.4f in^2\n', A_min);

r_range = linspace(0.5, 5, 500);
A_vals = zeros(size(r_range));
for i = 1:length(r_range)
    A_vals(i) = f_opt(r_range(i));
end

figure;
plot(r_range, A_vals, 'LineWidth', 2); hold on;
plot(r_opt, A_min, 'ro', 'MarkerSize', 10, 'DisplayName', 'Optimal Point');
yline(A_min * 1.1, '--r', '10% Increase Line'); % 10% 증가 선
xlabel('Radius r (in)'); ylabel('Surface Area A (in^2)');
title('r에 따른 표면적 A의 변화 (민감도 조사)');
grid on;

A_limit = A_min * 1.1;
r_upper = fzero(@(r) f_opt(r) - A_limit, r_opt + 1);
r_lower = fzero(@(r) f_opt(r) - A_limit, r_opt - 0.5);

fprintf('면적이 10%% 증가하는 범위: %.4f in ~ %.4f in\n', r_lower, r_upper);
fprintf('최적값에서 벗어날 수 있는 정도: -%.4f / +%.4f in\n', r_opt-r_lower, r_upper-r_opt);

f4 = @(x) 10 * exp(-2 * x);

x_range = linspace(0, 2, 100);

% 3. y 값 계산
y_vals = f4(x_range);

% 4. 그래프 그리기
figure;
plot(x_range, y_vals, 'LineWidth', 2, 'Color', 'r');
grid on;
xlabel('x axis');
ylabel('f(x) = 10e^{-2x}');
title('Exponential Decay Function: 10e^{-2x}');

% 그래프 꾸미기 (선택 사항)
legend('10e^{-2x}');


f5 = @(x) 30.*x.^2 - 300.*x + 4;


x_plot = linspace(0, 10, 100);
y_plot = f5(x_plot);

figure;
plot(x_plot, y_plot, 'LineWidth', 2);
grid on; hold on;
xlabel('x'); ylabel('f(x)');
title('f(x) = 30x^2 - 300x + 4 그래프');


[x_min_f5, f_min_val] = fminbnd(f5, 0, 10);

% 결과 표시
plot(x_min_f5, f_min_val, 'ro', 'MarkerSize', 10, 'DisplayName', 'Minimum');
fprintf('정확한 최소값 위치 x: %.4f\n', x_min_f5);
fprintf('최소값 f(x): %.4f\n', f_min_val);
legend('f(x)', 'Minimum');

h = @(z) 6 * exp(z);
g = @(y) 3 * cos(y);
f = @(x) x.^2;

composite_func = @(x) h(g(f(x)));

x_range6 = linspace(0, 4, 500);
y_vals6 = composite_func(x_range6);

figure;
plot(x_range6, y_vals6, 'LineWidth', 2, 'Color', 'm');
grid on;
xlabel('x');
ylabel('h(g(f(x)))');
title('Composite Function Graph: 6e^{3cos(x^2)}');

legend('6e^{3cos(x^2)}');
