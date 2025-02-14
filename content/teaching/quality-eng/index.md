---
title: Software Quality Engineering
summary: Concepts relevant to software quality, quality assurance and testing, quality engineering and quality planning. Anomaly prevention and defect classification. Fault tolerance. Software reliability engineering. Quality models. Comparison of different quality assurance techniques. Improving the software development process. Software and process. Identifying risks for quantifiable quality improvement.
date: 2023-10-24
type: docs
math: true
weight: 30
tags:
  - LOG8371
image:
  caption: 'Embed rich media such as videos and LaTeX math'
---

Concepts relevant to software quality, quality assurance and testing, quality engineering and quality planning. Anomaly prevention and defect classification. Fault tolerance. Software reliability engineering. Quality models. Comparison of different quality assurance techniques. Improving the software development process. Software and process. Identifying risks for quantifiable quality improvement.


## Lecture Notes 📚 Log8371


📥 **Download PDF**
[Lec-01](slides/01_Intro.pdf),... ,[Lec-05](slides/05_perf_eng.pdf), [Lec-06](slides/06_perf_model.pdf),..., [Lec-11](slides/11_security_testing.pdf), [Lec-12](slides/12_security_testing_2.pdf),...,[Lec-14](slides/14_Autoscaling.pdf)







## Outline 


```markmap 
- LOG8371
  - Module 1 (Qualité fonctionnelle, Fiabilité)
    - Activités et processus de SQA 
    - Normes de qualité 
    - Assurance de qualité fonctionnelle 
    - Tests unitaires 
    - Tests automatiques
    - Débogage
    - Inspections, audits et revues
    - Vérification et validation 
    - Intégration continue
    - Livraison continue 
    - Conflits de fusion 
  - Module 2 (Efficacité)
    - Performance
    - Profiling 
    - Monitoring 
    - Allocation des ressources 
    - Modèle de performance 
    - Systèmes auto-adaptatifs
    - Autoscaling
  - Module 3 (Sécurité)
    - Tests de pénétration
    - Mitigation des attaques 
    - Chaos Engineering 
    - Systèmes auto-réparateurs 
```



## Models

{{% callout note %}}
Software Performance Engineering (SPE) relies on mathematical models to analyze, predict, and optimize system performance. Here are some commonly used mathematical models for software performance engineering problems:
{{% /callout %}}


---

## **Queuing Theory Models**
Queuing models are widely used to represent software performance issues related to resource contention, response time, and throughput.

### **1.1 Single Queue Model (M/M/1)**
Used for single-server systems where requests arrive randomly.
- \( \lambda \) = arrival rate (requests per second)
- \( \mu \) = service rate (requests per second)
- **Utilization**: 
  \[
  \rho = \frac{\lambda}{\mu}, \quad 0 \leq \rho < 1
  \]
- **Average number of requests in the system**:
  \[
  L = \frac{\rho}{1 - \rho}
  \]
- **Average response time**:
  \[
  R = \frac{1}{\mu - \lambda}
  \]

### **1.2 Multi-server Queuing Model (M/M/c)**
Used for systems with multiple processing units (e.g., web servers with multiple threads).
- \( c \) = number of servers
- **Utilization per server**: 
  \[
  \rho = \frac{\lambda}{c \cdot \mu}
  \]
- **Probability that all servers are busy (Erlang-C formula)**:
  \[
  P_0 = \left[ \sum_{n=0}^{c-1} \frac{(\lambda / \mu)^n}{n!} + \frac{(\lambda / \mu)^c}{c!(1 - \rho)} \right]^{-1}
  \]
- **Expected response time**:
  \[
  R = \frac{1}{\mu} + \frac{P_0 \cdot \rho}{c(1 - \rho) \mu}
  \]

---

### **2. Little’s Law**
This fundamental law relates the number of users in a system to the arrival rate and response time.
\[
L = \lambda \times R
\]
Where:
- \( L \) = average number of requests in the system
- \( \lambda \) = arrival rate of requests
- \( R \) = response time

This law is often used to validate performance models and ensure consistency between measured and predicted values.

---

### **3. Bottleneck Analysis (Utilization Law)**
Bottleneck analysis helps identify the resource that limits system performance.
\[
U_i = X \times S_i
\]
Where:
- \( U_i \) = utilization of resource \( i \)
- \( X \) = system throughput (requests per second)
- \( S_i \) = average service time at resource \( i \)

A system’s maximum throughput is constrained by the slowest component:
\[
X_{\max} = \frac{1}{S_{\max}}
\]

