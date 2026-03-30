# Day 14 – Networking Fundamentals & Hands-on Checks

## Quick Concepts

### OSI vs TCP/IP
- OSI (7 layers) is a conceptual model; TCP/IP (4 layers) is what real networks actually use.
- TCP/IP merges OSI layers (e.g., OSI Session + Presentation → Application).

### Where things sit
- IP → Internet layer  
- TCP/UDP → Transport layer  
- HTTP/HTTPS, DNS → Application layer  

### Real Example
- `curl https://example.com` = HTTP (Application) → TCP (Transport) → IP (Internet)

---

## Target Host
Using: `google.com`

---

## Hands-on Checklist

### Identity
```bash
hostname -I
````

**Output:**

```
192.168.1.105
```

* Observation: Private LAN IP assigned by router (DHCP).

---

### Reachability

```bash
ping -c 4 google.com
```

**Output (trimmed):**

```
64 bytes from 142.250.192.14: icmp_seq=1 ttl=116 time=28.4 ms
64 bytes from 142.250.192.14: icmp_seq=2 ttl=116 time=26.9 ms
```

* Observation: ~25–30 ms latency, 0% packet loss → stable connectivity.

---

### Path

```bash
traceroute google.com
```

**Output (trimmed):**

```
1  192.168.1.1       1.2 ms
2  10.0.0.1          5.4 ms
3  * * *
4  72.14.xxx.xxx     22.1 ms
```

* Observation: Some hops don’t respond (*), which is normal (ICMP blocked).

---

### Ports

```bash
ss -tulpn
```

**Output (trimmed):**

```
tcp   LISTEN  0  128  0.0.0.0:22     0.0.0.0:*    users:(("sshd",pid=712))
tcp   LISTEN  0  128  127.0.0.1:631  0.0.0.0:*    users:(("cupsd",pid=654))
```

* Observation: SSH running on port 22; CUPS service on 631.

---

### Name Resolution

```bash
dig google.com +short
```

**Output:**

```
142.250.192.14
142.250.192.46
```

* Observation: Multiple IPs → DNS load balancing.

---

### HTTP Check

```bash
curl -I https://google.com
```

**Output (trimmed):**

```
HTTP/2 200 
content-type: text/html; charset=UTF-8
```

* Observation: HTTP 200 OK → service reachable and healthy.

---

### Connections Snapshot

```bash
netstat -an | head
```

**Output (trimmed):**

```
tcp  0  0 127.0.0.1:631   0.0.0.0:*    LISTEN
tcp  0  0 192.168.1.105:22 192.168.1.10:53422 ESTABLISHED
```

* Observation: Both LISTEN and ESTABLISHED connections present → normal activity.

---

## Mini Task: Port Probe & Interpret

### Selected Port

* Port: 22 (SSH)

### Test

```bash
nc -zv localhost 22
```

**Output:**

```
Connection to localhost 22 port [tcp/ssh] succeeded!
```

* Result: Port is reachable.

### If Not Reachable

* Check:

  * `systemctl status ssh`
  * `ufw status` / `iptables -L`
  * Service binding (`ss -tulpn`)

---

## Reflection

### Fastest Signal When Broken

* `curl -I` → fastest way to confirm service availability.
* `ping` → quick network connectivity check.

---

### Layer Troubleshooting

* DNS failure → Application layer (DNS) + Internet layer (IP routing)
* HTTP 500 → Application layer (server-side issue)

---

### Follow-up Checks in Real Incident

* Check service logs (`journalctl -u <service>`)
* Verify firewall/security group rules

---
