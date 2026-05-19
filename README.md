# Docker Log Analysis Lab

## Зорилго

Энэхүү лабораторийн ажлын зорилго нь Docker орчинд attacker, client, router-firewall, victim-server гэсэн 4 container ашиглан халдлагын дараах log analysis хийх юм.

## Ашигласан орчин

- Docker
- Docker Compose
- Ubuntu 22.04 container
- Apache2
- OpenSSH Server
- Nmap
- Curl
- Iptables

## Topology

```text
attacker  ----\
               router-firewall ---- victim-server
client    ----/
