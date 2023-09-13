# cribl-workshops

The goal of this project is to provide a relatively quick and easy way to provide custom workshops with Cribl Stream and Cribl Edge.

The python scripts spin up an arbitrary number of EC2 hosts and create a hosts.yml file.  An Ansible playbook takes it from there to deploy Docker et al, then your choice from [one] custom docker-compose.yml file will spin up a Cribl Stream Leader node and a Cribl Worker node on each host.

### How to get started

- If you have Git, clone the repo.
    ```
    git clone https://github.com/berthayes/cribl-workshops.git
    cd cribl-workshops
    ```

- If you don't have Git, download the .zip file, unzip it and get in there.

- Edit the `yak_shaving.conf` config file

- Spin up some EC2 hosts
    ```
    python3 create_aws_instances.py -n 3
    ```

- Consider how long it might take to spin up this hardware.  Think about it.  Have you?
- Create an Ansible hosts inventory file
    ```
    python3 create_hosts_dot_yaml.py
    ```
- Take a look at your new hosts.yml file as a sanity check
    ```
    cat hosts.yml
    ```
- Check for connectivity and that Ansible works
    ```
    ansible -i hosts.yml -m ping all
    ```
- Install dependencies and whatnot on each host. (This is a good time to get up and stretch your legs.)
    ```
    ansible-playbook -i hosts.yml all.yml
    ```
- Each host is now running Cribl Stream with the Leader Node's Web UI available on port 19000.
- Log in with default credentials `admin:admin`
- Accept the license agreement
- Change your password
