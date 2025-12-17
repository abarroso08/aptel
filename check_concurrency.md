

## 1.Check processes (sequential vs concurrent)

### Command

```bash
ps aux | grep 'program name'
```

### What to look for

* **1 line only** → **sequential server**
* **Several `program name` lines** → **concurrent server**

---

## 2. Check TCP connections to the server

### Command

```bash
netstat -tn | grep ':port'
```

### What to look for

* Many `ESTABLISHED` connections but only one responds → **sequential**
* Many `ESTABLISHED` connections responding → **concurrent**

(Optional, with process info)

```bash
netstat -tupan | grep ':port'
```

---

## 3. Check traffic behavior (tcpdump)

### Command

```bash
tcpdump -i any -nn tcp port 8888
```

### What to look for

* Replies go **one client at a time** → **sequential**
* Replies to **multiple clients interleaved** → **concurrent**

---

## 4. Easiest test (behavior)

1. Start two clients
2. Send data from both

* One blocks → **sequential**
* Both respond → **concurrent**

---

## One-line rule (remember this)

> **One server process and serialized replies → sequential.
> Multiple server processes and parallel replies → concurrent.**
