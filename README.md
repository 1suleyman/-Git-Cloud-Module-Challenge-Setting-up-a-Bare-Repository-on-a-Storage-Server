# 🌐 Git Cloud Module Challenge: Setting up a Bare Repository on a Storage Server

In this challenge, I learned how to **SSH into a remote server**, install Git, and create a **bare Git repository** on a storage server. The journey included some troubleshooting, learning about directory paths, and understanding system-wide permissions. This README generalizes the experience so it can be applied to any user and server.

---

## 📋 Challenge Overview

**Goal:**

* SSH into a remote storage server
* Install Git if not already available
* Create a **bare Git repository** at `/opt/official.git`

**Learning Outcomes:**

* Using `ssh` to access remote servers
* Installing packages with `yum` on a Linux server
* Understanding directory paths and permissions
* Initializing a bare Git repository with correct permissions

---

## 🛠 Step-by-Step Journey

### Step 1: SSH into the Storage Server

**Instructions I followed:**

1. Open a terminal on my local machine.
2. Run:

```bash
ssh username@<server-ip>
```

* `username` is the provided user on the server (kept generic)
* `<server-ip>` is the server IP address (kept generic)

3. Accept the host key if prompted (`yes`).
4. Enter the password provided for the user.

💡 **Tip:** SSH allows secure remote access to servers. You can be in any directory locally; your home directory on the server is the starting point.

---

### Step 2: Install Git on the Server

Since Git wasn’t pre-installed, I installed it using `yum`:

```bash
sudo yum install git
```

* Entered the user password when prompted.
* Confirmed installation by typing:

```bash
git --version
```

💡 **Tip:** Installing with `sudo` ensures Git is available system-wide. You don’t need to install it in `/opt` or your home directory — the installation location for Git binaries is system-managed (`/usr/bin`).

---

### Step 3: Navigate to `/opt` Directory

To prepare for the bare repository:

```bash
cd /opt
```

* Verified the directory exists:

```bash
ls
```

💡 **Tip:** `/opt` is a standard directory for optional software or shared resources. It requires `sudo` for write permissions.

---

### Step 4: Create the Bare Git Repository

**Incorrect first attempt:**

* Initially created the repository inside the user’s home directory by mistake (`/home/natasha/opt`)
* Initialized with:

```bash
sudo git init --bare official.git
```

* Result: repository created in the wrong location, challenge failed.

**Correct approach:**

* Ensure you are in `/opt` and run:

```bash
sudo mkdir -p /opt/official.git   # create directory if it doesn’t exist
sudo git init --bare /opt/official.git
```

* This ensures:

  1. The directory `/opt/official.git` exists
  2. The bare repository is created in the **absolute path**
  3. Permissions are correct via `sudo`

✅ **Checkpoint:** Bare repository successfully created at `/opt/official.git`

---

### Step 5: Verify Repository Creation

* Checked that the bare repository exists:

```bash
ls -l /opt/official.git
```

* Confirmed repository structure (`branches/`, `hooks/`, `objects/`, `refs/`).

💡 **Tip:** Bare repositories don’t have a working directory; they’re meant for remote pushes and pulls.

---

### Step 6: Lessons Learned

* **Directory paths matter:** Absolute paths ensure the repository is created in the correct location.
* **Sudo permissions:** Required to write in `/opt` or other system directories.
* **Git init --bare:** Initializes a repository without a working directory; perfect for remote server repositories.
* **SSH basics:** Always start in the user’s home directory, but be aware of where you want files created.

---

### Step 7: Reflection

* My first attempt failed because I assumed `mkdir opt` in my home directory would create `/opt`.
* Gemini’s AI advice clarified that using the **absolute path** with `sudo` is crucial for system-wide repositories.
* By the second attempt, I successfully created `/opt/official.git`, completing the challenge.

---

## ✅ Summary Table

| Step                    | Status | Key Notes                                |
| ----------------------- | ------ | ---------------------------------------- |
| SSH into storage server | ✅      | Used generic username and IP             |
| Install Git via yum     | ✅      | System-wide installation                 |
| Navigate to `/opt`      | ✅      | Verified directory exists                |
| Create bare repository  | ✅      | `sudo git init --bare /opt/official.git` |
| Verify repository       | ✅      | Confirmed repository structure           |

---

## 💡 Notes / Tips

* Always check your current directory with `pwd` before creating system resources.
* Use `sudo` when creating directories or repositories in protected paths.
* Bare repositories are ideal for remote central repositories — they do not have a working tree.
* Keep passwords secure and never hardcode them in scripts.

---

## 📸 Screenshots / Verification

* SSH into server
* Yum installation of Git
* `/opt` directory listing
* Bare repository structure

---

## ✅ References

* [Git Documentation: git init](https://git-scm.com/docs/git-init)
* [SSH Basics](https://www.ssh.com/ssh/)
* [Linux File Permissions and Sudo](https://linuxize.com/post/linux-sudo-command/)

