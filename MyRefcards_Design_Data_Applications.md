# Designing Data Intensive Applications

## Important concerns in software systems

- Reliability
  - Prevent Hardware Faults
    - Harddisk failure : Disks may be set up in a RAID configuration
    - Faulty RAM
    - Powergrid blackout : servers may havedual power supplies and hot-swappable CPUs, and datacenters may have batteries and dieselgenerators for backup power
    - Network failure
  - Prevent Software Errors
    - it can constantly check itself while it is running and raise an alert if a discrepancy is found
  - Prevent Human Errors
    - Design systems with minimal opportunities for error
    - Decouple the places where people make the most mistakes from the places where they can causefailures
    - Test thoroughly at all levels, from unit tests to whole-system integration tests and manual tests
    - Set up detailed and clear monitoring, such as performance metrics and error rates
- Scalability : Scalability is the term we use to describe a system’s ability to cope with increased load
    - When you increase a load parameter and keep the system resources (CPU, memory, network bandwidth,etc.) unchanged, how is the performance of your system affected?
    - When you increase a load parameter, how much do you need to increase the resources if you want tokeep performance unchanged?
    - LATENCY : Latency is the duration that a request is waiting tobe handled—during which it is latent, awaiting service
    - Response Time : The responsetime is what the client sees: besides the actual time to process the request (the service time),it includes network delays and queueing delays.
- Maintainability
    - Operbility : Make it easy for operations teams to keep the system running smoothly.
    - Simplicity : removing complexity to Make it easy for new engineers to understand the system
    - Evolvability : Make it easy for engineers to make changes to the system in the future
