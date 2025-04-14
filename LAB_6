#ifndef charQueue
#define charQueue

#include "integer_type.h"

typedef struct {
	char* str;
	unsigned front;
	unsigned rear;
	unsigned size;
	unsigned max_size;
} QUEUE;

QUEUE* create_queue(size_t size) {
	QUEUE* q = (QUEUE*)cAllocate(1, sizeof(QUEUE));
	q->str = (char*)cAllocate(size, sizeof(char));
	q->rear = -1;
	q->front = q->size = 0;
	q->max_size = size;
	return q;
}

void pushend(QUEUE* q, char c) {
	if (q->size >= q->max_size) {
		puts("Очередь заполнена...");
		return;
	}
	q->rear = (q->rear + 1) % q->max_size;
	q->str[q->rear] = c;
	q->size++;
}

char popstart(QUEUE* q) {
	if (!q->size) return 0;
	char c = q->str[q->front];
	q->front = (q->front + 1) % q->max_size;
	q->size--;
	return c;
}

void printfQueue(QUEUE* q) {
	if (!q->size) {
		puts("Очередь пуста...");
		return;
	}

	for (unsigned i = 0, idx = q->front; i < q->size; i++) {
		printf("%c", q->str[idx]);
		idx = (idx + 1) % q->max_size;
	}
	putchar('\n');
}

void freeQueue(QUEUE* q) {
	free(q->str);
	free(q);
}

void cQueue() {
	printf("Введите максимальный размер очереди: ");
	QUEUE* queue = create_queue((size_t)input_uninum());
	printf("\nВведите эталонный символ: ");
	char c = _getche();
	//while (getchar() != '\n');
	puts("\nВводите символы (до эталонного или заполнения очереди): ");
	char ch;
	while (queue->size < queue->max_size) {
		ch = _getche();
		if (ch == c)break;
		pushend(queue, ch);
		//while (getchar() != '\n');
	}
	puts("\nПолученная очередь: ");
	printfQueue(queue);
	freeQueue(queue);
}

#endif
#ifndef charDeque
#define charDeque

#include "integer_type.h"

typedef struct {
    char* str;
    unsigned front;
    unsigned rear;
    unsigned size;
    unsigned max_size;
} DEQUE;

DEQUE* createDeque(size_t max_size) {
    DEQUE* d = (DEQUE*)cAllocate(1, sizeof(DEQUE));
    d->str = (char*)cAllocate(max_size, sizeof(char));
    d->front = -1;
    d->rear = -1;
    d->size = 0;
    d->max_size = max_size;
    return d;
}

void push_front(DEQUE* d, char c) {
    if (d->size == d->max_size) return;
    if (d->front == -1) {
        d->front = d->rear = 0;
    }
    else {
        d->front = (d->front - 1 + d->max_size) % d->max_size;
    }
    d->str[d->front] = c;
    d->size++;
}

void push_back(DEQUE* d, char c) {
    if (d->size == d->max_size) return;
    if (d->front == -1) {
        d->front = d->rear = 0;
    }
    else {
        d->rear = (d->rear + 1) % d->max_size;
    }
    d->str[d->rear] = c;
    d->size++;
}

void printDeque(DEQUE* d) {
    if (!d->size) {
        puts("Дек пуст");
        return;
    }
    unsigned i = d->front;
    unsigned count = d->size;
    while (count--) {
        printf("%c", d->str[i]);
        i = (i + 1) % d->max_size;
    }
    putchar('\n');
}

void freeDeque(DEQUE* d) {
    free(d->str);
    free(d);
}

void cDeque() {
    printf("Введите максимальный размер дека: ");
    DEQUE* deque = createDeque((size_t)input_uninum());
    printf("\nВведите эталонный символ: ");
    char c = _getche();
    puts("\nВводите символы (до эталонного или заполнения дека): ");

    char ch, flag = 0;
    while (deque->size < deque->max_size) {
        ch = _getche();
        if (ch == c) break;
        if (flag) {
            push_back(deque, ch);
            flag = 0;
        }
        else {
            push_front(deque, ch);
            flag = 1;
        }
    }
    puts("\nПолученный дек: ");
    printDeque(deque);
    freeDeque(deque);
}
#endif
#ifndef stringQueue
#define stringQueue

#include "char_type.h"
#include "integer_type.h"

typedef struct {
	char** str;
	int front;
	int rear;
	unsigned* age;
	unsigned size;
} SQUEUE;

SQUEUE* create_squeue() {
	SQUEUE* sq = (SQUEUE*)cAllocate(1, sizeof(SQUEUE));
	sq->rear = -1;
	sq->front = sq->size = 0;
	return sq;
}

void ensqueue(SQUEUE* sq, char* s) {
	char** temp = (char**)realloc(sq->str, (sq->size + 1) * sizeof(char*));
	if (!temp) {
		fprintf(stderr, "Ошибка realloc\n");
		exit(1);
	}
	sq->str = temp;

	sq->rear++;
	sq->str[sq->rear] = s;
	sq->size++;
}

int isEmpty(SQUEUE* sq) {
	return sq->size == 0;
}

char* dequeue(SQUEUE* sq) {
	if (isEmpty(sq)) return NULL;
	char* s = sq->str[sq->front];

	for (int i = 0; i < sq->size - 1; i++) sq->str[i] = sq->str[i + 1];
	sq->rear--;
	sq->size--;
	char** temp = (char**)realloc(sq->str, sq->size * sizeof(char*));
	if (temp || sq->size == 0) {
		sq->str = temp;
	}

	return s;
}

