text
# 🔒 Linux File Permission Hardening Project  
*Cybersecurity Portfolio | 28th June 2025*

---

## 🏢 Scenario

As a security professional for a research organization, I audited and modified file system permissions to enforce least privilege access. The goal was to align permissions with authorization policies by removing excessive access while ensuring research team collaboration.

---

## 🐧 Initial File System State

-rw-rw-rw- 1 researcher2 research_team project_k.txt
-rw-r----- 1 researcher2 research_team project_m.txt
-rw-rw-r-- 1 researcher2 research_team project_r.txt
-rw-rw-r-- 1 researcher2 research_team project_t.txt
-rw--w---- 1 researcher2 research_team .project_x.txt
drwx--x--- 2 researcher2 research_team drafts

text

### 🔍 Permission Analysis
| File/Directory       | Issues Identified                          |
|----------------------|--------------------------------------------|
| `project_k.txt`      | World read/write (rw-) - Excessive access |
| `project_r.txt`      | Group write (w) - Unnecessary privilege   |
| `project_t.txt`      | Group write (w) - Unnecessary privilege   |
| `.project_x.txt`     | Group write (w) - Hidden file risk        |
| `drafts` directory   | Group execute (x) only - No read access   |

---

## 🛠️ Remediation Commands

### 1. Regular File Hardening
Remove world access from project_k.txt
chmod o-rwx project_k.txt

Remove group write + world access from project_r/t.txt
chmod g-w,o-rwx project_r.txt project_t.txt

Allow group read (remove write) from project_m.txt
chmod g+r-w project_m.txt

text

### 2. Hidden File Securing
Adjust .project_x.txt to secure standards
chmod g+r-w,o-rwx .project_x.txt

text

### 3. Directory Permission Fix
Enable secure collaboration in drafts
chmod g+rx drafts

text

---

## 🔐 Final Permission State
-rw-rw---- 1 researcher2 research_team project_k.txt
-rw-r----- 1 researcher2 research_team project_m.txt
-rw-r----- 1 researcher2 research_team project_r.txt
-rw-r----- 1 researcher2 research_team project_t.txt
-rw-r----- 1 researcher2 research_team .project_x.txt
drwxr-x--- 2 researcher2 research_team drafts

text

---

## 🛡️ Security Improvements

| Principle              | Implementation                             |
|------------------------|--------------------------------------------|
| **Least Privilege**    | Removed world access from all files        |
| **Need-to-Know**       | Group write privileges eliminated          |
| **Defense-in-Depth**   | Hidden files secured (.project_x.txt)     |
| **Secure Defaults**    | Directories allow read+execute (no write) |

---

## 📝 Summary

- **World access eliminated:** No files/directories accessible to unauthorized users
- **Group privileges restricted:** Read-only access to project files
- **Hidden files secured:** `.project_x.txt` now follows standard protocols
- **Directory safety:** `drafts` allows traversal without modification rights

---

## 💡 Lessons Learned

> "This project demonstrated how granular permission control acts as a critical defense layer. By auditing and modifying Linux file permissions, we transformed an overly permissive research environment into a least-privilege model without disrupting legitimate collaboration."  
> *— Security Team Reflection*

---

**Technical Skills Demonstrated:**  
- Linux file permission management (`chmod`)  
- Permission string interpretation (rwx)  
- Principle of least privilege enforcement  
- Hidden file security hardening  
- Directory permission best practices  
