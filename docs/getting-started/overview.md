# Overview

This repository provides a structured guide for setting up a complete development environment on Windows **without administrator privileges**.

It is designed for environments where admin access is restricted, such as:
- corporate laptops
- school or university machines
- shared systems

---

## 🎯 What This Covers

You will learn how to install and configure:

- Code editors (VSCode, Notepad++)
- Version control (Git)
- Programming runtimes (Node.js, Python, .NET)
- Databases (PostgreSQL, MySQL, SQLite)
- Terminal and shell enhancements
- System configuration (PATH, registry, VSCode settings)

All tools are installed using:
- Portable versions, or
- User-space (non-admin) installations

---

## ⚙️ Installation Strategy

Instead of using system-wide installers, this guide follows a consistent approach:

1. Download portable or zip distributions
2. Extract to a user-writable directory (e.g. `C:\sw\`)
3. Manually configure environment variables
4. Verify installation via command line

This avoids:
- admin prompts
- system-level changes
- dependency on IT policies

---

## 📁 Recommended Directory Structure

All tools are installed under a single root folder:
