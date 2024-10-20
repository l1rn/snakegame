#include <iostream>
#include <conio.h>   // Для _kbhit() и _getch()
#include <windows.h> // Для Sleep()
using namespace std;

// Класс для управления игрой
class SnakeGame {
private:
    bool gameOver;           // Флаг завершения игры
    const int width = 20;    // Ширина игрового поля
    const int height = 20;   // Высота игрового поля
    int x, y, fruitX, fruitY, score; // Координаты головы змеи, фрукта и счет
    int tailX[100], tailY[100];      // Координаты хвоста змеи
    int nTail;                       // Длина хвоста
    enum eDirection { STOP = 0, LEFT, RIGHT, UP, DOWN }; // Направления движения
    eDirection dir;                  // Текущее направление

public:
    // Конструктор для начальной настройки игры
    SnakeGame() {
        Setup();
    }

    // Начальная настройка игры
    void Setup() {
        gameOver = false;
        dir = STOP;
        x = width / 2; // Начальная позиция змейки
        y = height / 2;
        fruitX = rand() % width; // Рандомное положение фрукта
        fruitY = rand() % height;
        score = 0;
        nTail = 0; // Начальная длина хвоста
    }

    // Функция для отрисовки игрового поля
    void Draw() {
        system("cls"); // Очистка экрана

        // Верхняя граница
        for (int i = 0; i < width + 2; i++) cout << "#";
        cout << endl;

        // Отрисовка поля
        for (int i = 0; i < height; i++) {
            for (int j = 0; j < width; j++) {
                if (j == 0) // Левая граница
                    cout << "#";

                if (i == y && j == x) // Голова змейки
                    cout << "O";
                else if (i == fruitY && j == fruitX) // Фрукт
                    cout << "F";
                else {
                    bool printTail = false;
                    for (int k = 0; k < nTail; k++) { // Отрисовка хвоста
                        if (tailX[k] == j && tailY[k] == i) {
                            cout << "o";
                            printTail = true;
                        }
                    }
                    if (!printTail) cout << " "; // Пустое пространство
                }

                if (j == width - 1) // Правая граница
                    cout << "#";
            }
            cout << endl;
        }

        // Нижняя граница
        for (int i = 0; i < width + 2; i++) cout << "#";
        cout << endl;

        cout << "Score: " << score << endl;
    }

    // Управление через клавиатуру
    void Input() {
        if (_kbhit()) { // Если нажата клавиша
            switch (_getch()) {
            case 'a':
                dir = LEFT;
                break;
            case 'd':
                dir = RIGHT;
                break;
            case 'w':
                dir = UP;
                break;
            case 's':
                dir = DOWN;
                break;
            case 'x':
                gameOver = true;
                break;
            }
        }
    }

    // Основная логика игры
    void Logic() {
        int prevX = tailX[0];
        int prevY = tailY[0];
        int prev2X, prev2Y;
        tailX[0] = x;
        tailY[0] = y;

        for (int i = 1; i < nTail; i++) {
            prev2X = tailX[i];
            prev2Y = tailY[i];
            tailX[i] = prevX;
            tailY[i] = prevY;
            prevX = prev2X;
            prevY = prev2Y;
        }

        switch (dir) { // Движение змейки
        case LEFT:
            x--;
            break;
        case RIGHT:
            x++;
            break;
        case UP:
            y--;
            break;
        case DOWN:
            y++;
            break;
        default:
            break;
        }

        // Условие выхода за границы
        if (x >= width) x = 0; else if (x < 0) x = width - 1;
        if (y >= height) y = 0; else if (y < 0) y = height - 1;

        // Проверка на столкновение с хвостом
        for (int i = 0; i < nTail; i++) {
            if (tailX[i] == x && tailY[i] == y)
                gameOver = true;
        }

        // Если змейка съедает фрукт
        if (x == fruitX && y == fruitY) {
            score += 10;
            fruitX = rand() % width;
            fruitY = rand() % height;
            nTail++;
        }
    }

    // Проверка завершения игры
    bool isGameOver() {
        return gameOver;
    }
};

// Основная функция игры
int main() {
    SnakeGame snake; // Создание объекта игры

    while (!snake.isGameOver()) {
        snake.Draw();   // Отрисовка поля
        snake.Input();  // Обработка ввода
        snake.Logic();  // Логика игры
        Sleep(100);     // Задержка для контроля скорости
    }

    return 0;
}