---

### **4. Scalability Model (Amdahl’s Law)**
Amdahl’s Law predicts the maximum speedup of a system when parallelizing a portion of the workload.
\[
S(p) = \frac{1}{(1 - \sigma) + \frac{\sigma}{p}}
\]
Where:
- \( S(p) \) = speedup with \( p \) processors
- \( \sigma \) = fraction of execution time that is parallelizable
- \( p \) = number of processors

For large \( p \), the speedup is limited by the non-parallelizable portion \( (1 - \sigma) \).

---

### **5. Gunther’s Universal Scalability Law (USL)**
Gunther’s model improves Amdahl’s Law by considering contention and coherence costs:
\[
S(p) = \frac{p}{1 + \alpha(p - 1) + \beta p(p - 1)}
\]
Where:
- \( \alpha \) = contention factor (how much resources compete for shared resources)
- \( \beta \) = coherence penalty (overhead from synchronization)
- \( S(p) \) = speedup with \( p \) processors

This model helps predict performance degradation due to parallelism overhead.

---

### **6. Response Time Model (Mean Value Analysis)**
For multi-tier systems (e.g., web applications), response time at each tier can be estimated as:
\[
R_i = S_i \times (1 + N_i)
\]
Where:
- \( R_i \) = response time at resource \( i \)
- \( S_i \) = service time at resource \( i \)
- \( N_i \) = average number of requests in queue at resource \( i \)

The total response time is:
\[
R_{\text{total}} = \sum_{i=1}^{n} R_i
\]

---

### **7. Probabilistic Latency Model**
For applications that depend on multiple services with different latencies, response time follows a probabilistic distribution.
If each service \( i \) has a mean response time \( R_i \) and a probability \( P_i \) of being called, then the expected response time is:
\[
E[R] = \sum_{i=1}^{n} P_i \times R_i
\]

This is useful in microservices architectures where different services contribute to overall latency.

---

### **8. Load Testing Model (Throughput and Concurrency)**
The relationship between throughput, response time, and number of concurrent users is:
\[
X = \frac{N}{R}
\]
Where:
- \( X \) = throughput (requests/sec)
- \( N \) = number of concurrent users
- \( R \) = response time

If load increases beyond system capacity, response time grows exponentially.

---

### **9. Failure Rate and Reliability Models**
The probability of system failure follows an exponential distribution:
\[
R(t) = e^{-\lambda t}
\]
Where:
- \( R(t) \) = reliability (probability the system runs without failure up to time \( t \))
- \( \lambda \) = failure rate

For software systems, failure rate often decreases over time as bugs are fixed.

---

### **10. Cost-Benefit Model for Performance Optimization**
Optimizing performance often has associated costs. The trade-off between cost and performance can be modeled as:
\[
C_{\text{total}} = C_{\text{infra}} + C_{\text{latency}} + C_{\text{failure}}
\]
Where:
- \( C_{\text{infra}} \) = cost of additional hardware/cloud resources
- \( C_{\text{latency}} \) = lost revenue due to slow response time
- \( C_{\text{failure}} \) = downtime-related costs

Minimizing \( C_{\text{total}} \) ensures cost-effective performance improvements.

---

### **Conclusion**
These mathematical models provide a foundation for analyzing and improving software performance. They help predict system behavior, identify bottlenecks, and optimize resources effectively. By applying these models, engineers can ensure software applications meet performance requirements efficiently.


## **PID Controller in Software Performance Engineering**

A **Proportional-Integral-Derivative (PID) Controller** is a feedback control mechanism widely used in software performance engineering for tasks such as **autoscaling, latency management, and resource allocation**. It dynamically adjusts system parameters based on performance deviations.

---

## **1. PID Controller Equation**
A PID controller computes the corrective action \( u(t) \) using three components: Proportional (P), Integral (I), and Derivative (D):

\[
u(t) = K_p e(t) + K_i \int_{0}^{t} e(\tau) d\tau + K_d \frac{d}{dt} e(t)
\]

Where:
- \( u(t) \) = control output (e.g., CPU allocation, number of servers)
- \( e(t) \) = error between desired performance and actual performance:
  
  \[
  e(t) = R_{\text{target}} - R_{\text{actual}}
  \]
  
- \( K_p \) = Proportional gain (adjusts based on immediate error)
- \( K_i \) = Integral gain (adjusts based on accumulated past errors)
- \( K_d \) = Derivative gain (adjusts based on predicted future errors)
- \( R_{\text{target}} \) = target performance metric (e.g., response time)
- \( R_{\text{actual}} \) = actual observed performance metric

