#include <iostream>
#include <cmath>
#include <algorithm>
#include <vector>

int findfreedigit(std::vector<int> digits) {
    for (int i = 0; i < 10; ++i) 
        if (digits[i] == 0 && i != 0 && i != 2) return i;
    return -1;
}
bool analyzenumber(int64_t num) {
    while (num) {
        if (num % 10 == 2 || num % 10 == 0) return false;
        num /= 10;
    }
    return true;
}
void check_year(int64_t year) {
    if (year > pow(10,8)) {
        std::cout << -1 << '\n';
        exit(1);
    }
}
int main() {
    int64_t year;
    std::cin >> year;
    check_year(year);
    int64_t oldyear = year;
    std::vector<int> newyear;
    bool if_analyze_return_false = false;
    std::vector<int> newyear_buffer;
    std::vector<int> digits(10);
if_analize_return_false:
    if (if_analyze_return_false) {
        year = oldyear;
        year++;
    }
    int64_t newyearcome = 0;
    int pos_buffer_9 = 0;
    //differentiation on digits
    while (year) {
        newyear.push_back(year % 10);
        year /= 10;
    }
    reverse(newyear.begin(), newyear.end());
    bool check = false;
tryagain:
    for (int i = 0; i < newyear.size(); ++i) {
        check_year(newyearcome);
        if (check) {
            for (int l = i; l < newyear.size(); ++l) {
                newyear[l] = findfreedigit(digits);
                if (newyear[l] == -1) {
                    std::cout << -1 << '\n';
                    exit(1);
                } else digits[newyear[l]]++;
                newyearcome += pow(10, newyear.size() - 1 - l) * newyear[l];
                check_year(newyearcome);
            }
            break;
        } else if (newyear[i] == 0 || newyear[i] == 2 || digits[newyear[i]] > 0) {
            int count = 0;
            while (count <= 10) {
                newyear[i]++;
                if (newyear[i] != 2 && newyear[i] != 10 && digits[newyear[i]] == 0) {
                    newyearcome += pow(10,newyear.size() - 1 - i) * newyear[i];
                    digits[newyear[i]]++;
                    newyear_buffer.push_back(newyear[i]);
                    check = true;
                    break;
                } else if (newyear[i] == 10) { //critical case
                    for (int j = newyear_buffer.size() - 1; j >= 0; --j) {
                        digits[newyear_buffer[j]]--;
                        newyear_buffer[j]++;
                        if (digits[newyear_buffer[j]] && newyear_buffer[j] < 10) {
                            bool check_2 = false;
                            while(!check_2) {
                                newyear_buffer[j]++;
                                if (newyear_buffer[j] < 10 && digits[newyear_buffer[j]] == 0) check_2 = true;
                                if (newyear_buffer[j] == 10) check_2 = true;
                            }
                        }
                        if (j == 0 && newyear_buffer[j] == 10) {
                            newyear_buffer.clear();
                            for (auto &i : digits) i = 0;
                            newyear.push_back(0);
                            newyearcome = 0;
                            for (int k = 0; k < newyear.size(); ++k) {
                                newyear[k] = 0;
                                digits[newyear[k]]++;
                            }
                            check = true;
                            goto tryagain;
                        } else if (newyear_buffer[j] == 10) {
                            pos_buffer_9 = j;
                        } else {
                            newyearcome = 0;
                            for (auto &i : digits) i = 0;
                            if (newyear_buffer[j] == 2) newyear_buffer[j]++;
                            for (int z = 0; z < newyear_buffer.size(); ++z) {
                                if (z >= pos_buffer_9 && pos_buffer_9 != 0) {
                                    newyear_buffer[z] = findfreedigit(digits);
                                    if (newyear_buffer[z] == -1) {
                                        std::cout << -1 << '\n';
                                        exit(1);
                                    }
                                    newyearcome += pow(10,newyear.size() - 1 - z) * newyear_buffer[z];
                                    digits[newyear_buffer[z]]++;
                                } else {
                                    newyearcome += pow(10, newyear.size() - 1 - z) * newyear_buffer[z];
                                    digits[newyear_buffer[z]]++;
                                }
                            }
                            check = true;
                            break;
                        }
                    }
                    newyear[i] = findfreedigit(digits);
                    if (newyear[i] == -1) {
                        std::cout << -1 << '\n';
                        exit(1);
                    } else {
                        digits[newyear[i]]++;
                        newyearcome += pow(10, newyear.size() - 1 - i) * newyear[i];
                    }
                    break;
                }
                count++;
            }
        } else {
            newyearcome += pow(10,newyear.size() - 1 - i) * newyear[i];
            newyear_buffer.push_back(newyear[i]);
            digits[newyear[i]]++;
        }
    }
    if (newyearcome == oldyear) {
        newyearcome = oldyear + 1;
        if (!analyzenumber(newyearcome)) {
            for (auto &i : digits) i = 0; 
            newyear_buffer.clear();
            newyear.clear();
            if_analyze_return_false = true;
            goto if_analize_return_false;
        }
    }
    check_year(newyearcome);
    std::cout << newyearcome << '\n';
}
