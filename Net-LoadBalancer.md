# Load Balancer

The OCI Load Balancing Service - distribute the load of incoming requests among 2 or more servers.

## Basics

What the OCI Load Balancing Service does

- Service Discovery: What backends are available in the system? How should the load balancer talk to them?
- Health Check: What backends are currently healthy and available to accept requests? 
- Load Balancing: What algorithm should be used to balance individual requests across the healthy backends?

## Benefits
- Fault Tolerance
- Scaling for load
- Provides naming resolution so that back end servers do not need public IP
- A single LB can handle both TCP (OSI Layer 4)  and HTTP traffic (OSI Layer 7)

## Configuration Overview

Can be Public or Private

- Public requires 2 Subnets in 2 Availability Domains
  - Typically used to balance incoming traffic from the internet
- Private requires 1 Subnet in 1 Availability Domain
  - Must be in a single AD as it is a private address and subnets currently cannot span AD
  - Typically used to balance traffic between internal components
    - front end to app tier
    - app tier to db tier

Note: Load Balancer subnets are subnets that are dedicated to LB use

Supports:

- SSL
- TCP
- HTTP 1, 1.1, 2
- Websocket

Can be up to 16 listeners on different ports

## Load Balancing Policies

- Round Robin - just like it says
- IP Hash - incoming address hashed to determine which server to use
- Least Connection - sends traffic to the server with least connections

Policy decisions are dynamic, that is the type of traffic influences the policy used

- A TCP load balancer considers policy and weight criteria
- An HTTP load balancer w/ cookie-based session persistence forwards requests using cookie's session info
For non-sticky HTTP requests, the load balancer applies policy and weight criteria

Round Robin is the policy most commonly used.

## Health Check

The LB performs health checks every 3 minutes (shortest time available) to determine status of servers

- ok
- warning
- critical
- unknown

The backend components can be configured into 'Backend Sets'

There relationship of LB-Listener:BackendSet is 1:1

As there are 16 ports available, there can be 16 LB Listeners, and 16 Backup Sets



