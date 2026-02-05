# Module 0: Environment & Tools

**Duration:** 2 weeks
**Goal:** Set up a professional development environment and establish version control habits

---

## Overview

Before writing code, you need the right tools. This module establishes the foundation you'll build on for the entire course. Every professional developer uses these tools daily.

By the end of this module, you will:
- Navigate your computer using the terminal
- Have a properly configured code editor
- Understand Git version control
- Have a GitHub profile ready to showcase your work

---

## Why These Tools?

Before diving in, let's understand why we're using these specific tools. Understanding the "why" helps you make informed decisions as you grow.

### Why Terminal Over GUI?

**Speed:** Once learned, terminal commands are faster than clicking through menus. Navigating to a deeply nested folder takes 2 seconds with `cd`, but 15 seconds of clicking.

**Power:** Some operations are only possible (or practical) via terminal. Renaming 100 files? One command. Searching through thousands of files? Instant.

**Universality:** Every server, every cloud platform, every deployment pipeline uses the terminal. GUIs don't exist on servers.

**Automation:** Terminal commands can be scripted. Repetitive tasks become one-click operations.

**Alternatives:** File managers like Finder (Mac) or Explorer (Windows) work for basic tasks, but become limiting as projects grow.

### Why VS Code Specifically?

**Industry standard:** Most web developers use VS Code. Learning it means you can collaborate easily and find abundant resources.

**Extensions:** The ecosystem is massive. Whatever you need—linting, formatting, language support—there's an extension.

**Free and open-source:** No licensing costs, active development, transparent roadmap.

**Integrated terminal:** Code and command line in one window reduces context switching.

**Alternatives:**
- **Sublime Text:** Lightweight, fast, but fewer integrations
- **WebStorm:** Powerful, but paid and heavier
- **Vim/Neovim:** Extremely powerful, steep learning curve
- **Zed:** New, fast, promising but less mature ecosystem

VS Code hits the sweet spot of power, ease of use, and community support.

### Why Git for Version Control?

**Universal adoption:** Git won. It's used by virtually every software company and open-source project.

**Distributed:** Your full project history lives on your machine. No internet needed for most operations.

**Branching model:** Git's branches are lightweight and encourage experimentation.

**GitHub integration:** Git + GitHub = collaboration, portfolio, and deployment platform in one.

**Alternatives:**
- **SVN (Subversion):** Older, centralized, still used in some enterprises
- **Mercurial:** Similar to Git, less popular
- **Perforce:** Used in game development for large binary files

Git's dominance makes it the only practical choice for web development.

### What About IDEs vs Text Editors?

VS Code is technically a text editor with IDE-like features via extensions. Full IDEs (like WebStorm) include everything built-in but are heavier. For JavaScript/React development, VS Code with the right extensions provides IDE-level features with text editor speed.

---

## Week 1: Terminal & Editor Setup

### Day 1-2: The Terminal

The terminal (also called command line or shell) is how developers interact with their computers. GUIs are for consumers; the terminal is for builders.

#### Concepts to Learn

- What is a shell? (bash, zsh)
- Navigating the file system
- File and directory operations
- Reading and understanding command output

#### Essential Commands

| Command | Purpose |
|---------|---------|
| `pwd` | Print working directory (where am I?) |
| `ls` | List directory contents |
| `ls -la` | List all files including hidden, with details |
| `cd` | Change directory |
| `cd ..` | Go up one directory |
| `cd ~` | Go to home directory |
| `mkdir` | Create a directory |
| `touch` | Create an empty file |
| `rm` | Remove a file |
| `rm -r` | Remove a directory and its contents |
| `cp` | Copy files |
| `mv` | Move or rename files |
| `cat` | Display file contents |
| `clear` | Clear the terminal screen |
| `history` | Show command history |

#### Path Concepts

- Absolute paths: `/Users/yourname/projects/myapp`
- Relative paths: `./src/index.js` or `../config`
- Home directory: `~`
- Current directory: `.`
- Parent directory: `..`

### Day 3-4: VS Code Setup

Visual Studio Code is the industry-standard editor. Learn it well.

#### Installation

