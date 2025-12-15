#include <iostream>
#include <iomanip>
using namespace std;

bool isValidTime(int time) {
    int hour = time / 100;
    int min  = time % 100;

    return (time >= 0 && time <= 2359 &&
            hour >= 0 && hour <= 23 &&
            min >= 0 && min <= 59);
}

double getRate(int time) {
    if (time >= 800 && time <= 1759)
        return 0.40;     // Day
    else if (time >= 1800 && time <= 2359)
        return 0.25;     // Evening
    else
        return 0.15;     // Off-peak
}

int main() {
    int startTime, minutes;

    cout << "Enter call start time (HHMM): ";
    cin >> startTime;

    cout << "Enter call duration (minutes): ";
    cin >> minutes;

    if (!isValidTime(startTime) || minutes <= 0) {
        cout << "Invalid input.\n";
        return 0;
    }

    double rate = getRate(startTime);
    double totalCost = rate * minutes;

    cout << fixed << setprecision(2);
    cout << "\nRate per minute: $" << rate << endl;
    cout << "Total cost: $" << totalCost << endl;

    return 0;
}