---

## **2. Discrete-Time PID Controller**
In software systems, performance metrics are sampled at discrete time intervals (\( k \)). The discrete PID formula is:

\[
u_k = K_p e_k + K_i \sum_{i=0}^{k} e_i \Delta t + K_d \frac{e_k - e_{k-1}}{\Delta t}
\]

Where:
- \( u_k \) = control output at time step \( k \)
- \( e_k \) = error at time step \( k \)
- \( \Delta t \) = sampling interval

In **discrete implementation**, the integral is approximated as a sum:

\[
I_k = I_{k-1} + e_k \Delta t
\]

And the derivative as a difference:

\[
D_k = \frac{e_k - e_{k-1}}{\Delta t}
\]

Thus, the final control equation becomes:

\[
u_k = K_p e_k + K_i I_k + K_d D_k
\]

---

## **3. Application in Software Performance Engineering**
### **Autoscaling for Cloud Resources**
- **Objective**: Adjust the number of virtual machines (VMs) dynamically based on system load.
- **Error Signal**: Difference between target response time and measured response time.
- **Control Output**: Number of VMs to add or remove.

\[
\text{VMs}_{\text{new}} = \text{VMs}_{\text{current}} + u_k
\]

### **Response Time Optimization**
- **Objective**: Minimize response time in web applications.
- **Error Signal**: Difference between target latency and actual latency.
- **Control Output**: Request queue size limit or CPU allocation.

\[
\text{CPU}_{\text{new}} = \text{CPU}_{\text{current}} + u_k
\]

### **Database Query Rate Limiting**
- **Objective**: Prevent overload on a database by controlling query rates.
- **Error Signal**: Difference between allowed and actual queries per second.
- **Control Output**: Maximum query rate.

\[
\text{Rate}_{\text{new}} = \text{Rate}_{\text{current}} + u_k
\]

---

## **4. Choosing PID Parameters**
The effectiveness of a PID controller depends on tuning the parameters \( K_p, K_i, K_d \):

- **\( K_p \) (Proportional Gain)**: Large values lead to **faster response** but may cause instability.
- **\( K_i \) (Integral Gain)**: Large values **reduce steady-state error** but may cause overshoot.
- **\( K_d \) (Derivative Gain)**: Large values help in **predicting future errors** but may amplify noise.

### **Ziegler-Nichols Tuning Method**
A common method for tuning PID parameters:
1. Set \( K_i = 0 \) and \( K_d = 0 \).
2. Increase \( K_p \) until system oscillates (critical gain \( K_c \)).
3. Find the oscillation period \( T_c \).
4. Use tuning rules:

| Control Type | \( K_p \) | \( K_i \) | \( K_d \) |
|-------------|----------|----------|----------|
| P          | 0.5 \( K_c \) | 0 | 0 |
| PI         | 0.45 \( K_c \) | \( 1.2 K_c / T_c \) | 0 |
| PID        | 0.6 \( K_c \) | \( 2 K_c / T_c \) | \( K_c T_c / 8 \) |

---

## **5. Stability Analysis (Laplace Transform)**
The PID controller in Laplace domain is:

\[
U(s) = (K_p + K_i \frac{1}{s} + K_d s) E(s)
\]

The closed-loop system is:

\[
G(s) = \frac{U(s) G_{\text{plant}}(s)}{1 + U(s) G_{\text{plant}}(s)}
\]

The characteristic equation:

\[
1 + (K_p + K_i \frac{1}{s} + K_d s) G_{\text{plant}}(s) = 0
\]

Stability is determined using:
- **Root locus method**
- **Bode plot for frequency response**
- **Nyquist criterion**

---

## **6. Example: PID for Autoscaling Web Servers**
**Given Data:**
- **Target response time**: \( R_{\text{target}} = 200ms \)
- **Measured response time**: \( R_{\text{actual}} = 300ms \)
- **Sampling time**: \( \Delta t = 5s \)
- **Initial number of servers**: 10
- **PID Parameters**: \( K_p = 1.5, K_i = 0.1, K_d = 0.5 \)

**Step 1: Compute Error**
\[
e_k = R_{\text{target}} - R_{\text{actual}} = 200 - 300 = -100ms
\]

**Step 2: Compute PID Terms**
\[
P_k = K_p \cdot e_k = 1.5 \cdot (-100) = -150
\]

\[
I_k = I_{k-1} + K_i e_k \Delta t = 0 + 0.1 \times (-100) \times 5 = -50
\]