1. Download VS Code from https://code.visualstudio.com
2. Install and open it
3. Open the terminal in VS Code: `` Ctrl+` `` (backtick)

#### Essential Extensions

Install these extensions (Cmd/Ctrl+Shift+X to open extensions):

| Extension | Purpose |
|-----------|---------|
| ESLint | JavaScript linting |
| Prettier | Code formatting |
| GitLens | Enhanced Git integration |
| Error Lens | Inline error display |
| Auto Rename Tag | HTML/JSX tag renaming |

#### Key Settings

Open settings (Cmd/Ctrl+,) and configure:

- **Format On Save:** Enable (saves time, enforces consistency)
- **Tab Size:** 2 (JavaScript convention)
- **Word Wrap:** On (prevents horizontal scrolling)
- **Auto Save:** afterDelay (prevents lost work)

#### Essential Shortcuts

| Action | Mac | Windows |
|--------|-----|---------|
| Command Palette | Cmd+Shift+P | Ctrl+Shift+P |
| Quick Open File | Cmd+P | Ctrl+P |
| Toggle Terminal | Ctrl+` | Ctrl+` |
| Toggle Sidebar | Cmd+B | Ctrl+B |
| Find in File | Cmd+F | Ctrl+F |
| Find in Project | Cmd+Shift+F | Ctrl+Shift+F |
| Go to Line | Ctrl+G | Ctrl+G |
| Duplicate Line | Shift+Option+Down | Shift+Alt+Down |
| Move Line | Option+Up/Down | Alt+Up/Down |
| Multi-cursor | Option+Click | Alt+Click |
| Select Word | Cmd+D | Ctrl+D |

### Day 5: Node.js Installation

Node.js lets you run JavaScript outside the browser. You'll need it for the entire course.

#### Installation Steps

1. **Check if already installed:**
   ```
   node --version
   npm --version
   ```

2. **Install using nvm (recommended):**
   - nvm = Node Version Manager
   - Allows switching between Node versions
   - Install from: https://github.com/nvm-sh/nvm

   ```
   nvm install --lts
   nvm use --lts
   ```

3. **Verify installation:**
   ```
   node --version
   npm --version
   ```

#### First Node Program

Create a file called `hello.js`:
```javascript
console.log("Hello from Node.js!");
```

Run it:
```
node hello.js
```

### Week 1 Review Prompts

Before moving to Week 2, take 10 minutes to reflect:

1. **What did you learn this week?**
   Write 3-5 bullet points about new concepts or skills you acquired.

2. **What's still unclear?**
   List anything that felt confusing. Revisit those sections or search for additional explanations.

3. **What would you teach someone else?**
   If you had to explain one concept from this week to a friend, what would it be and how would you explain it?

---

## Week 2: Git & GitHub

### Day 1-2: Git Fundamentals

Git tracks changes to your code. Every professional project uses it.

#### Why Git?

- **History:** See every change ever made
- **Backup:** Never lose work
- **Collaboration:** Work with others without conflicts
- **Experimentation:** Try ideas safely with branches

#### Core Concepts

| Concept | Description |
|---------|-------------|
| Repository (repo) | A project tracked by Git |
| Commit | A snapshot of your code at a point in time |
| Branch | A parallel version of your code |
| Merge | Combining changes from different branches |
| Remote | A copy of your repo on another server (like GitHub) |

#### Essential Commands

**Setup (once per computer):**
```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

**Starting a project:**
```
git init                    # Initialize a new repo
git clone <url>             # Copy an existing repo
```

**Daily workflow:**
```
git status                  # See what's changed
git add <file>              # Stage a file for commit
git add .                   # Stage all changes
git commit -m "message"     # Save staged changes
git log                     # View commit history
git log --oneline           # Compact history view
```

**Branching:**
```
git branch                  # List branches
git branch <name>           # Create a branch
git checkout <name>         # Switch to a branch
git checkout -b <name>      # Create and switch
git merge <branch>          # Merge branch into current
```

**Remote operations:**
```
git remote add origin <url> # Connect to remote
git push -u origin main     # Push to remote (first time)
git push                    # Push to remote
git pull                    # Get changes from remote
```

### Day 3-4: GitHub Setup

GitHub hosts your repositories online. It's also your portfolio.

#### Account Setup

1. Create account at https://github.com
2. Set up SSH key for secure access:
   ```
   ssh-keygen -t ed25519 -C "your@email.com"
   ```
3. Add public key to GitHub (Settings → SSH Keys)
4. Test connection:
   ```
   ssh -T git@github.com
   ```

#### Profile Configuration

Your GitHub profile is your developer resume. Configure it:

