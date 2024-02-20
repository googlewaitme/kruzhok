---
marp: true
theme: gaia
math: mathjax
paginate: true
footer: Saint-Petersburg | SUAI 2024 | Кружок АиСД | Лекция 2
header:  Bulat Zaripov, Semkov Stepan
---
<style>
    h1 { font-size: 60px; margin: .67em 0 }
    section {font-size: 50px}
    header, footer {
        font-size: 20px
    }
</style>
<!--_paginate: false-->
<!--_class: invert -->

# <!--fit--> АиСД лекция 2

# Устройство памяти компьютера
---
# Вопросы, которые нужно обсудить

- Все ли расписались за технику безопасности?
- Как домашка?
- Что было сложно решить?

---

# Основные компоненты памяти компьютера
- Регистры
- КЭШ
- Оперативная память
- Внешняя память(постоянная память)
---

# Зачем нужны разные виды памяти
- Скорость доступа
- Стоимость хранения
- Время хранения
---

# Как хранятся целые числа?

$121_{10}=1111001_2$

|0|1|1|1|1|0|0|1|
|---|---|---|---|---|---|---|---|

---

# Как работают системы счисления

Переведите в нужную систему счисления:
$$121_{10}=X_2$$
$$78_{10}=X_5$$
$$100_{10}=X_3$$
$$555_{10}=X_{16}$$

---
# Как работают системы счисления

Ответы:
$$121_{10}=111001_2$$
$$78_{10}=303_5$$
$$100_{10}=10201_3$$
$$555_{10}=22B_{16}$$
---

# Как хранятся вещественные числа?

 float или с плавающей точкой
**Экспоненциальная запись**
$$(-1)^S \times 1.M \times 10^E$$

S(ign) - знак, M(antis) - мантисса, E(xponent) - экспонента

---
# Как хранятся вещественные числа?

$101.01=1.0101*10^2$
$0.0101=1.01*10^{-3}$

---
# Как сравнить два вещественных числа

``` py
>>> 0.1 + 0.2 == 0.3
False
```
Спрашивается почему?

---
# Как сравнить два вещественных числа
Вот так надо сравнивать
``` py
>>> accuracy = 10.0 ** (-9)
>>> abs(0.1 + 0.2 - 0.3) <= accuracy
True
```
--- 
# Как хранятся ссылки
``` c++
int x = 1;
int &y = x;
cout << &x << " " << x << endl; \\ 0x7ffc05c4e3ac 1
cout << &y << " " << y << endl; \\ 0x7ffc05c4e3ac 1
y = 5;
cout << &x << " " << x << endl; \\ 0x7ffc05c4e3ac 5
cout << &y << " " << y << endl; \\ 0x7ffc05c4e3ac 5
```
---
# Как хранятся массивы

<style scoped>
    pre {
        font-size: 39px;
    }
</style>

``` c++
int main() {
    int n = 5;
    int* array = new int[n];   
    for (int i=0; i<n; i++) {
        array[i] = i;
    }
    for (int i=0; i<n; i++) {
        cout << array[i] << " ";  // 0 1 2 3 4
    }
    delete [] array;
    return 0;
}
```
---
# Как хранятся массивы массивов
<style scoped>
    pre {
        font-size: 39px;
    }
</style>
``` c++
int n = 5;
int** array = new int*[n];   
for (int i=0; i<n; i++) {
    array[i] = new int[n];
}
...
array[i][j] = 5;
...
for (int i=0; i<n; i++) {
    delete[] array[i];
}
delete [] array;
```
---
# Как хранятся списки

Односвязный список

$$
\fbox{val}\fbox{url} \rightarrow 
\fbox{val}\fbox{url} \rightarrow 
\fbox{val}\fbox{null}
$$

Двусвязный список

$$
\fbox{null}\fbox{val}\fbox{url} \leftrightarrow 
\fbox{url}\fbox{val}\fbox{url} \leftrightarrow 
\fbox{url}\fbox{val}\fbox{null}
$$

---
# Пример односвязного списка
``` py
class ListNode:
    def __init__(self, value, next=None):
        self.value = value
        self.next = next
c = ListNode("C")
b = ListNode("B", c)
a = ListNode("A", b)
```
---
# Пример односвязного списка
``` py
current = a
print(current.value, current.next)
while current.next:
    current = current.next
    print(current.value, current.next)
# A <__main__.ListNode object at 0x7fbeb695ff10>
# B <__main__.ListNode object at 0x7fbeb695ffd0>
# C None

```
---
# Побитовые операции
<style scoped>
    section {font-size: 40px}
</style>
| a    | b    | operator | result |
|------|------|----------|--------|
| 1100 | 1010 | & and    | 1000   |
| 1100 | 1010 | \| or    | 1110   |
| 1100 | 1010 | ^ xor    | 0110   |
| 1100 |      | ! not    | 0011   |
---
# Побитовые операции
Логические сдвиги
``` py
>>> 1 << 2   # 0001 << 2 == 0100
4
>>> 4 >> 1   # 0100 >> 1 == 0010
2
>>> 4 & (1 << 2) == 1  # 0100 & (0001 << 2)
True
```
---
# Побитовые операции
$11 \land 7 = x_1$
$11 | 7 = x_2$
$11\ xor\ 7 = x_3$
$15\oplus16 = x_4$

---
# Побитовые операции

$11 \land 7 = 3$
$11 | 7 = 15$
$11\ xor\ 7 = 10$
$15\oplus16 = 0$

---
# <!--fit--> Спасибо за внимание

bulat.zar-1203@yandex.ru
https://vk.com/suai_it