# GitHub Authentication Journey: HTTP → SSH

This document chronicles the challenges and solutions encountered while pushing the Pi-hole + XB project to GitHub from a Raspberry Pi.  

---

## 1. Initial Attempt: HTTPS + GitHub Account Password
- Tried to push using HTTPS:
  ```bash
  git push -u origin main


Error received:

fatal: Authentication failed


Cause: GitHub no longer allows account passwords for Git operations over HTTPS.

2. Attempt: Personal Access Token (PAT)

Generated a token from GitHub (Settings → Developer settings → Personal access tokens → Tokens (classic))

Attempted to push using:

Username: GitHub username

Password: PAT

Issues encountered:

403 errors

“Permission denied”

Problems with copying the token correctly

Old cached credentials interfering

Lesson Learned: HTTPS + PAT can be tricky, especially on Linux/Pi with cached credentials.

3. Remote URL Conflicts

Tried git remote add origin ... multiple times

Errors: fatal: remote origin already exists

Fixed by either:

git remote set-url origin https://github.com/YOUR_USERNAME/pi-hole-xb-project.git


or

git remote remove origin
git remote add origin https://github.com/YOUR_USERNAME/pi-hole-xb-project.git

4. Solution: SSH Authentication
Step 1: Generate SSH Key
ssh-keygen -t ed25519 -C "your_email@example.com"


Press Enter to accept defaults

Leave passphrase empty (optional)

Step 2: Copy the public key
cat ~/.ssh/id_ed25519.pub


Copy the full output

Step 3: Add SSH key to GitHub

GitHub → Settings → SSH and GPG keys → New SSH key

Paste key and save

Step 4: Update Git remote to SSH
git remote set-url origin git@github.com:YOUR_USERNAME/pi-hole-xb-project.git
git remote -v

Step 5: Test SSH connection
ssh -T git@github.com


Should see:

Hi YOUR_USERNAME! You've successfully authenticated, but GitHub does not provide shell access.

Step 6: Push to GitHub
git add .
git commit -m "Initial commit via SSH"
git push -u origin main


No username or password needed

5. Lessons Learned

HTTPS + PAT works but is prone to copy/paste and cached credential issues.

SSH is more reliable on Raspberry Pi / Linux systems.

Always verify remote URLs (git remote -v) before pushing.

Documenting errors and solutions creates a valuable reference for future projects.

This journey adds credibility to the project: it shows problem-solving, persistence, and Git/GitHub mastery.

Conclusion

The SSH workflow became the final, stable solution for pushing projects from the Raspberry Pi. Documenting this process enhances the repo’s value and serves as a guide for anyone facing similar GitHub authentication challenges.


---

