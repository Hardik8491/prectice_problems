# Question 9

## Problem Statement

Write a Python program to build a system that identifies modified runners based on their running speed.

Create two classes:

**1. Runner Class**
*   **Attributes:**
    *   `name` (string): The name of the runner.
    *   `club_name` (string): The club the runner belongs to.
    *   `distance` (int): The total distance covered by the runner.
    *   `time` (int): The time taken by the runner to cover the distance.
*   Create an `__init__` method to initialize these attributes.

**2. Race Class**
*   **Attributes:**
    *   `runner_list` (list): A list of `Runner` objects.
    *   `user_place` (int): A target speed value to compare against.
*   Create an `__init__` method to initialize these attributes.
*   **Method `Qualified()`**: 
    *   This method should calculate the speed of each runner (calculated as `distance // time`).
    *   Find all runners whose speed is strictly greater than `user_place`.
    *   Print the `name` of each qualified runner on a new line.
    *   *(Note: Based on intended logic, if no runners meet the criteria, the system should print "not found!")*

## Input Format
1. An integer `n` representing the number of runners.
2. The next `n * 4` lines will contain the `name`, `club_name`, `distance`, and `time` for each of the `n` runners.
3. The last line will be an integer `user_place` representing the target speed threshold.

## Expected Output
Print the names of the runners who have a speed greater than `user_place`.

---

### Solution Code:
```python
class Runner:
    def __init__(self, name, club_name, distance, time):
        self.name = name
        self.club_name = club_name
        self.distance = distance
        self.time = time


class Race:
    def __init__(self, runner_list, user_place):
        self.runner_list = runner_list
        self.user_place = user_place

    def Qulified(self):
        records = []
        for runner in self.runner_list: # Fixed to use self.runner_list
            if runner.distance // runner.time > self.user_place:
                records.append(runner)

        if len(records) > 0:
            for runner in records:
                print(runner.name)
        else:
            print("not found!")


n = int(input())
runner_lst = []
for _ in range(n):
    name = input()
    club_name = input()
    distance = int(input())
    time = int(input())
    runner_lst.append(Runner(name, club_name, distance, time))
user_place = int(input())
race = Race(runner_lst, user_place)
race.Qulified()
```

