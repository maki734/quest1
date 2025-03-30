#include <iostream>
#include <vector>
#include <climits>

using namespace std;

class SortingAlgorithms {
public:
    
    static void bubbleSort(vector<int>& arr, int& comparisons, int& swaps) {
        int n = arr.size();
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                comparisons++;
                if (arr[j] > arr[j + 1]) {
                    swap(arr[j], arr[j + 1]);
                    swaps++;
                }
            }
        }
    }

   
    static void selectionSort(vector<int>& arr, int& comparisons, int& swaps) {
        int n = arr.size();
        for (int i = 0; i < n - 1; i++) {
            int minIdx = i;
            for (int j = i + 1; j < n; j++) {
                comparisons++;
                if (arr[j] < arr[minIdx]) {
                    minIdx = j;
                }
            }
            if (minIdx != i) {
                swap(arr[i], arr[minIdx]);
                swaps++;
            }
        }
    }

  
    static void insertionSort(vector<int>& arr, int& comparisons, int& swaps) {
        int n = arr.size();
        for (int i = 1; i < n; i++) {
            int key = arr[i];
            int j = i - 1;
            comparisons++;
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                swaps++;
                j--;
            }
            arr[j + 1] = key;
        }
    }

    static void simpleSort(vector<int>& arr, int& comparisons, int& swaps) {
        selectionSort(arr, comparisons, swaps);  // Using Selection Sort as Simple Sort
    }

   
    static void display(const vector<int>& arr) {
        for (int num : arr) {
            cout << num << " ";
        }
        cout << endl;
    }

    static void compareEfficiency(int bubbleComparisons, int bubbleSwaps, 
                                   int selectionComparisons, int selectionSwaps,
                                   int insertionComparisons, int insertionSwaps) {
        cout << "Algorithm Efficiency Comparison: \n";

        cout << "Bubble Sort: Comparisons: " << bubbleComparisons << ", Swaps: " << bubbleSwaps << endl;
        cout << "Selection Sort: Comparisons: " << selectionComparisons << ", Swaps: " << selectionSwaps << endl;
        cout << "Insertion Sort: Comparisons: " << insertionComparisons << ", Swaps: " << insertionSwaps << endl;

        int minComparisons = min({bubbleComparisons, selectionComparisons, insertionComparisons});
        int minSwaps = min({bubbleSwaps, selectionSwaps, insertionSwaps});

        if (minComparisons == bubbleComparisons && minSwaps == bubbleSwaps) {
            cout << "Bubble Sort is the most efficient algorithm." << endl;
        } else if (minComparisons == selectionComparisons && minSwaps == selectionSwaps) {
            cout << "Selection Sort is the most efficient algorithm." << endl;
        } else {
            cout << "Insertion Sort is the most efficient algorithm." << endl;
        }
    }
};

int main() {
    vector<int> data;
    int n, choice;

    cout << "Enter the number of elements: ";
    cin >> n;
    cout << "Enter the elements: ";
    for (int i = 0; i < n; i++) {
        int temp;
        cin >> temp;
        data.push_back(temp);
    }

    vector<int> arr1 = data;
    vector<int> arr2 = data;
    vector<int> arr3 = data;
    vector<int> arr4 = data;

    int bubbleComparisons = 0, bubbleSwaps = 0;
    int selectionComparisons = 0, selectionSwaps = 0;
    int insertionComparisons = 0, insertionSwaps = 0;

    SortingAlgorithms::bubbleSort(arr1, bubbleComparisons, bubbleSwaps);
    SortingAlgorithms::selectionSort(arr2, selectionComparisons, selectionSwaps);
    SortingAlgorithms::insertionSort(arr3, insertionComparisons, insertionSwaps);
    SortingAlgorithms::simpleSort(arr4, selectionComparisons, selectionSwaps);

    cout << "\nSorted Arrays:" << endl;
    cout << "Bubble Sort: ";
    SortingAlgorithms::display(arr1);
    cout << "Selection Sort: ";
    SortingAlgorithms::display(arr2);
    cout << "Insertion Sort: ";
    SortingAlgorithms::display(arr3);

    SortingAlgorithms::compareEfficiency(bubbleComparisons, bubbleSwaps, 
                                         selectionComparisons, selectionSwaps,
                                         insertionComparisons, insertionSwaps);

    return 0;
}
