# Симулятор жизни студента

Студент проживает год: учится, работает, отдыхает и спит. Работа приносит деньги, отдых их тратит, а при проблемах с деньгами или учёбой студент сам решает, что делать.

Запуск: `python main.py`

## Код (main.py)

```python
import random


class Student:
    def __init__(self, name):
        self.name = name
        self.gladness = 50      # настроение
        self.progress = 0       # успеваемость
        self.money = 100        # деньги
        self.alive = True

    def to_study(self):
        print("Пора учиться")
        self.progress += 0.12
        self.gladness -= 3

    def to_sleep(self):
        print("Я посплю")
        self.gladness += 3

    def to_chill(self):
        print("Время отдохнуть")
        self.gladness += 5
        self.progress -= 0.1
        self.money -= 20

    def to_work(self):
        print("Иду на работу")
        self.money += 50
        self.gladness -= 4
        self.progress -= 0.05

    def is_alive(self):
        if self.progress < -0.5:
            print("Отчислен...")
            self.alive = False
        elif self.gladness <= 0:
            print("Депрессия...")
            self.alive = False
        elif self.progress > 5:
            print("Сдал экстерном!")
            self.alive = False
        elif self.money < -100:
            print("Влез в долги и бросил учёбу...")
            self.alive = False

    def end_of_day(self):
        print(f"Настроение = {self.gladness}")
        print(f"Успеваемость = {round(self.progress, 2)}")
        print(f"Деньги = {self.money}")

    def live(self, day):
        print(f"\nДень {day} из жизни {self.name}")
        # Продуманное поведение: сначала решаем срочные проблемы
        if self.money < 0:
            self.to_work()
        elif self.progress < -0.2:
            self.to_study()
        elif self.gladness < 15:
            if self.money >= 20:
                self.to_chill()
            else:
                self.to_sleep()
        else:
            choice = random.randint(1, 4)
            if choice == 1:
                self.to_study()
            elif choice == 2:
                self.to_sleep()
            elif choice == 3:
                self.to_chill()
            else:
                self.to_work()
        self.end_of_day()
        self.is_alive()


nick = Student("Nick")
for day in range(1, 366):
    if not nick.alive:
        break
    nick.live(day)
else:
    print("\nСтудент прожил целый год!")

input("\nНажми Enter, чтобы выйти...")```
