## задание 1
Дана прямоугольная доска $N*M$ (**N** строк и **M** столбцов).  
В левом верхнем углу находится шахматный конь Олег, которого необходимо переместить в правый нижний угол доски. 
В данной задаче конь может перемещаться на две клетки вниз и одну клетку вправо или на одну клетку вниз и две клетки вправо.
### код-решение
```
with open('input.txt', 'r') as file:
    N, M = map(int, file.readline().split())
    if not (1 <= N <= 50 and 1 <= M <= 50):
        print("Нужны числа от 1 до 50!! измените числа в входном файле и перезапустите код")

    dp = [[0] * M for _ in range(N)]
    dp[0][0] = 1

    for i in range(N):
        for j in range(M):
            if i + 1 < N and j + 2 < M:
                dp[i+1][j+2] += dp[i][j]
            if i + 2 < N and j + 1 < M:
                dp[i+2][j+1] += dp[i][j]

    result = dp[N-1][M-1]
    print(result)
```
___________________________________________________
## задание 2
Олег очень любит занятия по программированию в университете. 
А еще больше он любит узнавать новые алгоритмы и структуры данных.
Для того, чтобы ему не было скучно на очередном занятии, преподаватель предложил придумать способ поиска медианы для последовательности 
**X** из **n** элементов.
Олег быстро нашел в сети нужный алгоритм и отчитался перед учителем. Тогда тот предложил усложнённую версию задачи: для каждого 
**i** от **1** до **n** нужно найти медиану среди первых **i** элементов последовательности 
**X**. В качестве результата преподаватель попросил сказать сумму найденных значений.

Медианой последовательности в случае нечётной длины **L** называется элемент, который будет равноудалён от концов последовательности, если ее отсортировать по возрастанию или убыванию 
(нетрудно сообразить, что этот элемент имеет номер $(L + 1) / 2$ в отсортированной последовательности, если номера считать с единицы). 
В случае чётной длины **L** медианой будем считать элемент, который окажется на месте $L/2$, если последовательность отсортировать по возрастанию.
### код-решение
```
with open('input.txt', 'r') as file:
    n = int(file.readline())
    sequence = list(map(int, file.readline().split()))
    medians = []

    for i in range(n):
        sequence[:i+1] = sorted(sequence[:i+1])
        if (i + 1) % 2 == 1:
            median = sequence[(i + 1) // 2]
        else:
            median = sequence[i // 2]
        medians.append(median)

    total_sum = sum(medians)
    print(total_sum)
```
___________________________________________________
## задание 3
Вовочка ломает систему безопасности Пентагона. 
Для этого ему понадобилось узнать, какие символы в секретных зашифрованных посланиях употребляются чаще других. 
Для удобства изучения Вовочка хочет получить графическое представление встречаемости символов. 
Поэтому он хочет построить гистограмму количества символов в сообщении. 
Гистограмма — это график, в котором каждому символу, встречающемуся в сообщении хотя бы один раз, соответствует столбик, 
высота которого пропорциональна количеству этих символов в сообщении.
### код-решение
```
with open('input.txt', 'r') as file:
    text = file.read()
    char_count = {}
    for char in text:
        if char not in char_count and char != ' ' and char != '\n':
            char_count[char] = 1
        elif char != ' ' and char != '\n':
            char_count[char] += 1

    sorted_chars = sorted(char_count.keys())
    max_count = max(char_count.values())

    for i in range(max_count, 0, -1):
        line = ''
        for char in sorted_chars:
            if char_count.get(char, 0) >= i:
                line += '#'
            else:
                line += ' '
        print(line)

    symbols_line = ''.join(sorted_chars)
    print(symbols_line)
```