# scientific-calci-
c++ source code of scientific calculator
#include <iostream>
#include <cmath>
using namespace std;

class ScientificCalculator {
public:
    // Constructor
    ScientificCalculator() : result(0.0), inputMode('r') {} // Initialize result and inputMode

    // Function to perform basic arithmetic operations
    void performOperation(char operation, double operand) {
        switch (operation) {
            case '+':
                result += operand;
                break;
            case '-':
                result -= operand;
                break;
            case '*':
                result *= operand;
                break;
            case '/':
                if (operand != 0) {
                    result /= operand;
                } else {
                    cout << "Error: Division by zero." << endl;
                }
                break;
            default:
                cout << "Error: Invalid operation." << endl;
                break;
        }
    }

    // Function to perform scientific operations
    void performScientificOperation(const string& operation) {
        if (operation == "sin" || operation == "cos" || operation == "tan") {
            char trigInputMode;
            cout << "Enter input mode ('r' for radians, 'd' for degrees): ";
            cin >> trigInputMode;

            setInputMode(trigInputMode);
        }

        if (operation == "sin") {
            double angle;
            cout << "Enter the angle: ";
            cin >> angle;

            result = sin(convertInput(angle));
        } else if (operation == "cos") {
            double angle;
            cout << "Enter the angle: ";
            cin >> angle;

            result = cos(convertInput(angle));
        } else if (operation == "tan") {
            double angle;
            cout << "Enter the angle: ";
            cin >> angle;

            result = tan(convertInput(angle));
        } else if (operation == "log") {
            result = log(result);
        } else if (operation == "sqrt") {
            result = sqrt(result);
        } else if (operation == "exp") {
            result = exp(result);
        } else if (operation == "inv") {
            if (result != 0) {
                result = 1.0 / result;
            } else {
                cout << "Error: Division by zero." << endl;
            }
        } else if (operation == "pi") {
            result = M_PI; // M_PI is a constant for pi in the cmath library
        } else if (operation == "e") {
            result = M_E; // M_E is a constant for Euler's number in the cmath library
        } else {
            cout << "Error: Invalid scientific operation." << endl;
        }
    }

    // Function to set input mode
    void setInputMode(char mode) {
        if (mode == 'r' || mode == 'd') {
            inputMode = mode;
        } else {
            cout << "Error: Invalid input mode." << endl;
        }
    }

    // Function to convert input based on the selected mode
    double convertInput(double value) {
        if (inputMode == 'd') {
            // Convert degrees to radians
            return value * M_PI / 180.0;
        } else {
            // Input is in radians
            return value;
        }
    }

    // Function to get the current result
    double getResult() const {
        return result;
    }

private:
    double result;
    char inputMode; // 'r' for radians, 'd' for degrees
};

int main() {
    ScientificCalculator calculator;

    string operationType;
    double operand;

    cout << "Enter an operation type (+, -, *, /, sin, cos, tan, log, sqrt, exp, inv, pi, e): ";
    cin >> operationType;

    // Check if the operation is a basic arithmetic operation
    if (operationType == "+" || operationType == "-" || operationType == "*" || operationType == "/") {
        // Get the first operand
        cout << "Enter the first operand: ";
        cin >> operand;
        calculator.performOperation(operationType[0], operand);

        // Get the second operand
        cout << "Enter the second operand: ";
        cin >> operand;
        calculator.performOperation(operationType[0], operand);
    }
    // For other operations, prompt for input based on the operation
    else {
        calculator.performScientificOperation(operationType);
    }

    // Display the result
    cout << "Result: " << calculator.getResult() << endl;

    return 0;
}
