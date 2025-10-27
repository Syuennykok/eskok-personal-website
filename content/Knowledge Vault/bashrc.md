---
created: 2025-10-27T15:13
updated: 2025-10-27T15:14
title: How to set Environment Variables in bashrc
tags:
  - SoftwareHacks
---
# 🛠️ Setting Environment Variables in `.bashrc` on WSL Ubuntu

This tutorial shows how to add custom environment variables (e.g., for OpenASIP or local libraries) to your `.bashrc` file in WSL Ubuntu.

---

## 📍 Step 1: Open `.bashrc` for Editing

Open your terminal and run:

```bash
nano ~/.bashrc
```

This opens the `.bashrc` file in a simple text editor.

---

## ✏️ Step 2: Add Your Environment Variables

Scroll to the **bottom** of the file and add the following lines:

```bash
# === Custom environment variables for OpenASIP or local libraries ===
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HOME/local/lib
export PATH=$HOME/local/bin:$PATH
export LDFLAGS=-L$HOME/local/lib
```

You can modify the paths if your libraries or binaries are in different locations.

---

## 💾 Step 3: Save and Exit

In the `nano` editor:

- Press `Ctrl + O`, then `Enter` to save the file.
- Press `Ctrl + X` to exit.

---

## 🔄 Step 4: Apply the Changes

To apply the new environment variables without restarting your terminal, run:

```bash
source ~/.bashrc
```

Now the new settings will be active in your current session.

---

## ✅ Notes

- `LD_LIBRARY_PATH` is used by the linker to find dynamic libraries at runtime.
- `PATH` allows you to run binaries in `$HOME/local/bin` from anywhere.
- `LDFLAGS` is passed to compilers (like `gcc`) during the linking step.

---

## 🧠 Tip

To check if your changes worked:

```bash
echo $LD_LIBRARY_PATH
echo $PATH
echo $LDFLAGS
```

---

## 📎 Related

If you're working with OpenASIP or custom toolchains, these settings are often required when installing libraries like Boost, LLVM, or custom simulators in `$HOME/local`.