1. **Profile photo:** Professional, recognizable
2. **Bio:** Brief description of your journey
3. **Pinned repositories:** Your best work (we'll add these as you build)
4. **README profile:** Create a repo named your username with a README.md

#### Repository Best Practices

- **One project per repo**
- **Meaningful repo names:** `todo-app` not `project1`
- **Always include a README.md**
- **Use .gitignore** to exclude node_modules, .env files
- **Commit often** with clear messages

### Day 5: Commit Message Standards

Good commit messages tell a story. Write for your future self.

#### Message Format

```
<type>: <short description>

<optional longer description>
```

#### Types

| Type | When to Use |
|------|-------------|
| feat | New feature |
| fix | Bug fix |
| docs | Documentation changes |
| style | Formatting, no code change |
| refactor | Code restructuring |
| test | Adding tests |
| chore | Maintenance tasks |

#### Examples

Good:
```
feat: add user login form
fix: prevent crash when email is empty
refactor: extract validation into separate function
```

Bad:
```
updated stuff
fix
asdfasdf
WIP
```

### Week 2 Review Prompts

Before moving to the labs, take 10 minutes to reflect:

1. **What did you learn this week?**
   Write 3-5 bullet points about Git and GitHub concepts you now understand.

2. **What's still unclear?**
   Branching? Merging? Remotes? Identify gaps and revisit those sections.

3. **What would you teach someone else?**
   Could you explain the difference between `git add`, `git commit`, and `git push` to a complete beginner?

---

## Labs

### Lab 0.1: Terminal Navigation

🔴 **Core** — must complete before moving on

**Objective:** Become comfortable navigating your file system using only the terminal.

**Tasks:**
1. Open your terminal
2. Navigate to your home directory
3. Create a directory called `dev`
4. Inside `dev`, create a directory called `zero-to-fullstack`
5. Inside that, create directories for each module: `module-0`, `module-1`, etc. through `module-6`
6. Create a file called `notes.txt` in `module-0`
7. List all contents of `zero-to-fullstack` to verify your structure
8. Navigate back to your home directory using a relative path
9. Navigate to `module-0` using an absolute path

**Verification:** Run `ls -la` in your `zero-to-fullstack` directory. You should see 7 module directories.

---

### Lab 0.2: VS Code Mastery

🟡 **Recommended** — reinforces understanding

**Objective:** Learn VS Code shortcuts through practice.

**Tasks:**
1. Open VS Code
2. Create a new file using keyboard shortcuts only (Cmd/Ctrl+N)
3. Save it as `shortcut-practice.txt` in your `module-0` folder
4. Type the following text:
   ```
   Line one
   Line two
   Line three
   Line four
   Line five
   ```
5. Using only keyboard shortcuts:
   - Duplicate line three
   - Move line one to become line four
   - Select all instances of "Line" and change to "Item"
   - Go to line 3
   - Open the command palette and change the language mode to JavaScript
6. Open the integrated terminal
7. Run `pwd` to verify you're in the right location

**Verification:** Your file should have 6 lines, all starting with "Item".

---

### Lab 0.3: First Git Repository

🔴 **Core** — must complete before moving on

**Objective:** Create and manage your first Git repository.

**Tasks:**
1. Navigate to your `module-0` directory
2. Initialize a Git repository
3. Check the status
4. Create a file called `README.md` with the following content:
   ```markdown
   # Module 0: Environment & Tools

   Learning terminal, VS Code, and Git.

   ## Progress

   - [ ] Terminal basics
   - [ ] VS Code setup
   - [ ] Git fundamentals
   ```
5. Stage the file
6. Commit with message: `feat: add initial README`
7. Create a file called `.gitignore` with:
   ```
   node_modules/
   .DS_Store
   .env
   ```
8. Stage and commit: `chore: add gitignore`
9. View your commit history

**Verification:** `git log --oneline` should show 2 commits.

---

### Lab 0.4: GitHub Connection

🔴 **Core** — must complete before moving on

**Objective:** Push your local repository to GitHub.

**Tasks:**
1. Create a new repository on GitHub called `zero-to-fullstack-module-0`
2. Do NOT initialize with README (you already have one)
3. Connect your local repo to GitHub using the provided commands
4. Push your commits
5. Verify on GitHub that your files appear
6. Edit the README on GitHub (add a line)
7. Pull the changes to your local machine
8. Verify the change appears locally

**Verification:** Your GitHub repo shows both commits, and local matches remote.

---

### Lab 0.5: Branching Practice

🟡 **Recommended** — reinforces understanding

**Objective:** Practice Git branching workflow.

**Tasks:**
1. Create a new branch called `add-notes`
2. Switch to that branch
3. Create a file called `day1-notes.md` with any content about what you learned
4. Stage and commit: `docs: add day 1 learning notes`
5. Switch back to main branch
6. Notice the notes file is gone (it's on the other branch)
7. Merge `add-notes` into main
8. Notice the notes file now appears
9. Delete the `add-notes` branch (it's been merged)
10. Push everything to GitHub

**Verification:** GitHub shows 4 commits total, and the notes file exists on main.

---

### Lab 0.6: Explore Git History

🟢 **Stretch** — for deeper mastery

**Objective:** Learn to navigate and understand Git history.

**Tasks:**
1. View your commit history with `git log`
2. View a compact history with `git log --oneline`
3. View history with a graph: `git log --oneline --graph --all`
4. Show details of a specific commit: `git show <commit-hash>`
5. See what changed between two commits: `git diff <hash1>..<hash2>`
6. View who last modified each line of a file: `git blame README.md`
7. Find when a specific line was added: `git log -S "some text" --oneline`

**Verification:** You can explain what each command does and when you'd use it.

---

### Lab 0.7: Terminal Power User

🟢 **Stretch** — for deeper mastery

**Objective:** Learn advanced terminal techniques.

**Tasks:**
1. Use `tab` completion to autocomplete file and folder names
2. Use `up arrow` to recall previous commands
3. Use `Ctrl+R` to search command history
4. Create an alias: add `alias ll='ls -la'` to your shell config file
5. Chain commands with `&&`: `mkdir test && cd test && touch file.txt`
6. Use pipes: `history | grep git` (find all git commands you've run)
7. Use output redirection: `ls -la > files.txt` (save output to file)

**Verification:** You can navigate faster using these techniques.

---

## First Deployment Checkpoint

### GitHub Profile Setup

By the end of Week 2, complete the following:

1. **Profile photo** uploaded
2. **Bio** written (1-2 sentences about your developer journey)
3. **One pinned repository** (your module-0 repo)
4. **SSH key** configured (no password prompts when pushing)

### Verification Checklist

- [ ] Can navigate file system using terminal only
- [ ] VS Code installed with essential extensions
- [ ] Node.js installed and working
- [ ] Git configured with name and email
- [ ] GitHub account created and SSH configured
- [ ] First repository created, committed, and pushed
- [ ] Comfortable with basic branching workflow

---

## Common Issues & Solutions

### "Permission denied" when pushing
- SSH key not set up correctly
- Run `ssh -T git@github.com` to test
- Regenerate and add key if needed

### "git: command not found"
- Git not installed
- On Mac: `xcode-select --install`
- On Windows: Download Git from git-scm.com

### "node: command not found"
- Node not installed or not in PATH
- Reinstall using nvm
- Restart terminal after installation

### "Cannot push to main"
- Branch might be called `master` not `main`
- Check with `git branch`
- Rename: `git branch -m master main`

---

## Can You Do This? (Self-Assessment)

Before moving to Module 1, complete these challenges **without looking at notes or hints**. If you can do them all, you're ready. If not, review the relevant sections.

### Challenge 1: Terminal Navigation
Starting from your home directory, navigate to `~/dev/zero-to-fullstack/module-0` using only terminal commands, then return to home using a relative path.

### Challenge 2: File Operations
Create a folder called `test-folder`, create three files inside it (`a.txt`, `b.txt`, `c.txt`), then delete the entire folder and its contents with one command.

### Challenge 3: Git Workflow
Initialize a new Git repo, create a file, stage it, commit it with a proper commit message, then view your commit history.

### Challenge 4: Branching
Create a new branch, make a change, commit it, switch back to main, and merge your branch.

### Challenge 5: GitHub Push
Push a local repository to a new GitHub repo you create. Verify it appears on GitHub.

### Challenge 6: VS Code Speed
Open a file in VS Code, duplicate a line, move a line up/down, open the command palette, and toggle the terminal—all using only keyboard shortcuts.

**How did you do?**
- All 6 completed easily: You're ready for Module 1!
- 4-5 completed: Review the challenging areas, then proceed
- Fewer than 4: Spend another day practicing before moving on

---

## Recommended Resources

### Video Tutorial
**"Git and GitHub for Beginners" by freeCodeCamp** (YouTube, ~1 hour)
A comprehensive visual walkthrough of Git concepts. Watch this if the text explanations aren't clicking.
https://www.youtube.com/watch?v=RGOj5yH7evk

### Article/Guide
**"The Missing Semester of Your CS Education: The Shell"** (MIT)
Deeper dive into terminal usage from MIT's free course. Excellent for understanding *why* things work, not just *how*.
https://missing.csail.mit.edu/2020/course-shell/

### Official Documentation
- **Git Documentation:** https://git-scm.com/doc
- **VS Code Documentation:** https://code.visualstudio.com/docs
- **Node.js Documentation:** https://nodejs.org/en/docs/
- **GitHub Docs:** https://docs.github.com/en

### Quick References
- **Git Cheat Sheet (GitHub):** https://education.github.com/git-cheat-sheet-education.pdf
- **VS Code Keyboard Shortcuts:** https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf (Mac) or https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf (Windows)

---

## Next Steps

Once you've completed all labs and the deployment checkpoint, proceed to [Module 1: Programming Fundamentals](module-1-programming-fundamentals.md).

Remember: The tools you learned in this module—terminal, editor, Git—will be used every single day of your development career. If anything feels shaky, revisit it before moving on.
