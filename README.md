# С++. Часть 1. Разбор задач из собеседований

Этот репозиторий содержит описание задач из реальных собеседований по С/С++. Здесь собраны условия задач, код решения и основные навыки, которого проверяются у кандидата.

# Введение

Программирование на С++ является крайне актуальной сферой в IT, так как сегодня многие сервисы, ориентированные на высокую производительность, вряд ли смогут сделать дизайн решения, миновав С++. [По сообщению TAdviser](https://www.tadviser.ru/index.php/%D0%A1%D1%82%D0%B0%D1%82%D1%8C%D1%8F:%D0%A0%D0%B5%D0%B9%D1%82%D0%B8%D0%BD%D0%B3_%D0%B2%D0%BE%D1%81%D1%82%D1%80%D0%B5%D0%B1%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8_%D1%8F%D0%B7%D1%8B%D0%BA%D0%BE%D0%B2_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F) этот язык занимает 4 место по популярности в 2021 году.

Существенная группа студентов отмечают сложность программирования на нем из-за высокого входного порога. Однако я считаю, что это не так, и мы можем уменьшить сложность изучения языка путем **актуализации учебного плана** курсов, связанных с С++. И в этом документе мы затронем то, какие знания требуют от кандидатов на должность Junior/Middle программиста С++.

# Требуемые компетенции

Стоит заметить, что у компаний разительно отличается подход к найму. Некоторые компании в ходе технического интервью не имеют тестовых задач, другие - самого технического интервью. Однако, на основе моего опыта можно выделить несколько наиболее важных областей знаний, в которых кандидат должен показывать довольно высокий уровень знаний:

* Общий цикл разработки ПО, современные подходы к разработке ПО
* Тестирование и виды тестов
* Базовая история языка С++ и его версий
* Процесс компиляции и сборки исполняемого файла
* Фундаментальные отличия от С
* Работа с памятью, указатели
* Понимание big-O нотации
* Паттерны проектирования (Design patterns), виды паттернов, 1-2 примера каждого вида
* Структуры данных: деревья, стек, очередь, дерево
* Алгоритмы STL
* Способы работы с многопоточностью

# Задача 1. Базовый синтаксис

## Условие

Посчитайте количество единиц в произвольном числе.

## Решение

Существует несколько способов решения задачи, которые приблизительно одинаково эффективно работают. Рассмотрим два самых популярных: преобразование в строку и работа с числами

<details>
    <summary>Преобразование в строку</summary>

Алгоритм использует встроенную функцию преобразования в строку. Итоговый алгоритм будет таким:
```c++
int a;
std::cin >> a;
auto str_a = std::to_string(a);

int res=0;
for(auto i: a){
    if(i == '1') 
        res++;
}
std::cout << res << std::endl;
```
</details>

<details>
    <summary> Работа с числами </summary>

Этот метод использует побитовые операции, которые являются частью С++.

``` c++
unsigned int count = 0;
for (; n; n <<= 1)
    count += n & 1;
```
</details>    

## Требуемые знания

- Синтаксис С++
- Двоичное представление числа

# Задача 2. Найти ошибку(-и) в коде

## Условие
Дан отрывок программы, которая должна вывести числа от 100 до 0. 

``` c
unsigned int i;
for (i = 100; i >= 0; --i)
    printf("%d", i);
```

Необходимо ответить на 2 вопроса

1. Что выведет программа?
2. Корректен ли вывод? Если нет, то какие ошибки были допущены?

## Решение

<details>
  <summary>Что выведет программа?</summary>
Программа не закончит свое выполнение, так как переменная будет всегда соответсовать условиям цикла.
</details>

<details>
  <summary>Корректен ли вывод?</summary>
Нет, так как будет бесконечный вывод 0.
</details>

<details>
  <summary>Корректен ли вывод?</summary>
Нет, так как будет бесконечный вывод 0.
</details>

<details>
  <summary>Допущенные ошибки</summary>
1. Неправильно выбранный тип данных.
2. Печать переменной типа unsigned int должна быть с %u вместо %d
</details>

## Требуемые знания

1. Понимание синтаксиса С
2. Принцип работы цикла for
3. Отличие unisnged типов переменных от обычных
4. Инвертирование знаков в бинарном коде

# Задача 3. STL, сложность алгоритмов

## Условие
Дан ненаправленный граф, который описывает схему метро. Пассажиру, который находится на определенной станции, необходимо узнать, до каких станций возможно доехать, имея проездной на N станций. Желательно сделать алгоритм оптимальным по времени

Необходимо описать структуру данных графа и алгоритм решения задачи

## Решение

<details>
  <summary>Базовая структура данных</summary>

Структура данных представляет собой два списка: список всех вершин и список пар соединений. Трансформируясь в код С++, структура данных была бы описана следующим образом:

``` c++
#include <string>
#include <vector>
#include <pair>

class Node{
    std::string Station;
}

class Graph {
    std::vector<Node> vertices;
    std::vector<std::pair<Node, Node>> edges;
```
</details>

<details>
  <summary>Улучшенная структура данных</summary>

Эту структуру данных можно оптимизировать по времени, так как дополнительные ограничения по памяти не были озвучены. Список пар можно заменить на словарь, так как он имеет ускоренный доступ по ключу: O(logN) вместо O(N). Поскольку соединений у вершины может быть более одного, должен использоваться тип ```std::multipmap<Node, Node>```. Таким образом, улучшенная структура данных выглядит следующим образом:

``` c++
#include <string>
#include <vector>
#include <multimap>

class Node{
    std::string Station;
}

class Graph {
    std::vector<Node> vertices;
    std::multimap<Node, Node> edges;
```
</details>

<details>
  <summary>Алгоритм поиска и его сложнсть</summary>

Решением задачи является функция, которая принимает на вход граф, текущую станцию и количество станций в проездном. Наиболее оптимальным контейнером будет ```std::set<Node>```, так как он автоматически верифицирует отсутствие дубликатов. Таким образом, необходимо релизовать следующую функцию:
``` c++
std::set<Node> findAll(const Graph &graph, const Node &node, int length);
```
Алгоритм заключается в модиффикации алгоритма BFS относительно текущей станции с учетом количества оставшихся поездок. Таким образом, код выглядит следующим образом:
``` c++
std::set<Node> findAll(const Graph &graph, const Node &node, int length) {
    std::set<Node> result;

    std::map<Node, bool> visited
    for(auto i: graph.vertices){
        visited.insert(i, false);
    }
 
    // Create a queue for BFS
    list<std::pair<Node, int>> queue;
 
    // Mark the current node as visited and enqueue it
    visited[node] = true;
    queue.push_back(std::make_pair(node, length));
 
    while(!queue.empty())
    {
        auto current = queue.front();
        if(current.second > 0) current.second--;
        else break;
        queue.pop_front();
 
        // Get all adjacent vertices of the dequeued
        // vertex s. If a adjacent has not been visited,
        // then mark it visited and enqueue it
        auto adj = graph.findEdges(current.first);
        for (auto i = adj.begin(); i != adj.end(); ++i)
        {
            if (!visited[*i])
            {
                visited[*i] = true;
                queue.push_back(std::make_pair(*i, length));
            }
        }
    }

```

Предположим, что в графе N вершин и M соединений. 
Следовательно, O(поиск соединения) равняется

- O(M) в случае базового подхода
- O(log M) в случае улучшенного подхода

Следовательно, сложность алгоритма по времени составляет O((M + N)*O(поиск соединения)) ~ O(N).
</details>

## Требуемые знания

- Знание типичных задач по работе с графами и алгоритмов их решения
- Знание контейнеров STL и их основных функций
- Сложностей базовых операций при работе с STL
  
# Задача 4. Полиморфизм

## Условие

Что выведет эта программа?

``` c++
class Foo {
public:
  int f() {
      return 1;
  }
};

class Bar : public Foo {
public:
  int f(){
      return 2;
  }
}

Foo *p = new Bar();
int res = p->f();
std::cout << res << std::endl;
```

## Решение

Функция выведет 1, так как функция ```inf f()``` не является виртуальной. П

## Требуемые знания
	
- Понимание принципов ООП
- Реализация полиморфизма
- Наследование
	
# Задача 5. Singleton

## Условие

Расскажите про паттерн Singleton. Расскажите основные особенности его реализации.

## Решение

<details>
<summary>Исходный код</summary>

```c++
#include <iostream>

class Singleton {
   static Singleton *instance;
   int data;
 
   // Private constructor so that no objects can be created.
   Singleton() {
      data = 0;
   }

   public:
   static Singleton *getInstance() {
      if (!instance)
      instance = new Singleton;
      return instance;
   }

   int getData() {
      return this -> data;
   }

   void setData(int data) {
      this -> data = data;
   }
};

//Initialize pointer to zero so that it can be initialized in first call to getInstance
Singleton *Singleton::instance = 0;

int main(){
   Singleton *s = s->getInstance();
   std::cout << s->getData() << std::endl;
   s->setData(100);
   std::cout << s->getData() << std::endl;
   return 0;
}
```
</details>

## Требуемые знания

- Паттерны и их виды
- Паттерн Singleton

# Бонус. Что бы я спросил на собеседовании?

## Условие

Реализуйте итератор для однозсвязанного списка. 

## Решение

Итератор - класс, который хранит ссылку на объект списка и реализует следующие операции

- ```operator =``` - присваивание
- ```operator ++``` - увеличение на 1 (пост-и пре-инкремент)
- ```operator ==``` - логическое сравнивание
- ```operator *``` - получение значения объекта, на который ссылается итератор

<details>
  <summary>Код решения</summary>

``` c++
class Iterator {
	public:
	Iterator() noexcept :
		m_pCurrentNode (m_spRoot) { }

	Iterator(const Node* pNode) noexcept :
		m_pCurrentNode (pNode) { }

		Iterator& operator=(Node* pNode) {
			this->m_pCurrentNode = pNode;
			return *this;
		}

		// Prefix ++ overload
		Iterator& operator++() {
			if (m_pCurrentNode)
				m_pCurrentNode = m_pCurrentNode->pNext;
			return *this;
		}

		// Postfix ++ overload
		Iterator operator++(int) {
			Iterator iterator = *this;
			++*this;
			return iterator;
		}

		bool operator!=(const Iterator& iterator) {
			return m_pCurrentNode != iterator.m_pCurrentNode;
		}

		int operator*() {
			return m_pCurrentNode->data;
		}

	private:
		const Node* m_pCurrentNode;
};
```
</details>

## Требуемые знания

- Знание ООП
- Навык перегрузка операторов
- Навык декомпозиции задачи на подзадачи
- Знание определения итератора и его области применения

# Итоги

В этом документе мы разобрали встречаемые на моей практике задачи и темы в рамках собеседований в С++. Если Вы найдете ошибку в коде или будет какое-либо замечание пишите на [почту](ilya210819993@gmail.com).

# Полезые ссылки

- [400 вопросов на собеседованиях по С++](https://itvdn.com/ru/blog/article/400-about-cplspls)
- [123 задачи с IT собеседований](https://tproger.ru/articles/problems/)
