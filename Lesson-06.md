# Final Lesson Overview
IF YOU ARE NOT USING JENKINS, THIS CAN ONLY BE DONE BY LINUX AND MAC USERS
>This playbook is going to expand using your knowledge of Terraform and  Ansible.
We are going to upload a Dockerfile and run the Tomcat image that builds jpetstore.
> The Dockerfile will be provided for you, but the Ansible playbook will be written by you.

##Tips:
1. Feel free to long into the instance and test your methods, remember that Ansible is just a fancy way of doing command line
2. If you are trying to use a Docker SDK, you are going about it the wrong way. Remember that we are installing a Docker Engine on an **instance**
3. Just because the build works, it doesn't mean it did what you want. To test that this works: check ```<instance ip>:8080``` in your browser
[JpetImage](!https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/main/imgs/jpetIMG.PNG)
 ---
## Creating a Dockerfile
1. For this project we need to install and run the following Docker file
```yaml
FROM tomcat:9

WORKDIR /tmp/jpet/
RUN apt-get update
RUN git clone https://github.com/mybatis/jpetstore-6.git


WORKDIR /tmp/jpet/jpetstore-6/
RUN ./mvnw clean package
RUN mv /tmp/jpet/jpetstore-6/target/jpetstore.war /usr/local/tomcat/webapps/ROOT.war

```
2. Using a file provisioner, add this file to the instance
3. Resources for Docker:
    + [Docker Documentation](https://docs.docker.com/)
    + [Steampunk's Docker Guide])(https://github.com/SteampunkFoundry/intro-to-docker)


### Provisioning with Ansible

Ansible Playbooks allow you to configure your instance with the applications needed just by building the pipeline. Using the Ansible Playbook, users can run shell scripts, install applications and set up their environment as needed.

The goal of this playbook is to install Docker, the Dockerfile is supposed to create an image that will build jpetstore using Tomcat-9. To test that this works: check 127.0.0.1:8080
1. Using the following code as a template fill in the following for your ansible playbook.
    + Below are links to documentation
    + Beware that spacing and indexing is critical for this portion

```yaml
- hosts: localhost

tasks:

- name: install dependency

- name: add GPG key

- name: add docker repository to apt

- name: install docker

- name: start docker

- name: restart docker

- name: change permissions to docker.sock

```
2. After attempting to do this yourself: try [this](https://medium.com/@pierangelo1982/install-docker-with-ansible-d078ad7b0a54)
3. Add the following code to your "remote-exec"
    ```terraform
     "docker build -qt <image name> <location of Dockerfile>",
     "docker run -dp 8080:8080 <image name"
     ```
4. Links
    + Ansible Playbook Documentation: https://docs.ansible.com/ansible/latest/user_guide/playbooks.html
    + Modules Documentation: https://docs.ansible.com/ansible/latest/user_guide/modules.html
        + Apt Module Documentation: https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_module.html
    + List of Modules: https://docs.ansible.com/ansible/2.8/modules/list_of_all_modules.html


Previous Lesson: [Lesson-05 Jenkins](./Lesson-05.md)
