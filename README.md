# xnt_gpu_guesser

**GPU ​Hardware Requirements**:​

- ​RAM: Minimum ​12GB​ (the software requires ​11GB​ to run).
- GPU: Nvidia

| Parameter   | Resource Allocation | VRAM Requirement Description                                 |
| ----------- | ------------------- | ------------------------------------------------------------ |
| **`-m 0`**  | GPU-only            | Requires **over 12GB** of VRAM                               |
| **`-m 1`**  | GPU-only            | Requires **over 8GB** of VRAM                                |
| **`-m 2`**  | GPU-only            | Requires **over 7GB** of VRAM                                |
| **`-m 20`** | Hybrid (GPU + CPU)  | Allocates approx. **3GB** of VRAM per instance. Should be used with the `-t N` by setting the number of concurrent instances `N`, ensuring that `3 * N`does not exceed total VRAM. **The default value is `N=3`**.|

## **📌 Mining Tutorial**  

### **1️⃣ Mining Pool Address**  
```bash
-p stratum+tcp://xnt.drpool.io:30120
```

### **2️⃣ Latest Miner Releases**  
🔗 **[Download Here](https://github.com/0xdrpool/xnt_gpu_guesser/blob/main/download.md)**  

### **3️⃣ Mining Guide**  

#### **Basic Command**  
```bash
./dr_xnt_prover -p stratum+tcp://xnt.drpool.io:30120 -w drpoolaccount.xxx
```

### **4️⃣ Register a DRPool Account​**  

[drpool register](https://drpool.io/user/register)

### **5️⃣ USE GPU（Option）**

```bash
# -g
# Indexes of GPUs to use (starts from 0)
# Specify multiple times to use multiple GPUs
# Example: -g 0  -g 0,1,2,3

# -m
# GPU Memory: 0, 1, 20 (default: 0)
# 0: GPU with 12GB+ memory
# 1: GPU with 8GB+ memory
# 20: GPU + CPU，3G * N

# -t N It only works with the -m 20 option.

./dr_neptune_prover -p stratum+tcp://xnt.drpool.io:30120 -w drpoolaccount.xxx -g 0,1,2,3 -m 0
```

---

### **⚙️ HiveOS**

**New Wallet**

Address input your drpool accountname

<img width="596" height="616" alt="image" src="https://github.com/user-attachments/assets/8a621c28-00d9-46a8-9e41-ceca1a2d65a2" />

**Add New Flight Sheet**

<img width="1207" height="275" alt="image" src="https://github.com/user-attachments/assets/ec7599c7-df18-456e-a550-0066679c31d6" />

**Setup Miner Config**

Extra config arguments:
- Miner name: `xntprover`
- Installation URL: `https://pub-7c2f8935763c410d8897cc0d6379670e.r2.dev/xntprover-1.0.0.tar.gz`
- Hash algorithm: `----`
- Wallet and worker template: `%WAL%.%WORKER_NAME%`
- Pool URL: `stratum+tcp://xnt.drpool.io:30120`
- Extra config arguments: 
  ```
  # -g
  # Indexes of GPUs to use (starts from 0)
  # Specify multiple times to use multiple GPUs
  # Example: -g 0  -g 0,1,2,3
  
  # -m
  # GPU Memory: 0, 1, 20 (default: 0)
  # 0: GPU with 10GB+ memory
  # 1: GPU with 8GB+ memory
  # 20: GPU + CPU，3G * N

  # -t N It only works with the -m 20 option.
  ```

<img width="677" height="700" alt="image" src="https://github.com/user-attachments/assets/8566fbc7-4671-4844-b7b3-6a021d46df56" />

**View HiveOS logs**

`tail -f /root/hive/miners/custom/xntprover/xntprover.log -n 100`

<img width="1198" height="849" alt="image" src="https://github.com/user-attachments/assets/8370bb70-52f0-4124-9e9c-fccf6b3c4c2c" />


### **⚙️ Setup on Ubuntu (v18.04+)**  

1. **Get a Mining Address**
   
todo

1. **Download the Miner**  
   - Get the latest `ubuntu-dr_xnt_prover-x.x.x.tar.gz` from **[Download](https://github.com/0xdrpool/neptune_v2_cpu_guesser/blob/main/download.md)**
   ```bash
   # Ubuntu 18.04+
   wget https://pub-7c2f8935763c410d8897cc0d6379670e.r2.dev/ubuntu_20-dr_xnt_prover-1.0.0.tar.gz
   ```
     
3. **Extract & Prepare**  
   ```bash
   tar -zxvf ubuntu-dr_xnt_prover-x.x.x.tar.gz
   cd dr_xnt_prover && chmod +x inner_guesser.sh run_guesser.sh stop_guesser.sh dr_xnt_prover
   ```

4. **Configure Your Account**  
   - Edit `inner_guesser.sh` and update your **[drpool](https://drpool.io) account name**.  

5. **GPU Acceleration**
   - Edit `inner_guesser.sh` and update `./dr_xnt_prover --pool stratum+tcp://xnt.drpool.io:30120 --worker $accountname -g 0 -m 0`

7. **Start Mining**  
   ```bash
   ./start_guesser.sh
   ```
8. **View Mining Logs:**
   ```bash
   tail -n 100 -f guesser.log
   ```
   ![alt text](image.png)
   **Part1**
   1. ​Create the guesser_buffer for later guessing​
   2. The guesser_buffer generation took ​65 seconds.
   
   **Part2**
   
   Mined a valid nonce after proof generation

   **Last 1m speed(KP/s)**

   The proof generation speed per second in the last minute
  
9. **Stop Mining**
   ```bash
   ./stop_guesser.sh
   ```
   
