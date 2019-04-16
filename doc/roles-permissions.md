# Rockside Roles & Permissions
There are two roles in Rockside, **ADMIN** users, and **NON-ADMIN** users. Depending on the version of Rockside, **CLOUD** or **ENTERPRISE**, permissions on roles can vary. 
This document specifies the permissions for each context

## Roles
### ADMIN ON PREMISE
This is the person who installed Rockside. The system sets an ADMIN profile to the default user that is generated during the rockside installation,

### NON-ADMIN
todo

## Permissions

### node
A node is the gateway to Blockchain Network

### slave
A slave is the representation of an instance of Rockside-Slave. To simplify, this is the server where the node is installed 

### groupe


### consortium

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
