# CS3873 - Assignment 4

**Author:** Shahriar Kariman

**Due:** March 20th

## Question 1

The routers internal interface will be the first address of the home netwrok which is 192.168.1.1 and the other hosts can have the next 3 addresses:

- A $\rightarrow$ 192.168.1.2
- B $\rightarrow$ 192.168.1.2
- C $\rightarrow$ 192.168.1.3

And here is the NAT translation table.

| WAN Side (Public)                     | LAN Side (Private)                    |
|----------------------------------------|--------------------------------------|
| (24.34.136.211, **45000**) → (128.119.40.86, 22) | (192.168.1.2, **5000**) → (128.119.40.86, 22) |
| (24.34.136.211, **45001**) → (128.119.40.86, 22) | (192.168.1.2, **5001**) → (128.119.40.86, 22) |
| (24.34.136.211, **45002**) → (128.119.40.86, 22) | (192.168.1.3, **6000**) → (128.119.40.86, 22) |
| (24.34.136.211, **45003**) → (128.119.40.86, 22) | (192.168.1.3, **6001**) → (128.119.40.86, 22) |

## Question 2

| Network Prefix (Decimal)      |  Output Interface     |  Address Range                |
|-------------------------------|-----------------------|-------------------------------|
| 224.0.0.0/10                  |          0            | 224.0.0.0 ~ 224.63.255.255    |
| 224.64.0.0/16                 |          1            | 224.64.0.0 ~ 224.64.255.255   |
| 224.112.0.0/12                |          2            | 224.112.0.0 ~ 224.127.255.255 |
| 225.176.0.0/12                |          3            | 225.176.0.0 ~ 225.191.255.255 |
| 225.128.0.0/9                 |          4            | 225.128.0.0 ~ 225.255.255.255 |

- 225.180.250.10 $\rightarrow$ Output Interface 3
- 225.192.3.4 $\rightarrow$ Output Interface 4

## Question 3

**Subnet 2** has the last address of $176.31.251.255$ if I assume the first address is $176.31.251.192$ then the subnet would have $64$ addresses
which is more than the required $50$ addresses.

**Subnet 1** has the last address of $176.31.255.255$ if I assume the first address is $176.31.252.0$ then the subent would have $4 \times 256$ addresses
which is plenty more than the required $600$ addresses.

**Subnet 3** would get the other addresses before $176.31.251.192$ then it would have the first address of $176.31.250.192$ and the last address of
$176.31.251.191$ then it would have $256$ addresses which is more than the required $200$ addresses.

In the end the network prefix for the 3 subnets is:

$$
\begin{split}
  subnet \ 1 \rightarrow 176.31.252.0/22
  \\
  subnet \ 2 \rightarrow 176.31.251.192/26
  \\
  subnet \ 3 \rightarrow 172.31.250.192/23
\end{split}
$$

## Question 4

So it is possible to do the forwarding table like this:

|  Network Prefix (Decimal)    |  Output Interface |
|------------------------------|-------------------|
|   128.119.40.128/26          |   Subnet A        |
|   214.97.254.0/23            |   Router X        |
|   223.1.17.0/23              |   Router W        |

Which would work if we have the full cooporation of all the other routers but I do not think it is optimal.

## Question 5

Using the new information the minimum cost to subnet C is $\text{cost}_{U \rightarrow Y} + \text{cost}_{Y \rightarrow Z}$
which is equal to $35$.

And f you calcualte the optimal path to subnet B both the minimum cost path would also be through router Y. Which makes the new forwardin table:

| Network Prefix      | Output Interface |
|---------------------|------------------|
| 128.119.40.128/26   | Subnet A         |
| 214.97.254.0/23     | Router Y         |
| 223.1.17.0/23       | Router Y         |
