# 🚦 Traffic Signal Simulation System (C, POSIX Threads)

A multithreaded **Traffic Signal Simulation System** implemented in **C**, demonstrating:

- Process & thread management  
- Mutex synchronization  
- Condition variables  
- Event scheduling  
- File I/O  
- Emergency handling  
- Concurrent logging  

This project was created as part of the **Computer System Programming** course and showcases real-world systems concepts using a traffic intersection simulation.

## 📌 Features

### ✔ Event-Driven Simulation  
Reads events from `events.txt`:

```
<time> vehicle <lane> <count>
<time> emergency
```

Automatically adds vehicles and triggers emergencies based on timestamps.

### ✔ Two-Thread Architecture  
- **Event Scheduler Thread**  
  Handles event timing, vehicle arrivals, and emergency triggers.
  - **Emergency Handler Thread**
      Managing Emergency situations

- **Traffic Controller Thread**  
  Controls lanes, manages green timing, and processes vehicles.
  


### ✔ Emergency Pause + Resume  
- Emergency immediately pauses all lanes  
- Controller waits using a condition variable  
- Auto-clear thread simulates emergency ending  
- Controller resumes remaining green time seamlessly

### ✔ Thread-Safe Logging  
Logs every state change to both console and `traffic_log.txt` using a dedicated mutex.

## 🧠 System Architecture

```
events.txt
      |
      v
+------------------+
| Event Scheduler  |
+------------------+
| Loads events     |
| Triggers updates |
+--------+---------+
         |
         v
+----------------------+
| Traffic Controller   |
+----------------------+
| Green/Red cycles     |
| Pass vehicles        |
| Handle emergencies   |
+----------------------+
```

## 📂 Project Structure

```
.
├── traffic_controller.c      # Main simulation source code
├── events.txt         # Input event script
├── traffic_log.txt    # Auto-generated log output
└── README.markdown    # Documentation
```

## 🛠 Build & Run

### Compile:

```bash
gcc traffic_controller.c -o traffic -pthread
```

### Run:

```bash
./traffic
```

Output will appear in:

- Console  
- `traffic_log.txt` (auto-created)

## 📝 Input Format (`events.txt`)

```
# time type lane count
0  vehicle  0  5
2  vehicle  1  3
5  emergency
10 vehicle  2  4
```

## 🔧 Key Concepts Demonstrated

### 🧵 POSIX Threads (`pthread`)
- `pthread_create`
- `pthread_join`
- Detached threads

### 🔒 Synchronization
- Mutex locks for shared state  
- Condition variables for waiting and signaling

### 🗃️ File I/O
- Reading events (`fopen`, `fgets`, `sscanf`)  
- Writing logs (`fprintf`, `fflush`)

### 📡 Real-Time Simulation Techniques
- Simulated time scaling  
- Sleep intervals using `usleep`  

### 🚨 Emergency Handling
- Pause controller instantly  
- Auto-clear using another thread  
- Resume logic using `cvResume`

## 📜 Example Log Output

```
Traffic simulation started
Time 0: Added 5 vehicles to lane 0, total = 5
Lane 0 GREEN for 10 seconds
Lane 0: Vehicle passed. Remaining: 4
...
Time 5: Emergency triggered!
Emergency pause detected: all RED, waiting...
Emergency auto-cleared (simulated).
Controller resumed after emergency.
Simulation complete.
```

## 🚀 Possible Extensions

- IPC using **pipes** to send events from another process  
- Use **Unix signals (SIGUSR1)** to trigger emergencies  
- Add **TCP sockets** to receive events from a client  
- Simulate **multiple intersections**  
- Add GUI using SDL or ncurses

## 🙌 Credits

| Name / Username |
|-----------------|
|[Yash Oza](https://github.com/Yash-Oza-ui)|
|[Dhvanit Shah](https://github.com/shahdhvanit)|
|[Tanishq Shah](https://github.com/Tanishq7361)|
|[Harshil Shah](https://github.com/Harshil607)|
|Het Kapadiya| 

## 🤝 Contributing
Pull requests and issue reports are welcome.

## 📄 License
This project is open-source under the **MIT License**.
