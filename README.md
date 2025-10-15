# CBWO: A Novel Multi-objective Load Balancing Technique for Cloud Computing

This project is a Java-based implementation and replication of the research paper **"CBWO: A Novel Multi-objective Load Balancing Technique for Cloud Computing"**. The simulation is built using the **CloudSim 4.0** framework and aims to create a validated baseline of the CBWO algorithm for future research and hybridization.  

This README tracks the project lifecycle, from initial setup and dependency management to the iterative process of analysis and refinement that led to a successful replication of the paper's results.

---

## Dependencies & Environment Setup

To ensure compatibility and reproducibility, this project uses specific software versions:

### Software Requirements
- **Java Development Kit (JDK):** Version 8 (e.g., OpenJDK 8u202+)
- **IDE:** Apache NetBeans 12.3
- **Simulation Framework:** CloudSim 4.0

### Required Libraries (JARs)
Add the following JAR files to the project libraries in NetBeans:
- `cloudsim-4.0.jar`
- `cloudsim-examples-4.0.jar`
- `commons-math3-3.6.1.jar`
- `opencsv-2.3.jar`

---

## Project Structure

The simulation logic is organized into three main classes:

- **`CBWOSimulation.java`**: Main driver class; initializes the CloudSim environment, creates datacenters and broker, starts the simulation, and prints results.  
- **`CloudSimHelper.java`**: Utility class for creating simulation entities (Datacenters, Hosts, VMs, and Cloudlets) based on paper parameters.  
- **`CBWOBroker.java`**: Custom broker extending CloudSim's `DatacenterBroker`. Implements the **Chaotic Black Widow Optimization (CBWO)** algorithm, including chaotic maps, genetic operators (procreation, cannibalism, mutation), and the fitness function.  

---

## Replication Journey: Analysis and Refinement

### Run 1: Initial Implementation
- **Configuration:** 10 hosts, 50 VMs, 200 identical tasks  
- **Result:** VM allocation failed due to insufficient RAM  
- **Makespan:** ~2560s  
- **Analysis:** Homogeneous workload caused stagnation in CBWO optimization  

### Run 2: Fixing Resource Allocation
- **Change:** Increased hosts from 10 to 13  
- **Result:** All VMs created successfully  
- **Makespan:** ~2240s  
- **Analysis:** Algorithm still not optimizing due to identical tasks  

### Run 3: Introducing Heterogeneity
- **Change:** Tasks now have random lengths between 1,000 and 20,000 MI  
- **Result:** CBWO algorithm began optimizing  
- **Makespan:** ~525s  
- **Analysis:** Heterogeneous workload improved optimization (~76% improvement)  

### Run 4: Investigating Hardware Ambiguity
- **Hypothesis:** Low VM MIPS caused discrepancy with paper results  
- **Change:** Increased VM MIPS to 1000  
- **Result:** Simulation failed due to insufficient host MIPS  

### Run 5: Balancing the Infrastructure
- **Change:** Increased Host MIPS from 1000 to 4000  
- **Result:** Successful simulation, effective CBWO optimization  
- **Makespan:** ~141s  

### Run 6: Final Alignment with Paper Parameters
- **Changes:**  
  - 10 datacenters, 6 hosts each  
  - Hosts: 40,000 MIPS, 32GB RAM  
  - Heterogeneous VMs with random RAM (256–2048 MB) and bandwidth (500–1000 Mbit/s)  
  - CBWO algorithm: 10 iterations, population size 10  
  - VM MIPS inferred as 4000  
- **Result:** Simulation ran perfectly, optimizing makespan from 39.5s → 36.6s  
- **Final Makespan:** 36.80s (near paper result of 36.44s)  

---

## Conclusion

This project successfully replicates the findings of the CBWO paper, validating that the algorithm effectively reduces makespan in a cloud environment. The codebase serves as a reliable baseline for future research on hybrid load balancing algorithms.

---

## How to Run the Simulation

1. Open the project in **NetBeans IDE**.  
2. Ensure all required **JAR files** are added to the project libraries.  
3. Navigate to `Source Packages > cbwo.simulation`.  
4. Right-click on `CBWOSimulation.java` and select **Run File**.  
5. Simulation progress and final results will be printed in the **Output** window.

---
