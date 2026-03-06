# Git & Unity Daily Workflow Practices

Follow this routine **every single time** you work on the project to keep everything stable.

## Core Rule #1: Develop on PC, Test on Robot
- Always develop and edit code on your PC. The robot cannot access the internet, so transfer files to the robot only for testing.
- If you make changes directly on the robot, transfer them back to your PC, then commit and push from there.
- Why? This ensures all changes are tracked in Git on the PC, prevents desyncs, and maintains a clean history on GitHub.

## Step-by-Step Routine

### Part A. Pure Programming

1. **Open Visual Studio Code**
   - Open VS Code -> choose "open folder" -> choose the folder containing the repository
   
2. **Git pull (always do so before working)**
   - Open your terminal in the project folder (eg. `Team-A1`).
   - Pull the latest changes from the remote:
     ```bash
     git pull origin your-branch
     ```
   - If conflicts appear → resolve them carefully (see Troubleshooting below).
   - (Optional: Run git status to confirm clean working tree.)

3. **Go on to develop**
   - Save frequently or enable auto-save in VS Code

4. **Stage, commit & push**
   - Stage all changes:
     ```bash
     git add .
     ```
   - Commit with a clear message:
     ```bash
     git commit -m "your commit message"
     ```
      - Good commit messages: what + why (short & descriptive)
   - Push to remote:
     ```bash
     git push origin your-branch
     ```
      - If push rejected (non-fast-forward), it means someone else pushed meanwhile. Git pull again, resolve, then push.
    
### Part B. Testing on Robot

1. **Start session – on PC**
   - Pull from github (follow the steps in A1)
     
2. **Transfer to robot**
   - Copy needed folders/files to robot using a USB

3. **Work on robot**
   - Run experiments / training / testing

4. **Transfer back to PC**
   If you have editted the code on the robot, copy back to your PC into correct places.

5. **Back on PC – commit changes**
   - Push to github (follow the steps in A4).
  
### Branching & Merging Strategy
Rule of thumb: One branch per meaningful piece of work (eg. 1 training session homework)

1. Creating a new branch
   - You should start a new brach at each training session
   ```bash
   git checkout main
   git pull origin main
   git checkout -b new-branch
   ```

3. Working on branch
   - Commit often
   - Push regularly so others can see progress
   ```bash
   git push origin new-branch
   ```

4. Finishing & Merging
   - When the task is completed and reviewed, merge back to main
   Make sure branch is up-to-date
   ```bash
   git checkout new-branch
   git pull origin tnew-branch
   ```
   
   Switch to target branch (usually main)
   ```bash
   git checkout main
   git pull origin main
   ```
   
   Merge (use --no-ff to keep history clear)
   ```bash
   git merge new-branch --no-ff
   ```
   - resolve conflicts if any
   
   Push integrated result
   ```bash
   git push origin main

   (Optional – delete the branch)
   ```bash
   git branch -d new-branch
   git push origin --delete new-branch
   ```
   
## When Things Go Wrong

- Push rejected? git pull origin main first.
- Merge conflicts? Edit files (choose which version to keep, or edit manually), commit & push again. Usually safe to keep "theirs" or "ours" based on who changed the asset last.
- Still stuck? Run git status, screenshot errors, and ask excos.