SQUEUE* fillInSqueue(SQUEUE* sq, int count) {
	int i = 0, size = 2;
	sq->str = (char**)cAllocate(size, sizeof(char*));
	while (1) {
		if (count) if (i >= count) break;
		if (i >= size) {
			char** temp = (char**)realloc(sq->str, (size + 1) * sizeof(char*));
			if (!temp) {
				fprintf(stderr, "Ошибка выделения памяти.\n");
				exit(1);
			}
			sq->str = temp;
			size++;
		}

		short flag = 0;
		char* surname = input_str(&flag);
		if (flag == 1 && i != 0) {
			if (count) {
				if (i < count) continue;
				else break;
			}
			else break;
		}
		if (!*surname) {
			puts("Введите корректное значение...");
			continue;
		}
		ensqueue(sq, surname);
		putchar('\n');
		i++;
		if (flag < 0) {
			if (count) {
				if (i < count) continue;
				else break;
			}
			else break;
		}
	}
	putchar('\n');
	return sq;
}

void freeQueue(SQUEUE* sq) {
	for (int i = 0; i < sq->size; i++) {
		free(sq->str[i]);
	}
	free(sq->str);
	free(sq);
}

void printSQueue(SQUEUE* sq, const char *str) {
	printf("+-----+------------------------------+\n");
	printf("| №   | %s                         |\n", str);
	printf("+-----+------------------------------+\n");
	for (int i = 0; i < sq->size; i++) {
		printf("| %-3d | %-28s |\n", i + 1, sq->str[i]);
	}
	printf("+-----+------------------------------+\n\n");
}

void printPerson(SQUEUE* sq) {
	printf("+-----+------------------------------+--------+\n");
	printf("| №   | ФИО                         | Возраст|\n");
	printf("+-----+------------------------------+--------+\n");

	for (int i = 0; i < sq->size; i++) {
		printf("| %-3d | %-28s | %-6u |\n", i + 1, sq->str[i], sq->age ? sq->age[i] : 0);
	}
	printf("+-----+------------------------------+--------+\n\n");
}

void freeSQueue(SQUEUE* sq) {
	for (int i = 0; i < sq->size; i++) {
		free(sq->str[i]);
	}
	free(sq->str);
	free(sq);
}

void sQueue() {
	puts("Введите фамилии: ");
	SQUEUE* Surname = fillInSqueue(create_squeue(), 0);
	puts("\nВведите имена: ");
	SQUEUE* Name = fillInSqueue(create_squeue(), Surname->size);
	puts("\nВведите отчества: ");
	SQUEUE* Fname = fillInSqueue(create_squeue(), Surname->size);
	system("cls");
	printSQueue(Surname, "Фамилии");
	printSQueue(Name, "Имена");
	printSQueue(Fname, "Отчества");

	SQUEUE* fullNames = create_squeue();
	unsigned count = 5, i = 0;
	fullNames->age = (unsigned*)cAllocate(count, sizeof(unsigned));

	while (!isEmpty(Surname) && !isEmpty(Name) && !isEmpty(Fname)) {
		char* surname = dequeue(Surname);
		char* name = dequeue(Name);
		char* fname = dequeue(Fname);

		if (i >= count) {
			count *= 2;
			unsigned* temp = (unsigned*)realloc(fullNames->age, count * sizeof(unsigned));
			if (!temp) {
				fprintf(stderr, "Ошибка выделения памяти.\n");
				exit(1);
			}
			fullNames->age = temp;
		}

		size_t size = my_strlen(surname) + my_strlen(name) + my_strlen(fname) + 3;
		char* fullName = (char*)cAllocate(size, sizeof(char));
		snprintf(fullName, size, "%s %s %s", surname, name, fname);

		printf("\nВведите возраст %s: ", fullName);
		fullNames->age[i++] = input_uninum();
		ensqueue(fullNames, fullName);

		free(surname);
		free(name);
		free(fname);
	}

	printf("\nСписок ФИО:\n");
	printPerson(fullNames);

	freeQueue(Surname);
	freeQueue(Name);
	freeQueue(Fname);
	freeQueue(fullNames);
}
#endif
/*1. Создать очередь для символов. Максимальный размер очереди вводится с экрана. Создать
функции для ввода и вывода элементов очереди. Ввести эталонный символ. Вводить символы с экрана
в очередь до встречи эталонного. Вывести все элементы очереди.*/
/*2. Создать дек для символов. Максимальный размер дека вводится с экрана. Создать функции
для ввода и вывода элементов дека. Ввести эталонный символ. Вводить символы в дек поочередно
справа и слева до встречи эталонного. Вывести все элементы дека.*/
/*3.Организовать три очереди с одинаковым количеством элементов, содержащие соответствено
имена, отчества и фамилии людей. Составьте очередь из элементов, содержащих наиболее полную
информацию о людях, воспользовавшись уже созданными очередями и запросив какую-то
дополнительную информацию. Решение в программе оформляйте через подпрограммы.*/
#include "stringQueue.h"
#include "charDeque.h"
#include "charQueue.h"

int main() {
	setlocale(LC_ALL, "Rus");
	//sQueue();
	//cDeque();
	//cQueue();

	return 0;
}
