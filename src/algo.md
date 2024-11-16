# Алгосы

## Задача 1 (MinStack)
### Условие
Реализовать класс MinStack, который поддерживает push, pop, top и получение минимального элемента за
константное время. Класс должен обладать следующим интерфейсом:
```cpp
struct MinStack {
    MinStack(); // инициализирует объект
    void push(int val); // помещает элемент в стек
    void pop(); // удаляет элемент из вершины стека
    int top(); // возвращает верхний элемент стека.
    int getMin(); // возвращает минимальный элемент в стеке
};
```
### Решение
```cpp
struct MinStack {
private:
    std::stack<std::pair<int, int>> stack_{};
    void validate_stack() {
        if (stack_.empty()) {
            throw std::runtime_error("stack is empty");
        }
    }

public:
    MinStack() = default;
    void push(int val) {
        if (stack_.empty()) {
            stack_.push({val, val});
        } else {
            stack_.push({val, std::min(val, stack_.top().second)});
        }
    }

    void pop() {
        validate_stack();
        stack_.pop();
    }

    int top() {
        validate_stack();
        return stack_.top().first;
    }

    int getMin() {
        validate_stack();
        return stack_.top().second;
    }
};
// O(1) - time
// O(2n) = O(n) - memory
```
## Задача 2 (Move even, move zeros)
### Условие
Реализовать функцию, которая удаляет четные числа из std::vector (inplace). Порядок нечетных элементов остается неизменным

Пример: [2, 3, 1, 6, 7, 8] -> [3, 1, 7]

### Решение
```cpp
// Используя библиотеку STL
void remove_even(std::vector<int>& input) {
    input.erase(std::remove_if(input.begin(), input.end(), [](int x){
        return x % 2 == 0;
    }), input.end());
}

// Самописный алгоритм
void remove_even(std::vector<int>& input) {
    size_t p = 0;
    for (size_t i = 0; i < input.size(); i++) {
        if (input[i] % 2 != 0) {
            input[p++] = input[i];
        }
    }
    input.resize(p);
}
// O(n) - time
// O(1) - memory
```