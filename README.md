# highpeak

#include <iostream>
#include <algorithm>
using namespace std;

struct Job {
int start, end, profit;
};

bool compare(Job a, Job b) {
return a.end < b.end;
}

int findMaxProfit(Job arr[], int n) {
sort(arr, arr+n, compare);
int dp[n];
dp[0] = arr[0].profit;
int maxProfit = dp[0];
int totalJobs = 1;
for (int i = 1; i < n; i++) {
dp[i] = arr[i].profit;
for (int j = 0; j < i; j++) {
if (arr[j].end <= arr[i].start) {
dp[i] = max(dp[i], dp[j] + arr[i].profit);
}
}
if (dp[i] > maxProfit) {
maxProfit = dp[i];
totalJobs = 1;
} else if (dp[i] == maxProfit) {
totalJobs++;
}
}
cout << "Lokesh can pick " << totalJobs << " jobs with a total earnings of " << maxProfit << endl;
return maxProfit;
}

int main() {
Job arr[] = {{1, 2, 50}, {3, 5, 20}, {6, 19, 100}, {2, 100, 200}};
int n = sizeof(arr)/sizeof(arr[0]);
int remainingJobs = n - findMaxProfit(arr, n);
cout << "This leaves " << remainingJobs << " jobs for other employees." << endl;
return 0;
}

