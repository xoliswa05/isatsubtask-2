// converter_extended.cpp
#include <iostream>
#include <string>
#include <algorithm>

// Decimal to binary (returns string)
std::string decimalToBinary(unsigned long long n) {
    if (n == 0) return "0";
    std::string bin;
    while (n > 0) {
        bin.push_back(char('0' + (n % 2)));
        n /= 2;
    }
    std::reverse(bin.begin(), bin.end());
    return bin;
}

// Binary to decimal
unsigned long long binaryToDecimal(const std::string &s) {
    unsigned long long result = 0;
    for (char c : s) {
        if (c != '0' && c != '1') continue;
        result = result * 2 + (c - '0');
    }
    return result;
}

void menu() {
    std::cout << "\n--- Converter Menu ---\n";
    std::cout << "1) Decimal -> Binary\n";
    std::cout << "2) Binary -> Decimal\n";
    std::cout << "3) Exit\n";
    std::cout << "Choose (1-3): ";
}

int main() {
    while (true) {
        menu();
        int opt;
        if (!(std::cin >> opt)) {
            std::cin.clear();
            std::string skip; std::getline(std::cin, skip);
            std::cout << "Invalid input.\n";
            continue;
        }
        if (opt == 1) {
            unsigned long long dec;
            std::cout << "Enter decimal number: ";
            if (!(std::cin >> dec)) {
                std::cin.clear();
                std::string skip; std::getline(std::cin, skip);
                std::cout << "Invalid decimal input.\n";
                continue;
            }
            std::cout << "Binary: " << decimalToBinary(dec) << '\n';
        } else if (opt == 2) {
            std::string bin;
            std::cout << "Enter binary number: ";
            std::cin >> bin;
            std::string clean;
            for (char c : bin) if (c == '0' || c == '1') clean.push_back(c);
            if (clean.empty()) {
                std::cout << "No valid binary digits found. Decimal = 0\n";
            } else {
                std::cout << "Decimal: " << binaryToDecimal(clean) << '\n';
            }
        } else if (opt == 3) {
            break;
        } else {
            std::cout << "Invalid option.\n";
        }
    }
    std::cout << "Exiting converter.\n";
    return 0;
}
