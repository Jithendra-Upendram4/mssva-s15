# Nuclei Bootcamp — CH1-CH3 Quick-Start Guide

This README explains how to launch the vulnerable apps and run the Nuclei templates for the first three challenges.

---

## Prerequisites

1. **Python 3.8+** and **Flask** installed.
2. **Nuclei** CLI (install via `go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest` or download from [GitHub releases](https://github.com/projectdiscovery/nuclei/releases)).

---

## 1 — Start the Vulnerable Applications

Open **three** separate terminals and run:

```bash
# CH1 — Auth bypass (port 8001)
python apps/ch1-auth/app.py

# CH2 — File traversal (port 8002)
python apps/ch2-file/app.py

# CH3 — Weak API auth (port 8003)
python apps/ch3-api/app.py
```

Verify each server responds:

```bash
curl http://127.0.0.1:8001/login -X POST -H "Content-Type: application/json" -d "{\"username\":\"test\"}"
# Expected: {"token":"internal-access"}

curl "http://127.0.0.1:8002/download?file=../../../../etc/passwd"
# Expected: /etc/passwd contents (on Unix) or 404 (on Windows)

curl http://127.0.0.1:8003/api/orders/1 -H "Authorization: fake"
# Expected: {"item":"laptop","user":"elanthriyan"}
```

---

## 2 — Run Nuclei Templates

From the **nuclei-bootcamp** directory:

```bash
# Scan CH1
nuclei -t templates/ch1-auth-bypass.yaml -u http://127.0.0.1:8001

# Scan CH2
nuclei -t templates/ch2-file-traversal.yaml -u http://127.0.0.1:8002

# Scan CH3
nuclei -t templates/ch3-weak-api-auth.yaml -u http://127.0.0.1:8003
```

Or scan all three targets at once:

```bash
nuclei -t templates/ -l targets/local.txt
```

---

## 3 — Review Submissions

Pre-filled submission files are available in the `submissions/` folder:

- [ch1-submission.md](submissions/ch1-submission.md)
- [ch2-submission.md](submissions/ch2-submission.md)
- [ch3-submission.md](submissions/ch3-submission.md)

---

## Folder Structure After Setup

```
nuclei-bootcamp/
├── apps/
│   ├── ch1-auth/app.py
│   ├── ch2-file/app.py
│   └── ch3-api/app.py
├── templates/
│   ├── ch1-auth-bypass.yaml
│   ├── ch2-file-traversal.yaml
│   └── ch3-weak-api-auth.yaml
├── submissions/
│   ├── ch1-submission.md
│   ├── ch2-submission.md
│   └── ch3-submission.md
├── targets/
│   ├── local.txt
│   └── intranet.txt
└── README.md   <-- this file
```

Happy hunting! 🎯