\[
D_k = K_d \frac{e_k - e_{k-1}}{\Delta t} = 0.5 \frac{(-100) - (-50)}{5} = -5
\]

**Step 3: Compute Control Output**
\[
u_k = P_k + I_k + D_k = -150 - 50 - 5 = -205
\]

**Step 4: Update Number of Servers**
\[
\text{Servers}_{\text{new}} = \text{Servers}_{\text{current}} + u_k = 10 - 2 = 8
\]

If \( u_k \) is negative, it means reducing the number of servers.

---

## **7. Conclusion**
The PID controller is a powerful tool in **software performance engineering**, allowing dynamic resource management by **continuously adjusting** system parameters. It is applied in:
- **Autoscaling cloud resources**
- **Latency and throughput optimization**
- **Database rate limiting**

By tuning the parameters correctly, it ensures that **performance targets are met** while **avoiding oscillations and instability**.


## **Dynamic Layered Queuing Networks (LQN)**

## **1. Overview of Dynamic LQN**
Layered Queuing Networks (LQNs) extend traditional queuing models to capture the interaction between multiple software and hardware layers, often representing client-server, microservices, and cloud-based architectures. 

A **Dynamic LQN (DLQN)** incorporates time-varying workload, adaptive resource allocation, and system behavior changes over time. These models help predict performance bottlenecks, optimize system capacity, and adjust service strategies dynamically.

---

## **2. Basic Mathematical Formulation of LQN**
LQNs describe a system as a set of **tasks** and **entries**, where:
- **Tasks (\( T_i \))** represent processing elements (e.g., database, application server).
- **Entries (\( E_i \))** represent functions or operations executed within a task.
- **Calls (\( C_{ij} \))** denote interactions between tasks.

Each task \( T_i \) has:
- **Arrival rate** \( \lambda_i(t) \) (requests per second)
- **Service demand** \( S_i(t) \) (time per request)
- **Queue discipline** \( Q_i \) (e.g., FIFO, priority-based)

### **Queuing Equations for a Single Layer**
For a task \( T_i \), the response time \( R_i \) is:
\[
R_i = S_i + \frac{Q_i}{1 - \rho_i}
\]
where:
- \( \rho_i = \frac{\lambda_i S_i}{m_i} \) is the utilization of task \( T_i \) (with \( m_i \) parallel servers),
- \( Q_i \) is the waiting time due to other tasks.

The total throughput for task \( i \) is given by:
\[
X_i = \frac{\lambda_i}{1 + \sum_{j \in C_{i}} P_{ij} R_j}
\]
where:
- \( P_{ij} \) is the probability that \( T_i \) calls \( T_j \),
- \( R_j \) is the response time of task \( j \).

---

## **3. Dynamic Extension of LQN (DLQN)**
To model dynamic behavior, we introduce time-dependent parameters.

### **State Equations in Dynamic LQN**
For each task \( T_i \), the **state equation** models the queue evolution over time:
\[
\frac{dN_i(t)}{dt} = \lambda_i(t) - \mu_i(t) N_i(t)
\]
where:
- \( N_i(t) \) is the number of requests in task \( i \) at time \( t \),
- \( \lambda_i(t) \) is the dynamic arrival rate,
- \( \mu_i(t) \) is the service rate.

### **Dynamic Resource Allocation**
A key aspect of DLQN is **adaptive resource allocation**:
\[
m_i(t) = \max \left( 1, \frac{\lambda_i(t) S_i}{\rho_{\text{max}}} \right)
\]
where \( \rho_{\text{max}} \) is the maximum allowable utilization.

The **adjusted service rate**:
\[
\mu_i(t) = \frac{m_i(t)}{S_i}
\]

### **Dynamic Scaling**
If a system auto-scales by adding/removing instances:
\[
m_i(t+1) = m_i(t) + \Delta m_i
\]
where \( \Delta m_i \) is calculated based on:
\[
\Delta m_i = k_p e(t) + k_i \int e(\tau) d\tau + k_d \frac{d e(t)}{dt}
\]
where \( e(t) = \rho_i - \rho_{\text{target}} \) and \( k_p, k_i, k_d \) are PID controller gains.

---

## **4. Performance Metrics in DLQN**
**System Response Time (End-to-End)**
\[
R_{\text{sys}}(t) = \sum_{i=1}^{n} P_i R_i(t)
\]
where \( P_i \) is the probability that a request visits task \( i \).

**Utilization at Time \( t \)**
\[
U_i(t) = \frac{\lambda_i(t) S_i}{m_i(t)}
\]
where \( U_i(t) \leq 1 \) ensures the system does not overload.

