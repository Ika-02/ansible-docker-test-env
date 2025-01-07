# Ansible Playground

This document provides instructions on how to set up and use an Ansible environment with Docker. It includes steps to check the Ansible installation, install a web server and a database, run Ansible playbooks, and some useful Ansible commands.

## Environment Customization 🛠️

This environment is based on Alpine containers and can be easily customized using the `compose.yml` file. You can change the names of the containers, exposed ports, and other settings to fit your needs.

## Launching the Environment 🚀

### Cloning the Repository 🌀

To get a local copy of this repository, use the following command. This will clone the repository to your local machine.

```sh
git clone https://github.com/Ika-02/ansible-docker-test-env.git
```

Navigate to the repository directory:

```sh
cd ansible-docker-test-env
```

### Fire It Up 🔥

To start the Docker environment, use the following command. This will build and run the Docker containers defined in the `compose.yml` file (be sure to be in the `ansible` folder).

```sh
docker compose up --build
```

## Check Ansible Installation ✅

Verify that Ansible is installed and check its version with the following command inside the `ansible` container.

```sh
ansible --version
```

## Using the Shared Folder 📁

The `shared` folder can be used to add configuration files to the Ansible master container. 

This folder is mounted into the container and set as working directory, allowing you to easily manage and access your configuration files from within the container.

## Install a Web Server 🌐

Follow these steps to install and start an Apache web server on your target machines using Ansible.

```sh
ansible web -i inventory.yml -m apk -a "name=apache2 state=present"

ansible web -i inventory.yml -m service -a "name=apache2 state=started"

ansible web -i inventory.yml -m shell -a "service apache2 status"
```

## Install DB 🗄️

Use the following commands to install and configure a MariaDB database on your target machines using Ansible.

```sh
ansible db -i inventory.yml -m apk -a "name=mysql state=present"

ansible db -i inventory.yml -m shell -a "/etc/init.d/mariadb setup"

ansible db -i inventory.yml -m service -a "name=mariadb state=started"

ansible db -i inventory.yml -m shell -a "service mariadb status"
```

## Running Ansible Playbooks 📜

To run an Ansible playbook, use the following command. This will execute the tasks defined in your `playbook.yml` file on the hosts specified in your `inventory.yml`.

```sh
ansible-playbook -i inventory.yml playbook.yml
```

## Useful Ansible Commands 🛠️

Here are some useful Ansible commands for checking playbook syntax, listing tasks, and performing a dry run.

- Check the syntax of a playbook:

```sh
ansible-playbook --syntax-check playbook.yml
```

- List the tasks that will be executed:

```sh
ansible-playbook --list-tasks playbook.yml
```

- Execute a playbook in check mode (dry run):

```sh
ansible-playbook --check playbook.yml
```

## References 📚

For more information, refer to the official documentation of Ansible, Docker, Apache, and MariaDB.

- [Ansible Documentation](https://docs.ansible.com/)
- [Docker Documentation](https://docs.docker.com/)
- [Apache Documentation](https://httpd.apache.org/docs/)
- [MariaDB Documentation](https://mariadb.com/kb/en/documentation/)
- [Alpine Linux Documentation](https://wiki.alpinelinux.org/wiki/Main_Page)

## Disclaimer ⚠️

This repository is maintained by a student and may not be perfect. Contributions and suggestions for improvements are welcome.

## Acknowledgements 🙏

This repository is partially based on the work from [shellwhale/ansible-docker-playground](https://github.com/shellwhale/ansible-docker-playground).
