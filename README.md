# ⏱️ Round Robin Scheduling Algorithm  

A Python implementation of the **Round Robin (RR) CPU Scheduling Algorithm**, a widely used **pre-emptive scheduling technique** in operating systems.  

Round Robin works by **assigning a fixed time quantum** (time slice) to each process in the ready queue. If a process doesn't finish in its time slice, it goes to the back of the queue, allowing the CPU to **fairly allocate time to all processes**. This method balances efficiency and responsiveness, making it suitable for time-sharing systems.  

---

## 📌 Features  
- Object-oriented design using `Process` and `Round_Robin` classes  
- Tracks **arrival time, burst time, waiting time, and turnaround time**  
- Supports **time-slice execution**  
- Includes example process queue for simulation  
- Gantt chart visualization for process execution  

---

## 🧩 Code Example  

```py
class Process:
    def __init__(self, pid, arrival_time, burst_time, remaining_time, waiting_time, turnaround_time):
        self.__pid = pid
        self.__arrival_time = arrival_time
        self.__burst_time = burst_time
        self.__remaining_time = remaining_time
        self.__waiting_time = waiting_time
        self.__turnaround_time = turnaround_time

    def Execute_Time_Slice(self, timeslice):
        self.__remaining_time -= timeslice
        return self.__waiting_time

    def Set_Completion_Time(self, current_time):
        self.__turnaround_time = current_time - self.__arrival_time
        self.__waiting_time = self.__turnaround_time - self.__burst_time
        return self.__waiting_time


class Round_Robin:
    def __init__(self, processes, time_slice):
        self.__processes = processes
        self.__time_slice = time_slice
        self.__current_time = 0
```

Example process queue:  

```py
queue = [
    Process(1, 0, 7, 7, 0, 0),
    Process(2, 2, 4, 4, 0, 0),
    Process(3, 4, 9, 9, 0, 0),
    Process(4, 6, 5, 5, 0, 0),
    Process(5, 8, 2, 2, 0, 0),
]
```

---

## 🚀 How to Run  

Clone the repository:  

```bash
git clone https://github.com/cosalt/scheduling-algorithms.git
cd scheduling-algorithms
```

Run the Python script:  

```bash
python round_robin.py
```

---

## 📊 Gantt Chart Visualization  

Visualize the execution of processes with a Gantt chart:

```py
import matplotlib.pyplot as plt

# Example process execution order and times (process_id, start_time, duration)
execution_log = [
    (1, 0, 3),
    (2, 3, 3),
    (3, 6, 3),
    (1, 9, 3),
    (4, 12, 3),
    (5, 15, 2)
]

fig, ax = plt.subplots(figsize=(10, 3))

colors = ['skyblue', 'orange', 'green', 'red', 'purple']
for i, (pid, start, duration) in enumerate(execution_log):
    ax.barh(1, duration, left=start, height=0.3, color=colors[pid-1 % len(colors)], edgecolor='black')
    ax.text(start + duration/2, 1, f"P{pid}", ha='center', va='center', color='black', fontsize=10)

ax.set_xlim(0, max(start + duration for _, start, duration in execution_log) + 1)
ax.set_ylim(0.5, 1.5)
ax.set_xlabel("Time")
ax.set_yticks([])
ax.set_title("Round Robin CPU Scheduling Gantt Chart")
plt.show()
```

This chart **illustrates which process is executing at each time slice**, giving a visual understanding of RR scheduling fairness.  

---

## 📈 Future Improvements  
- Add dynamic Gantt chart generation from the Round Robin class  
- Output **average waiting time** and **turnaround time** automatically  
- Expand to include **other scheduling algorithms**: FCFS, SJF, Priority  

---

## 🛠️ Tech Used  
- Python 3  
- Object-Oriented Programming  
- Operating System Scheduling Concepts  

---

## 📚 Learning Purpose  
This project was built to **practice operating system scheduling algorithms**, improve understanding of **process management**, and demonstrate **fair CPU allocation in time-sharing systems**.
