# Ansible Role: Java

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-java.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-java)

Installs Java for RedHat/CentOS and Debian/Ubuntu linux servers.

## Requirements (WIP)

This scripts a multi node cluster for hadoop

## How to run the playbook

1. Clone this repository
2. vagrant up

## Dependencies


## Example Playbook (using default package, usually OpenJDK 7)

    - hosts: servers
      roles:
        - geerlingguy.java

## Example Playbook (install OpenJDK 8)

For RHEL / CentOS:

    - hosts: server
      roles:
        - role: geerlingguy.java
          when: "ansible_os_family == 'RedHat'"
          java_packages:
            - java-1.8.0-openjdk

For Ubuntu < 16.04:

    - hosts: server
      tasks:
        - name: installing repo for Java 8 in Ubuntu
  	      apt_repository: repo='ppa:openjdk-r/ppa'
    
    - hosts: server
      roles:
        - role: geerlingguy.java
          when: "ansible_os_family == 'Debian'"
          java_packages:
            - openjdk-8-jdk

## License

MIT / BSD

