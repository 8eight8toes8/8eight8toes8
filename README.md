# 👋 Hi, I'm John Henderson (Jay)

## 🔐 Cybersecurity Intern | Technical Writer | CompTIA Certified

**Location:** Branson, Missouri | **Organization:** MCCoE (Mid-Continent Cybersecurity Operations and Engineering)

---

### 🚀 Current Focus

- 🛡️ Developing **[Sec-PBQ](https://github.com/8eight8toes8/Sec-PBQ)** - Interactive Security+ (SY0-701) PBQ training platform for CompTIA certification prep
- 📊 Building SOC operations documentation and SIEM integration guides
- 🌐 Creating cybersecurity educational content and technical write-ups
- 📚 Actively pursuing CompTIA Network+ and A+ recertification

---

### 💼 Recent Accomplishments (December 2025)

 - ✅ **SANS Academy Acceptance (Winter 2025)** - Selected for highly competitive cybersecurity scholarship program
- ✅ **Sec-PBQ Platform Refactoring** - Promoted new feature branch to production, implemented professional documentation
- ✅ **Repository Management** - Organized and archived legacy projects with clear version control strategies
- ✅ **Technical Documentation** - Created comprehensive READMEs with proper descriptions, topics, and professional structure
- ✅ **GitHub Workflow Optimization** - Established best practices for branch management and repository organization

---

### 🛠️ Technical Skills

**Security & Networking**
- Network Scanning: Nmap, Wireshark
- SIEM: Splunk, QRadar, Sentinel
- Threat Intelligence: OTX, X-Force
- Firewall Configuration: OpenWrt, DMZ architecture

**Development & Scripting**
- Languages: JavaScript/TypeScript, Python, Bash, PowerShell
- Frameworks: React, Node.js, Vite
- Tools: Docker, Git, VS Code, GitHub

**Operating Systems**
- Kali Linux, Parrot OS
- Windows 11 (WSL)
- Linux system administration

**Tools & Platforms**
- Burp Suite, Hashcat, Suricata
- Google AI Studio, Cloud Run
- Technical documentation and reporting

---

### 📂 Featured Projects

#### 🎯 [Sec-PBQ](https://github.com/8eight8toes8/Sec-PBQ) (Private)
**Interactive Security+ (SY0-701) PBQ training platform**
- Hands-on labs for CompTIA certification prep
- Built with React + TypeScript
- Professional documentation and modular architecture

#### 🔍 [cybersecurity-writeups](https://github.com/8eight8toes8/cybersecurity-writeups) (Public)
**Technical documentation for cybersecurity tools, penetration testing methodologies, and SOC operations**
- Security tool tutorials
- SOC operation guides
- Network analysis documentation

#### 🌐 [home-network-ids](https://github.com/8eight8toes8/home-network-ids) (Public)
**Home Network Intrusion Detection System (IDS) setup documentation**
- OpenWrt configuration
- Suricata IDS deployment on WSL2
- Network monitoring best practices

#### 🎖️ [Google-Studio-Code-First-Build](https://github.com/8eight8toes8/Google-Studio-Code-First-Build) (Private)
**🏆 First Build - Original Sec-PBQ app preserved as a milestone trophy**

---

### 📜 Certifications

- 🎓 **CompTIA Network+** (Active)
- 🎓 **CompTIA A+** (Active)
- 📋 **CompTIA Security+** (Expired 05/25 - Recertifying)
- 🎯 **HackTheBox Academy** - Linux Fundamentals, OS Fundamentals, Information Security Foundations, SOC Analyst Prerequisites
- 🏅 **SANS Aptitude Assessment** - 4/5 Stars

---

### 📫 How to Reach Me

- 📧 Email: [jhenderson@mccoe.org](mailto:jhenderson@mccoe.org)
- 💼 LinkedIn: [Connect with me](#) <!-- Add your LinkedIn URL -->
- 🌐 GitHub: [@8eight8toes8](https://github.com/8eight8toes8)
- 📱 Phone: 417-901-3198

---

### 📊 GitHub Stats

![GitHub stats](https://github-readme-stats.vercel.app/api?username=8eight8toes8&show_icons=true&theme=tokyonight)

---

### 💡 Fun Facts

- 🎮 Gaming enthusiast (Kingdom Come: Deliverance 2, Europa Universalis V, Subnautica, XCOM2)
- 🚁 Drone flying hobbyist
- 🐕 Service dog trainer
- 🍄 Mycology enthusiast
- 🥊 Boxing analysis fan

---

📄 **[Download My Resume](https://github.com/8eight8toes8/8eight8toes8/blob/main/John_Henderson_Resume.md)**

---

*Self-taught cybersecurity professional passionate about SOC operations, security automation, and helping others learn cybersecurity through hands-on training platforms.*

---

### ⚙️ Git Workflow Guide

**Disciplined Solo Development Pattern** - Multi-device safety workflow for test-to-production promotion

#### 🎯 Use Case
Syncing code between test repository (`Sec-PBQ-New_Features`) and production repository (`Sec-PBQ`) across 3 devices (Desktop, Laptop, Chromebook) without breaking production.

#### 📋 Phase 1: Create Production Backup

```bash
cd ~/path/to/Sec-PBQ
git checkout main
git pull origin main
git checkout -b main-release-backup
git push -u origin main-release-backup
```

**Safety**: Creates frozen snapshot at `main-release-backup` for rollback if needed.

#### 📋 Phase 2: Link Test Repo to Production

```bash
cd ~/path/to/Sec-PBQ-New_Features
git remote add release git@github.com:8eight8toes8/Sec-PBQ.git
git remote -v  # verify both 'origin' and 'release' remotes
```

#### 📋 Phase 3: Create Sync Branch in Test Repo

```bash
git checkout main
git pull origin main
git checkout -b pbq-sync-v2
git add .
git commit -m "Sync PBQ features and fixes to production"
npm start  # test locally before syncing
```

#### 📋 Phase 4: Push Sync Branch to Production

```bash
git push release pbq-sync-v2
```

**Result**: Production repo now has `pbq-sync-v2` branch with new code.

#### 📋 Phase 5: Merge into Production Main

```bash
cd ~/path/to/Sec-PBQ
git fetch origin
git checkout main
git pull origin main
git checkout pbq-sync-v2  # optional: verify/test
git checkout main
git merge pbq-sync-v2
git push origin main
```

#### 📋 Phase 6: Cleanup

```bash
git branch -d pbq-sync-v2
git push origin --delete pbq-sync-v2
```

#### ⚡ Why This Works for Multi-Device Setup

- **Desktop**: Creates and tests sync branch
- **Chromebook**: Runs `git pull origin main` → gets tested code
- **Laptop**: Runs `git pull origin main` → gets tested code
- **Backup**: `main-release-backup` branch allows instant rollback

#### 🚨 Rollback (If Needed)

```bash
git checkout main
git reset --hard origin/main-release-backup
git push --force origin main  # use with caution
```

---
