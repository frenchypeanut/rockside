# Rockside Roles & Permissions
There are two roles in Rockside, **ADMIN** users, and **NON-ADMIN** users. Depending on the version of Rockside, **CLOUD** or **ENTERPRISE**, permissions on roles can vary. 
This document specifies the permissions for each context

## Roles
### ADMIN user ON PREMISE Version
This is the person who installed Rockside. The system sets an ADMIN profile to the default user that is generated during the rockside installation.

### ADMIN user CLOUD Version
This is Rockside Team.

### NON-ADMIN (ON PREMISE & CLOUD Version)
All users who register at Rockside after installation

## Permissions

### node
A node is the gateway to Blockchain Network (ledger copy)

### slave
A slave is the representation of an instance of Rockside-Slave. To simplify, this is the server where the node is installed 

### groupe
A groupe is a context. In this context we find people, consortiums, and nodes.

### consortium
A consortium represents a set of validating nodes on the same network.A consortium represents a set of validating nodes on the same network. These nodes can be linked to slaves or not (external)

## Relationship
- A user is in one or several groups
- A node is in one and only one group
- A consortium is in one and only one group
- A node is linked or not to a consortium
- A node is in on one and only one Slave


## Permissions of Admin On Premise

| Feature           | read      | Write     |
| -------------     |:---------:|:---------:|
| groupe            |[x]        |[x]        |
| slave             |[x]        |[x]        |
| node              |[x]        |[x]        |
| consortium        |[x]        |[x]        |
