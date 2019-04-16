# Rockside Roles & Permissions
There are two roles in Rockside, **ADMIN** users, and **NON-ADMIN** users. Depending on the version of Rockside, **CLOUD** or **ENTERPRISE**, permissions on roles can vary. 
This document specifies the permissions for each context.


## Roles
### ADMIN (ON PREMISE)
This is the person who installed Rockside. The system sets an ADMIN profile to the default user that is generated during the rockside installation.

### ADMIN (CLOUD)
This is Rockside Team.

### NON-ADMIN (ON PREMISE & CLOUD)
All users who register at Rockside after installation

## Permissions

### node
A node is the gateway to Blockchain Network (ledger copy)

### slave
A slave is the representation of an instance of Rockside-Slave. To simplify, this is the server where the node is installed. A Slave is not linked to a group. It is global to the instance and visible / usable by all groups. 

### groupe
A groupe is a context. In this context we find people, consortiums, and nodes.

### consortium
A consortium represents a set of validating nodes on the same network.A consortium represents a set of validating nodes on the same network. These nodes can be linked to slaves or not (external)

### Alert Mail
todo

### Address Book
todo


## Relationship
- A user is in one or several groups
- A node is in one and only one group
- A consortium is in one and only one group
- A node is linked or not to a consortium
- A node is in on one and only one Slave


## Permissions of ADMIN vs NON-ADMIN for ON PREMISE & CLOUD versions

| Feature                               | ADMIN     | USER ON PREMISE | USER CLOUD |
| -------------                         |:---------:|:---------:|:---------:|
| Create groupe                         |✅         |✅        |✅        |
| Add user to groupe                    |✅         |✅        |✅        |
| Read applications users               |✅         |          |           |
| Create / Update user                  |✅         |          |           |
| Give Admin Role to User               |✅         |          |           |
| Enable / Disable Registration         |✅         |          |           |
| Register slave                        |✅         |          |           |
| Read slave infos                      |✅         |          |           |
| Create node                           |✅         |          |           |
| Stop/Start Node Sync                  |✅         |          |           |
| See TX going through Node RPC         |✅         |✅        |✅         |
| Use node RPC                          |✅         |✅        |✅        |
| Create / Join consortium              |✅         |✅        |only 1  |
| Choose Slave for consortium member    |✅         |✅        |          |
| Add member to consortium              |✅         |✅        |max 3   |
| Create Address Book                   |✅         |✅        |✅        |
| Notification setup                    |✅         |          |           |
| Notification activation by node       |✅         |✅        |            |





