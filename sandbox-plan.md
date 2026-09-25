# Development Plan: Sage UIC Sandbox

**Concept:** Users of the Sage Grande Testbed need a place to start -- a small set of SGT nodes in a controlled laboratory environment.  The Sandbox will give students a place to try new ideas, test new software stacks, and explore sensors without disrupting nodes deployed in the field, such as at NEON or HPWREN.

## Components

The Sandbox needs several components that can be developed over time, each building on the previous component, and each component evolving over time. The list of components below is ordered, starting with the fundemental pieces, and then adding functionality and components with each step.

### 1) Thors in a Rack

There are currently 10 Thors online, and running the SGT software task.  The Sage Portal provides a simple interface to list the [UIC Sandbox Nodes](https://portal.sagecontinuum.org/nodes?query=UIC&show_all=true).


### 2) Sandbox Landing Page

While the portal page is helpful, it does not provide an end-to-end guide for requesting an account on the Sandbox and testing a simple Hello_World() AI program.  New SGT users need a simplified starting point that guides them through these steps (and probably others):

- Simple overview of the Sandbox -- what is it?  How can it be used?  What is the equipment attached?
- Request a Sage Grande *account* ([See Getting Started Guide](https://sagecontinuum.org/docs/getting-started))
- Create and upload credentials (SSH credentials)
- Request access to the "*UIC Sandbox*" *resource*.
- SSH connect to a Sandbox Node, explore
- Download and test with a simple Hello_World example
- Access a camera 

#### Additional Notes

- Where do Sandbox users ask questions?  Slack channel?
- In this first version, how do they find the list of nodes to use?
- How should they select a node?  (randomly?)
- The Sandbox landing page should be in a Sage [github repo](https://github.com/sagecontinuum).

### 3) Cameras and Sensors

Nodes within the sandbox can ***share*** cameras and sensors.  This is a very unique configuration -- only available in the Sandbox.  For Sage nodes deployed in production, such as within NEON or HPWREN, a camera, microphone, or other sensor is mapped to one and only one Sage node.  However, for the Sandbox, each node in the Sandbox can access any sensor on the local EVL Sandbox network.  To accomplish this, requires several pieces:

- Every network attached device (Camera, microphone, etc.) must be on the Sage Wireguard VPN (such as the Beryl routers)
- Cameras should be configured in unique ways, without the possibility to see humans (students), but rather interesting objects, an LCD screen, a fishtank, etc.
- When possible, the *admin* password for a camera should be secret, and the *user* access password will be shared with Sandbox users
- The Sandbox Landing Page (web page), should enumerate all the sensors and instructions for using them

#### Additional Notes
- Common accessible directory with large number of pre-fetched camera/mic resources.


### 4) Network-attached, Shared Home Directory

It would be a little more convienient for users of the Sandbox if they had a persistant, network mounted home directory.  There are standard ways to provide a Network File System (NFS) to a set of nodes in a cluster.  Key pieces:

- A lightweight Linux server (sandbox-homes) with sufficient disk - maybe 1TB.
- The server should be integrated with the Sage configuration management system via Ansible so user credentials are automatically updated and managed
- The Sage nodes is the Sandbox will need a special Ansible configuration that uses the NSF server for home directories.

### 5) Simple SSH Load Balancing

At this point, a user must choose which of the Sandbox nodes to use.  If the Shared Home Directory is configured, they will have access to their files, no matter which node they log into, but it would ideal if a user could just land on the least busy node.  Often, this is called SSH Load Balancing across a pool of login nodes, and it would be convenient to have dynamic, load-aware balancing.

There are several packages that provide the needed capability, and they can be explored.



