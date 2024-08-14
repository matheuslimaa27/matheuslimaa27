import unittest
import time
import random

# Implementação do QuickSort
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)

# Implementação do MergeSort
def mergesort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = mergesort(arr[:mid])
    right = mergesort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    left_index, right_index = 0, 0
    while left_index < len(left) and right_index < len(right):
        if left[left_index] < right[right_index]:
            result.append(left[left_index])
            left_index += 1
        else:
            result.append(right[right_index])
            right_index += 1
    result.extend(left[left_index:])
    result.extend(right[right_index:])
    return result

# Classe de Teste para Algoritmos de Ordenação
class TestSortingAlgorithms(unittest.TestCase):

    def setUp(self):
        # Cria dados de teste com duas listas de tamanhos diferentes
        self.test_data_small = [random.randint(0, 100) for _ in range(100)]
        self.test_data_large = [random.randint(0, 1000) for _ in range(1000)]

    def test_quicksort_performance(self):
        start_time = time.time()
        quicksort(self.test_data_large)
        end_time = time.time()
        execution_time = end_time - start_time
        print(f"QuickSort execution time: {execution_time:.6f} seconds")
        # Ajuste o limite conforme necessário para sua máquina e dados
        self.assertLess(execution_time, 1.0)  # Assume 1 segundo como limite para este exemplo

    def test_mergesort_performance(self):
        start_time = time.time()
        mergesort(self.test_data_large)
        end_time = time.time()
        execution_time = end_time - start_time
        print(f"MergeSort execution time: {execution_time:.6f} seconds")
        # Ajuste o limite conforme necessário para sua máquina e dados
        self.assertLess(execution_time, 1.0)  # Assume 1 segundo como limite para este exemplo

if __name__ == "__main__":
    unittest.main()

