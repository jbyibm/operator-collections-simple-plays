[![Build Status](https://travis.ibm.com/operator-collections/simple-plays.svg?token=zaKdnezhBLzXmTpcxLdZ&branch=main)](https://travis.ibm.com/operator-collections/simple-plays)

# Simple Plays

The `simple-plays` collection contains some example inventory configurations and simple playbooks that may be run standalone or via Kubernetes.

- [Simple Plays](#simple-plays)
  - [Development & Releases](#development--releases)
  - [Inventories & Variables](#inventories--variables)
  - [Playbooks](#playbooks)
    - [File](#file)
    - [DiscoverFiles](#discoverfiles)
    - [FileMessage](#filemessage)

## Development & Releases
This repository has built-in automation using Travis for builds and releases of new material. The automation process uses `release-it` and has a generic logic in `travis` to enable any user to fork this repo and it will automatically build a properly semantically-versioned archive and release it as a Github Release.

Reference the [`release-it` documentation](./release-it.md) for more information. 

WIP - switch to the public [oc-releaser](https://github.com/ivandov/oc-releaser)

## Inventories & Variables
The `inventories` folder creates a set of inventories to run against a local or remote system. Use `ansible-playbook -i` to specify an inventory.

Variables provided by Kubernetes and the [OperatorCollection specification](https://github.ibm.com/operator-collections/operator-collections/blob/master/spec.md#provided-variables) are defaulted in the `playbooks/vars` folder. These values may need to be modified for local development on various branches or forks.

The playbooks provided also use `vars_prompt` to allow local execution and specifying values directly.

## Playbooks
The playbooks and CustomResources provided by this OperatorCollection are listed below.

### File
The `file` playbook is a simple example of executing a playbook to create or delete a file on a target system.

- Create (Provision)
    ```
    ansible-playbook playbooks/file.yml -i inventories/local.yml
    ```
- Delete (Deprovision)
    ```
    ansible-playbook playbooks/file.yml -i inventories/local.yml --extra-vars "action=delete"

### DiscoverFiles
The `discover` playbook connects to a system and populates Kubernetes with File CustomResources

- Discover
    ```
    ansible-playbook playbooks/discover.yml -i inventories/local.yml
    ```

### FileMessage
The `day2` playbook connects to a system and populates Kubernetes with File CustomResources

- Write to a file
    ```
    ansible-playbook playbooks/day2.yml -i inventories/local.yml
    ```
