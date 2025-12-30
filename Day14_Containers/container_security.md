## Day 14 – Container Security

### Scenario Overview

Wareville woke up to another incident when DoorDasher, the city’s popular food delivery platform, was defaced and rebranded as **Hopperoo** by King Malhare and his bandit bunnies. Reports flooded in from customers and regulators after contaminated meals were allegedly delivered, causing widespread panic.

A security engineer prepared a recovery script to restore the service, but before it could be executed, the attacker locked them out of the system. With traditional access blocked, the SOC team identified one remaining entry point: a **monitoring container (uptime-checker)** still running on the host.

### My Role

I acted as a **SOC / Blue Team Analyst**, tasked with investigating the containerized environment, identifying security misconfigurations, escaping a vulnerable container, escalating privileges, and restoring the DoorDasher service.

### Tools Used

* Docker
* Linux command line
* Docker CLI
* Container runtime (Docker Engine)
* Web browser (service validation)

### Investigation Approach

I began by enumerating all running Docker containers to understand the environment and identify potential access points. After locating the **uptime-checker** container, I accessed it interactively and inspected its filesystem and permissions.

During analysis, I discovered that the container had access to the **Docker socket (`/var/run/docker.sock`)**, a critical misconfiguration that allowed direct interaction with the Docker daemon. This effectively granted control over the host’s containers.

Using this access, I pivoted from the monitoring container into a **privileged deployer container**, where the recovery script was stored. From there, I escalated privileges and executed the script to restore the original DoorDasher service.

### Key Findings

* A monitoring container had unrestricted access to the Docker socket.
* Docker socket exposure allowed full interaction with the Docker daemon.
* Container isolation was broken, enabling **container escape**.
* A privileged container contained a recovery script capable of restoring the service.
* The attacker relied on container misconfiguration rather than a kernel exploit.

### Outcome

By exploiting the exposed Docker socket and escalating privileges:

* I successfully escaped the compromised container
* Accessed a privileged container
* Executed the recovery script
* Restored DoorDasher to its original state

This investigation demonstrated how a **single container misconfiguration** can lead to full host compromise.

### Useful Commands Used in This Challenge

| Purpose                                    | Command                             |
| ------------------------------------------ | ----------------------------------- |
| List running containers                    | `docker ps`                         |
| Enter a running container                  | `docker exec -it uptime-checker sh` |
| Check Docker socket access                 | `ls -la /var/run/docker.sock`       |
| Interact with Docker from inside container | `docker ps`                         |
| Access privileged container                | `docker exec -it deployer bash`     |
| Confirm current user                       | `whoami`                            |
| Restore service                            | `sudo /recovery_script.sh`          |

### Skills & Concepts Learned

* Container vs virtual machine architecture
* Docker images, containers, and runtime behavior
* Docker socket security risks
* Container escape techniques
* Privilege escalation via container misconfiguration
* Real-world impact of insecure container deployments
