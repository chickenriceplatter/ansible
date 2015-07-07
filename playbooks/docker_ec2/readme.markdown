Install docker in ec2 instance running on amazon linux
===

1. add your ec2 instance public DNS to your ~/.ssh/config file

  ```bash
  # container_dummy
  Host dummy_hostname
  Hostname ec2-100-100-100-100.compute-1.amazonaws.com
  User ec2-user
  IdentityFile ~/.ssh/your_key.pem
  ```

2. add the your host info to your host inventory

  ```bash
  [container_dummy]
  ec2-user@dummy_hostname
  ```

3. substitute your hostname inside the install_dependencies.yml

  ```
  ---
  - hosts: dummy_hostname
    remote_user: ec2-user
    sudo: true
    ...
  ```

4. run:

  ```bash
  $ ansible-playbook install_dependencies.yml
  ```
