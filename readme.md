# Ansible + Docker Compose Deployment

A hands-on DevOps practice project that demonstrates how to use **Ansible to automate the deployment of a multi-container application using Docker Compose.

The project is designed to understand the relationship between:

Ansible → Docker → Docker Compose → Application

The application is containerized using Docker Compose, while Ansible automates the setup and deployment process.

## Architecture

```text
                    Ansible
                       |
                       | SSH / Local Connection
                       v
              +-------------------+
              |   Target Machine  |
              |                   |
              |      Docker       |
              |         |         |
              |   Docker Compose  |
              +---------|---------+
                        |
              +---------+---------+
              |                   |
          Backend               Nginx
          Container             Container
```

## Project Structure

```text
Ansible_Practise_DockerCompose/
│
├── app_code/
│   ├── Backend/
│   │   └── ...
│   │
│   ├── Nginx/
│   │   └── ...
│   │
│   ├── docker-compose.yaml
│   ├── .gitignore
│   └── README.md
│
├── deploy_docker_app.yaml
├── local_inventory
└── README.md
```

### `app_code/`

Contains the application and Docker Compose configuration.

The Docker Compose file defines the containers/services required to run the application.

### `deploy_docker_app.yaml`

The main Ansible playbook responsible for automating the deployment.

Typical responsibilities include:

* Installing required packages
* Installing Docker
* Ensuring the Docker service is running
* Installing Docker Compose
* Preparing the application
* Starting the Docker Compose application

### `local_inventory`

Ansible inventory defining the hosts on which the playbook should run.

For this practice project, the inventory is configured for local deployment.

## Technologies Used

* Ansible — Infrastructure automation and configuration management
* Docker — Application containerization
* Docker Compose — Multi-container application orchestration
* Linux / WSL — Development environment
* Git / GitHub — Version control

## Prerequisites

Make sure the following are installed:

* Linux / WSL
* Ansible
* Docker
* Docker Compose

Verify the installations:

```bash
ansible --version
docker --version
docker compose version
```

## Running the Project

Clone the repository:

```bash
git clone https://github.com/KaarthikeyanB02/Ansible_Practise_DockerCompose.git
```

Navigate into the project:

```bash
cd Ansible_Practise_DockerCompose
```

Check the Ansible inventory:

```bash
cat local_inventory
```

Run the playbook:

```bash
ansible-playbook -i local_inventory deploy_docker_app.yaml
```

If the playbook requires privilege escalation:

```bash
ansible-playbook -i local_inventory deploy_docker_app.yaml --ask-become-pass
```

## Verify the Deployment

After Ansible completes successfully, check the running containers:

```bash
docker compose ps
```

You can also check all running containers:

```bash
docker ps
```

To view application logs:

```bash
docker compose logs
```

To follow logs in real time:

```bash
docker compose logs -f
```

## Stopping the Application

Navigate to the application directory:

```bash
cd app_code
```

Stop the containers:

```bash
docker compose down
```

To start them again:

```bash
docker compose up -d
```

## What This Project Demonstrates

This project is primarily intended as a learning exercise for understanding infrastructure automation.

The main concepts practiced are:

1. **Ansible Inventory**

   * Defining target hosts
   * Running playbooks against hosts

2. **Ansible Playbooks**

   * Tasks
   * Variables
   * Privilege escalation
   * Idempotent configuration

3. **Docker Installation and Configuration**

   * Installing Docker
   * Managing the Docker service

4. **Docker Compose**

   * Defining multiple services
   * Starting and stopping services
   * Managing application containers

5. **Infrastructure Automation**

Instead of manually executing:

```bash
apt install docker
docker compose up -d
```

the goal is to let Ansible perform the required setup and deployment automatically.

## Deployment Flow

```text
Developer
    |
    | git clone
    v
Project Repository
    |
    | ansible-playbook
    v
Ansible
    |
    +--> Install required packages
    |
    +--> Configure Docker
    |
    +--> Prepare application
    |
    +--> Start Docker Compose
    |
    v
Running Containers
```

## Learning Goal

The main goal of this project is to move from manually managing Docker applications toward **automated infrastructure and application deployment using Ansible**.
