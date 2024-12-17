#include <iostream>
#include <cmath>
#include <iomanip>
#include <functional>

using namespace std;

// 前向差分法
double forward_diff(function<double(double)> f, double x, double h) {
    return (f(x + h) - f(x)) / h;
}

// 後向差分法
double backward_diff(function<double(double)> f, double x, double h) {
    return (f(x) - f(x - h)) / h;
}

// 中心差分法
double central_diff(function<double(double)> f, double x, double h) {
    return (f(x + h) - f(x - h)) / (2 * h);
}

int main() {
    cout << "============================================\n";
    cout << "        數值微分計算器 (C++版)              \n";
    cout << "============================================\n\n";

    // 讓使用者輸入函數類型
    cout << "選擇要微分的函數:\n";
    cout << "1. f(x) = x^2\n";
    cout << "2. f(x) = sin(x)\n";
    cout << "3. f(x) = e^x\n";
    cout << "4. 自定義函數 (需在程式內修改)\n";
    cout << "請輸入選項 (1-4): ";
    
    int choice;
    cin >> choice;

    // 定義函數
    function<double(double)> func;
    switch (choice) {
        case 1:
            func = [](double x) { return x * x; }; // f(x) = x^2
            break;
        case 2:
            func = [](double x) { return sin(x); }; // f(x) = sin(x)
            break;
        case 3:
            func = [](double x) { return exp(x); }; // f(x) = e^x
            break;
        default:
            cout << "無效選項，預設使用 f(x) = x^2\n";
            func = [](double x) { return x * x; };
    }

    // 使用者輸入微分點與步長
    double x0, h;
    cout << "\n請輸入微分點 x0: ";
    cin >> x0;
    cout << "請輸入步長 h (例如 0.01): ";
    cin >> h;

    // 計算數值微分
    double forward = forward_diff(func, x0, h);
    double backward = backward_diff(func, x0, h);
    double central = central_diff(func, x0, h);

    // 顯示結果
    cout << fixed << setprecision(6);
    cout << "\n計算結果:\n";
    cout << "前向差分法的導數近似值: " << forward << endl;
    cout << "後向差分法的導數近似值: " << backward << endl;
    cout << "中心差分法的導數近似值: " << central << endl;

    cout << "\n============================================\n";
    cout << "程式執行完畢，謝謝使用！\n";
    return 0;
}