**Throughput Over Time**
\[
X_{\text{sys}}(t) = \frac{\lambda_{\text{entry}}(t)}{1 + \sum_{i=1}^{n} P_i R_i(t)}
\]

---

## **5. Example: Dynamic LQN for Cloud Autoscaling**
### **Scenario: Web Application with 3 Tiers**
- **Task 1**: Load Balancer (\( T_1 \))
- **Task 2**: Web Server (\( T_2 \))
- **Task 3**: Database (\( T_3 \))

### **Step 1: Define Arrival Rate**
\[
\lambda_1(t) = \lambda_{\text{users}}(t)
\]

### **Step 2: Compute Response Time per Layer**
\[
R_1(t) = S_1 + \frac{Q_1}{1 - \rho_1}
\]

\[
R_2(t) = S_2 + \frac{Q_2}{1 - \rho_2}
\]

\[
R_3(t) = S_3 + \frac{Q_3}{1 - \rho_3}
\]

### **Step 3: Compute System Response Time**
\[
R_{\text{sys}}(t) = R_1(t) + P_{12} R_2(t) + P_{23} R_3(t)
\]

### **Step 4: Adjust Resources Dynamically**
Using PID control:
\[
\Delta m_2 = k_p e_2 + k_i \int e_2 d\tau + k_d \frac{d e_2}{dt}
\]

where \( e_2 = \rho_2 - 0.8 \) ensures the web server operates below 80% utilization.

### **Step 5: Compute Throughput**
\[
X_{\text{sys}}(t) = \frac{\lambda_1(t)}{1 + P_{12} R_2(t) + P_{23} R_3(t)}
\]

---

## **6. Conclusion**
Dynamic LQN (DLQN) extends standard LQN models by incorporating **time-dependent queuing equations**, **adaptive resource allocation**, and **autoscaling mechanisms**. It is particularly useful in **cloud computing, microservices architectures, and dynamic performance modeling**.

This model allows for:
1. **Predicting workload changes** and adjusting resources accordingly.
2. **Reducing latency** by dynamically adapting queue processing.
3. **Ensuring scalability** using PID-based autoscaling.

Using these equations, performance engineers can **simulate, optimize, and manage** complex distributed systems dynamically.


## Code


```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint
import numpy as np
import matplotlib.pyplot as plt
```

Global variables

```python
time = 0
integral = 0
time_prev = -1e-6
e_prev = 0
```

The function below calculates the value of manipulated variable (MV) based on the measured value (in example it is the temperature of the liquid) and setpoint value (temperature we want to obtain).

```python
def PID(Kp, Ki, Kd, setpoint, measurement):
    global time, integral, time_prev, e_prev

    # Value of offset - when the error is equal zero
    offset = 320
    
    # PID calculations
    e = setpoint - measurement
        
    P = Kp*e
    integral = integral + Ki*e*(time - time_prev)
    D = Kd*(e - e_prev)/(time - time_prev)

    # calculate manipulated variable - MV 
    MV = offset + P + integral + D
    
    # update stored data for next iteration
    e_prev = e
    time_prev = time
    return MV
```


```python
def system(t, temp, Tq):
    epsilon = 1
    tau = 4
    Tf = 300
    Q = 2
    dTdt = 1/(tau*(1+epsilon)) * (Tf-temp) + Q/(1+epsilon)*(Tq-temp)
    return dTdt
```    


```python
tspan = np.linspace(0,10,50)
Tq = 320,
sol = odeint(system,300, tspan, args=Tq, tfirst=True)
plt.xlabel('Time')
plt.ylabel('Temperature')
plt.plot(tspan,sol)
```

```python
# number of steps
n = 250
time_prev = 0
y0 = 300
deltat = 0.1
y_sol = [y0]
t_sol = [time_prev]
# Tq is chosen as a manipulated variable
Tq = 320,
q_sol = [Tq[0]]
setpoint = 310
integral = 0
for i in range(1, n):
    time = i * deltat
    tspan = np.linspace(time_prev, time, 10)
    Tq = PID(0.6, 0.2, 0.1, setpoint, y_sol[-1]),
    yi = odeint(system,y_sol[-1], tspan, args = Tq, tfirst=True)
    t_sol.append(time)
    y_sol.append(yi[-1][0])
    q_sol.append(Tq[0])
    time_prev = time

plt.plot(t_sol, y_sol)
plt.xlabel('Time')
plt.ylabel('Temperature')
```


