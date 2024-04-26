# NFS

## **Introduction**

> * Network File System (NFS) is a network file system developed by Sun Microsystems and has the same purpose as SMB.
> * Its purpose is to access file systems over a network as if they were local. However, it uses an entirely different protocol.
> * NFS' default port is 2049 TCP

***

## **Basic Enumeration & Interaction**

> * When footprinting NFS, the TCP ports 111 and 2049 are essential.
> * We can also get information about the NFS service and the host via RPC (2049)

| Command                                             | Description                                               |
| --------------------------------------------------- | --------------------------------------------------------- |
| Use nmap scripts to find connected NFS shares names | sudo nmap --script nfs\* 10.129.14.128 -sV -p111,2049     |
| Show Available shares on target IP                  | showmount -e 10.129.14.128                                |
| Mount (locally) an available share                  | sudo mount -t nfs 10.129.14.128:/ ./target-NFS/ -o nolock |
| Unmount a previously mounted share                  | sudo umount ./target-NFS                                  |