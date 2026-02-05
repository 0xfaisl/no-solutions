# Troubleshooting Guide

A comprehensive reference for debugging common errors across your development journey. When something breaks, start here.

---

## Table of Contents

1. [General / Environment Issues](#general--environment-issues)
2. [Terminal Issues](#terminal-issues)
3. [Git Issues](#git-issues)
4. [Node.js / npm Issues](#nodejs--npm-issues)
5. [JavaScript Runtime Errors](#javascript-runtime-errors)
6. [React Issues](#react-issues)
7. [TypeScript Issues](#typescript-issues)
8. [Database / PostgreSQL Issues](#database--postgresql-issues)
9. [Express / API Issues](#express--api-issues)
10. [Deployment Issues](#deployment-issues)

---

## General / Environment Issues

### "command not found" errors

**Error message:**
```
zsh: command not found: <command>
bash: command not found: <command>
```

**What it means:**
Your shell cannot locate the executable for the command you're trying to run. Either the program isn't installed, or it's not in your system's PATH.

**How to fix it:**
1. Verify the program is installed:
   ```bash
   # For Homebrew packages (macOS)
   brew list | grep <package>

   # Check if binary exists somewhere
   which <command>
   ```

2. If not installed, install it:
   ```bash
   # macOS
   brew install <package>

   # npm global packages
   npm install -g <package>
   ```

3. If installed but not found, add to PATH in `~/.zshrc` or `~/.bashrc`:
   ```bash
   export PATH="/path/to/binary:$PATH"
   ```

4. Reload your shell:
   ```bash
   source ~/.zshrc
   ```

**How to prevent it:**
- Always restart your terminal after installing new tools
- Keep track of where tools are installed
- Use a version manager (nvm, rbenv) that handles PATH automatically

---

### Permission denied errors

**Error message:**
```
Error: EACCES: permission denied
npm ERR! Error: EACCES, permission denied
```

**What it means:**
You're trying to access or modify a file/directory that your user account doesn't have permission for.

**How to fix it:**
1. **Never use `sudo npm install`** - this creates permission issues

2. Fix npm permissions (recommended approach):
   ```bash
   # Create a directory for global packages
   mkdir ~/.npm-global

   # Configure npm to use it
   npm config set prefix '~/.npm-global'

   # Add to PATH in ~/.zshrc
   export PATH=~/.npm-global/bin:$PATH

   # Reload shell
   source ~/.zshrc
   ```

3. Or use nvm (best solution):
   ```bash
   # nvm manages its own directory, avoiding permission issues
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
   ```

**How to prevent it:**
- Use nvm for Node.js management
- Never install npm packages globally with sudo
- Keep projects in your home directory

---

### PATH issues

**Error message:**
```
command not found: node
# (even though you just installed it)
```

**What it means:**
The PATH environment variable tells your shell where to look for executables. If a program's location isn't in PATH, the shell can't find it.

**How to fix it:**
1. Find where the program is installed:
   ```bash
   # Find node, for example
   find /usr -name "node" 2>/dev/null
   find /opt -name "node" 2>/dev/null
   ```

2. Check your current PATH:
   ```bash
   echo $PATH
   ```

3. Add the directory to PATH in `~/.zshrc`:
   ```bash
   # Add this line (adjust path as needed)
   export PATH="/usr/local/bin:$PATH"
   ```

4. Reload:
   ```bash
   source ~/.zshrc
   ```

**How to prevent it:**
- Use version managers (nvm, pyenv) that handle PATH
- Read installation instructions carefully
- Keep your shell config file organized

---

### Node/npm version mismatches

**Error message:**
```
error <package>@x.x.x: The engine "node" is incompatible with this module
npm WARN EBADENGINE Unsupported engine
```

**What it means:**
The project requires a different Node.js version than what you have installed.

**How to fix it:**
1. Check required version in `package.json`:
   ```json
   "engines": {
     "node": ">=18.0.0"
   }
   ```

2. Check your current version:
   ```bash
   node --version
   npm --version
   ```

3. Switch versions with nvm:
   ```bash
   # Install required version
   nvm install 18

   # Use it
   nvm use 18

   # Set as default
   nvm alias default 18
   ```

4. If project has `.nvmrc` file:
   ```bash
   nvm use
   ```

**How to prevent it:**
- Always check project requirements before starting
- Use `.nvmrc` files in your projects
- Run `nvm use` when switching projects

---

## Terminal Issues

### Command not found (git, node, npm)

**Error message:**
```
zsh: command not found: git
zsh: command not found: node
zsh: command not found: npm
```

**What it means:**
The tool isn't installed, or it's not in your PATH.

**How to fix it:**

For **git**:
```bash
# macOS (comes with Xcode Command Line Tools)
xcode-select --install

# Or via Homebrew
brew install git
```

For **node/npm**:
```bash
# Using nvm (recommended)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.zshrc
nvm install --lts
nvm use --lts

# Or via Homebrew
brew install node
```

**How to prevent it:**
- Set up your development environment completely before starting projects
- Keep a checklist of required tools

---

### "zsh: permission denied"

**Error message:**
```
zsh: permission denied: ./script.sh
```

**What it means:**
You're trying to execute a file that doesn't have execute permissions.

**How to fix it:**
```bash
# Add execute permission
chmod +x ./script.sh

# Then run it
./script.sh
```

**How to prevent it:**
- When creating scripts, remember to make them executable
- Use `npm scripts` in package.json instead of shell scripts when possible

---

### Terminal not recognizing installed programs

**Error message:**
```
# You just installed something, but terminal says "command not found"
```

**What it means:**
Your terminal session hasn't loaded the updated PATH or configuration.

**How to fix it:**
1. **Restart your terminal** (easiest)

2. Or reload your shell config:
   ```bash
   # For zsh
   source ~/.zshrc

   # For bash
   source ~/.bashrc
   ```

3. Start a new shell:
   ```bash
   exec $SHELL
   ```

**How to prevent it:**
- Always restart terminal after installing development tools
- Add a reminder to installation notes

---

### How to check if something is installed

**Verification commands:**
```bash
# Check if command exists and show version
git --version
node --version
npm --version
psql --version

# Find where a command is located
which git
which node

# Check if command exists (returns path or nothing)
command -v git

# List all versions available (nvm)
nvm ls

# Check what's installed via Homebrew
brew list
```

---

## Git Issues

### "fatal: not a git repository"

**Error message:**
```
fatal: not a git repository (or any of the parent directories): .git
```

**What it means:**
You're trying to run a git command in a directory that isn't a git repository.

**How to fix it:**
1. Check if you're in the right directory:
   ```bash
   pwd
   ls -la  # Look for .git folder
   ```

2. Navigate to your project root:
   ```bash
   cd /path/to/your/project
   ```

3. Or initialize a new repository:
   ```bash
   git init
   ```

**How to prevent it:**
- Always verify you're in the project directory before running git commands
- Use your terminal prompt to show git status (oh-my-zsh does this)

---

### Merge conflicts

**Error message:**
```
CONFLICT (content): Merge conflict in <filename>
Automatic merge failed; fix conflicts and then commit the result.
```

**What it means:**
Git found changes in the same location from two different branches and doesn't know which to keep.

**How to fix it:**
1. Open the conflicting file(s). Look for conflict markers:
   ```
   <<<<<<< HEAD
   your changes
   =======
   their changes
   >>>>>>> branch-name
   ```

2. Edit the file to resolve:
   - Keep your changes, their changes, or combine them
   - Remove all conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)

3. Mark as resolved and commit:
   ```bash
   git add <filename>
   git commit -m "Resolve merge conflict in <filename>"
   ```

4. If you want to abort the merge:
   ```bash
   git merge --abort
   ```

**How to prevent it:**
- Pull frequently to stay up to date
- Communicate with teammates about who's working on what
- Keep commits small and focused

---

### "Please tell me who you are" (config not set)

**Error message:**
```
*** Please tell me who you are.

Run
  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"
```

**What it means:**
Git needs to know who you are to attribute commits.

**How to fix it:**
```bash
# Set your identity (use your GitHub email)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Verify
git config --global --list
```

**How to prevent it:**
- Set this up immediately after installing Git
- Add to your development environment setup checklist

---

### SSH key problems ("Permission denied (publickey)")

**Error message:**
```
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.
```

**What it means:**
GitHub doesn't recognize your SSH key, or you don't have one set up.

**How to fix it:**
1. Check for existing SSH keys:
   ```bash
   ls -la ~/.ssh
   # Look for id_ed25519.pub or id_rsa.pub
   ```

2. Generate a new key if needed:
   ```bash
   ssh-keygen -t ed25519 -C "your.email@example.com"
   # Press Enter to accept default location
   # Enter a passphrase (recommended)
   ```

3. Start the SSH agent and add your key:
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   ```

4. Copy the public key:
   ```bash
   # macOS
   pbcopy < ~/.ssh/id_ed25519.pub

   # Or display it
   cat ~/.ssh/id_ed25519.pub
   ```

5. Add to GitHub:
   - Go to GitHub > Settings > SSH and GPG keys > New SSH key
   - Paste your key and save

6. Test the connection:
   ```bash
   ssh -T git@github.com
   # Should say: "Hi username! You've successfully authenticated"
   ```

**How to prevent it:**
- Set up SSH keys when you first install Git
- Use SSH URLs for remotes: `git@github.com:user/repo.git`

---

### Accidentally committed to wrong branch

**Error message:**
No error - you just realize you committed to `main` instead of a feature branch.

**How to fix it:**

**If you haven't pushed yet:**
```bash
# Create new branch with your commits
git branch new-feature-branch

# Reset main to before your commits
git reset --hard HEAD~1  # Go back 1 commit

# Switch to new branch
git checkout new-feature-branch
```

**If you've already pushed:**
```bash
# Create new branch from current state
git checkout -b new-feature-branch

# Go back to main
git checkout main

# Revert the commit (creates a new commit that undoes changes)
git revert HEAD

# Push both branches
git push origin main
git push origin new-feature-branch
```

**How to prevent it:**
- Always check which branch you're on before committing
- Use branch name in terminal prompt
- Create feature branches immediately when starting new work

---

### How to undo last commit

**Scenarios and solutions:**

**Undo commit, keep changes staged:**
```bash
git reset --soft HEAD~1
```

**Undo commit, keep changes unstaged:**
```bash
git reset HEAD~1
# or
git reset --mixed HEAD~1
```

**Undo commit and discard changes completely:**
```bash
git reset --hard HEAD~1
# WARNING: This permanently deletes your changes!
```

**Undo a commit that's already pushed:**
```bash
# Create a new commit that reverses the changes
git revert HEAD
git push
```

**Oops, I want that commit back!**
```bash
# Find the commit hash
git reflog

# Restore it
git cherry-pick <commit-hash>
```

---

## Node.js / npm Issues

### "npm ERR! code ENOENT"

**Error message:**
```
npm ERR! code ENOENT
npm ERR! syscall open
npm ERR! path /path/to/package.json
npm ERR! errno -2
npm ERR! enoent ENOENT: no such file or directory
```

**What it means:**
npm can't find a file it needs, usually `package.json`.

**How to fix it:**
1. Make sure you're in the right directory:
   ```bash
   pwd
   ls  # Should see package.json
   ```

2. If starting a new project:
   ```bash
   npm init -y
   ```

3. If package.json exists but npm still fails:
   ```bash
   # Check for typos in scripts or file paths
   cat package.json
   ```

**How to prevent it:**
- Always navigate to project root before running npm commands
- Verify package.json exists before running npm install

---

### "Module not found"

**Error message:**
```
Error: Cannot find module 'express'
Module not found: Can't resolve 'react'
```

**What it means:**
The code is trying to import a package that isn't installed.

**How to fix it:**
1. Install the missing package:
   ```bash
   npm install <package-name>
   ```

2. If it's a dev dependency:
   ```bash
   npm install --save-dev <package-name>
   ```

3. If packages should be installed but aren't:
   ```bash
   rm -rf node_modules package-lock.json
   npm install
   ```

4. Check for typos in import statement:
   ```javascript
   // Wrong
   import Expresss from 'express';

   // Right
   import express from 'express';
   ```

**How to prevent it:**
- Run `npm install` after cloning a project
- Check import statements match package names exactly
- Review package.json when errors occur

---

### Node version issues (nvm commands)

**Common scenarios and fixes:**

**Check current version:**
```bash
node --version
nvm current
```

**List installed versions:**
```bash
nvm ls
```

**List available versions:**
```bash
nvm ls-remote
```

**Install a specific version:**
```bash
nvm install 18
nvm install 20.10.0
nvm install --lts
```

**Switch versions:**
```bash
nvm use 18
nvm use --lts
```

**Set default version:**
```bash
nvm alias default 18
```

**Use project's .nvmrc:**
```bash
# If project has .nvmrc file
nvm use
```

**nvm command not found after installation:**
```bash
# Add to ~/.zshrc
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

# Reload
source ~/.zshrc
```

---

### Package conflicts

**Error message:**
```
npm ERR! ERESOLVE unable to resolve dependency tree
npm ERR! peer dep missing
```

**What it means:**
Two packages require different versions of the same dependency.

**How to fix it:**
1. Try with legacy peer deps flag:
   ```bash
   npm install --legacy-peer-deps
   ```

2. Or force installation:
   ```bash
   npm install --force
   ```

3. Check which packages conflict:
   ```bash
   npm ls <package-name>
   ```

4. Update packages to compatible versions:
   ```bash
   npm update
   ```

**How to prevent it:**
- Keep dependencies up to date
- Check compatibility before adding new packages
- Use exact versions in package.json when stability matters

---

### Clearing npm cache

**When to do it:**
- Strange installation errors
- Packages not updating properly
- Corruption errors

**How to clear:**
```bash
# Verify cache (finds corrupted packages)
npm cache verify

# Force clean (last resort)
npm cache clean --force
```

**Nuclear option (when nothing else works):**
```bash
rm -rf node_modules
rm package-lock.json
npm cache clean --force
npm install
```

---

### node_modules issues (delete and reinstall)

**Error message:**
Various errors about modules, corrupted packages, or just weird behavior.

**How to fix it:**

**Basic reinstall:**
```bash
rm -rf node_modules
npm install
```

**Full clean reinstall:**
```bash
rm -rf node_modules
rm package-lock.json
npm install
```

**If using multiple package managers:**
```bash
# Make sure you're using the right one
rm -rf node_modules
rm package-lock.json  # npm
rm yarn.lock          # yarn
rm pnpm-lock.yaml     # pnpm

# Then install with correct manager
npm install
# or
yarn
# or
pnpm install
```

**How to prevent it:**
- Stick to one package manager per project
- Commit lock files to git
- Don't manually edit node_modules

---

## JavaScript Runtime Errors

### "undefined is not a function"

**Error message:**
```
TypeError: undefined is not a function
TypeError: x is not a function
```

**What it means:**
You're trying to call something as a function, but it's not a function.

**How to fix it:**
1. Check if the function exists:
   ```javascript
   console.log(typeof myFunction);  // Should be "function"
   ```

2. Check import/export:
   ```javascript
   // Wrong - importing non-existent export
   import { myFunction } from './utils';

   // Check utils.js actually exports myFunction
   export function myFunction() { }
   ```

3. Check for typos:
   ```javascript
   // Wrong
   array.mapp(x => x * 2);

   // Right
   array.map(x => x * 2);
   ```

4. Check method exists on object:
   ```javascript
   // data might be undefined
   data.forEach(item => console.log(item));

   // Safe version
   data?.forEach(item => console.log(item));
   ```

**How to prevent it:**
- Use TypeScript for type checking
- Always verify data exists before calling methods
- Use optional chaining (`?.`)

---

### "Cannot read property X of undefined"

**Error message:**
```
TypeError: Cannot read property 'name' of undefined
TypeError: Cannot read properties of undefined (reading 'name')
```

**What it means:**
You're trying to access a property on something that is `undefined`.

**How to fix it:**
1. Find what's undefined:
   ```javascript
   // If error is: Cannot read property 'name' of undefined
   console.log(user);  // This is undefined
   console.log(user.name);  // This fails
   ```

2. Add null checks:
   ```javascript
   // Traditional
   if (user && user.name) {
     console.log(user.name);
   }

   // Optional chaining (modern)
   console.log(user?.name);

   // With default value
   console.log(user?.name ?? 'Unknown');
   ```

3. Check async data:
   ```javascript
   // Data might not be loaded yet
   const [user, setUser] = useState(null);

   // Guard against null
   if (!user) return <Loading />;
   return <div>{user.name}</div>;
   ```

**How to prevent it:**
- Initialize variables with default values
- Use optional chaining (`?.`)
- Handle loading states for async data
- Use TypeScript with strict null checks

---

### "Unexpected token"

**Error message:**
```
SyntaxError: Unexpected token '{'
SyntaxError: Unexpected token '<'
SyntaxError: Unexpected identifier
```

**What it means:**
There's a syntax error in your code - JavaScript can't parse it.

**How to fix it:**
1. **"Unexpected token '<'"** usually means:
   - Trying to run JSX without a transpiler
   - Importing an HTML file as JavaScript
   ```javascript
   // Wrong - JSX in a .js file without proper setup
   const App = () => <div>Hello</div>;

   // Fix: Use .jsx extension or configure babel
   ```

2. **"Unexpected token '{'"** usually means:
   - Missing parentheses or brackets somewhere
   - Incorrect destructuring syntax
   ```javascript
   // Wrong
   function greet(name { console.log(name); }

   // Right
   function greet(name) { console.log(name); }
   ```

3. **Check for:**
   - Missing commas in objects/arrays
   - Unclosed brackets, braces, or parentheses
   - Missing semicolons (in some cases)
   - Copy-pasted special characters

**How to prevent it:**
- Use a code editor with syntax highlighting
- Install ESLint for automatic syntax checking
- Use Prettier for consistent formatting

---

### Reference errors

**Error message:**
```
ReferenceError: x is not defined
```

**What it means:**
You're using a variable that hasn't been declared.

**How to fix it:**
1. Check for typos:
   ```javascript
   // Wrong
   const userName = "Alice";
   console.log(username);  // typo!

   // Right
   console.log(userName);
   ```

2. Check scope:
   ```javascript
   // Wrong - x only exists inside the if block
   if (true) {
     const x = 5;
   }
   console.log(x);  // ReferenceError

   // Right
   let x;
   if (true) {
     x = 5;
   }
   console.log(x);
   ```

3. Check imports:
   ```javascript
   // Forgot to import
   console.log(moment());  // ReferenceError

   // Fix
   import moment from 'moment';
   console.log(moment());
   ```

**How to prevent it:**
- Use `const` and `let` (not `var`) for clearer scoping
- Use ESLint to catch undefined variables
- Verify imports at the top of files

---

### Type errors

**Error message:**
```
TypeError: Assignment to constant variable
TypeError: x.toUpperCase is not a function
```

**What it means:**
You're performing an operation on a value of the wrong type.

**How to fix it:**
1. **"Assignment to constant variable":**
   ```javascript
   // Wrong
   const name = "Alice";
   name = "Bob";  // TypeError

   // Right - use let if you need to reassign
   let name = "Alice";
   name = "Bob";
   ```

2. **Method doesn't exist on type:**
   ```javascript
   // Wrong - calling string method on number
   const num = 123;
   num.toUpperCase();  // TypeError

   // Right
   const num = 123;
   num.toString().toUpperCase();  // "123"
   ```

3. Check your data types:
   ```javascript
   console.log(typeof variable);
   console.log(Array.isArray(variable));
   ```

**How to prevent it:**
- Use TypeScript for static type checking
- Validate data before operating on it
- Use descriptive variable names

---

### Async/Promise errors ("Unhandled promise rejection")

**Error message:**
```
UnhandledPromiseRejectionWarning: Error: something went wrong
Unhandled promise rejection
```

**What it means:**
A Promise was rejected but there's no `.catch()` or `try/catch` to handle the error.

**How to fix it:**
1. **With .then()/.catch():**
   ```javascript
   // Wrong
   fetch('/api/data').then(res => res.json());

   // Right
   fetch('/api/data')
     .then(res => res.json())
     .catch(err => console.error('Failed:', err));
   ```

2. **With async/await:**
   ```javascript
   // Wrong
   async function getData() {
     const res = await fetch('/api/data');
     return res.json();
   }

   // Right
   async function getData() {
     try {
       const res = await fetch('/api/data');
       return res.json();
     } catch (err) {
       console.error('Failed:', err);
       throw err;  // Re-throw if caller should handle it
     }
   }
   ```

3. **Handle when calling async functions:**
   ```javascript
   // Wrong
   getData();

   // Right
   getData().catch(err => console.error(err));

   // Or in async context
   try {
     await getData();
   } catch (err) {
     console.error(err);
   }
   ```

**How to prevent it:**
- Always add error handling to async operations
- Use ESLint rules to require catch handlers
- Create reusable error handling utilities

---

## React Issues

### "Invalid hook call"

**Error message:**
```
Error: Invalid hook call. Hooks can only be called inside of the body of a function component.
```

**What it means:**
You're breaking one of the Rules of Hooks.

**How to fix it:**
1. **Hooks must be in function components or custom hooks:**
   ```javascript
   // Wrong - hook in regular function
   function getData() {
     const [data, setData] = useState(null);  // Error!
   }

   // Right - hook in component
   function MyComponent() {
     const [data, setData] = useState(null);  // OK
   }

   // Right - hook in custom hook
   function useData() {
     const [data, setData] = useState(null);  // OK
     return data;
   }
   ```

2. **Hooks must be at the top level:**
   ```javascript
   // Wrong - hook inside condition
   function MyComponent() {
     if (someCondition) {
       const [value, setValue] = useState(0);  // Error!
     }
   }

   // Right
   function MyComponent() {
     const [value, setValue] = useState(0);  // OK
     if (someCondition) {
       // use value here
     }
   }
   ```

3. **Check for duplicate React:**
   ```bash
   npm ls react
   # Should show only one version
   ```

**How to prevent it:**
- Name custom hooks with `use` prefix
- Never call hooks conditionally
- Use the ESLint react-hooks plugin

---

### "Objects are not valid as a React child"

**Error message:**
```
Error: Objects are not valid as a React child (found: object with keys {x, y}).
If you meant to render a collection of children, use an array instead.
```

**What it means:**
You're trying to render a JavaScript object directly in JSX.

**How to fix it:**
1. **Render specific properties:**
   ```javascript
   // Wrong
   const user = { name: 'Alice', age: 25 };
   return <div>{user}</div>;  // Error!

   // Right
   return <div>{user.name}</div>;
   ```

2. **Convert to string if needed:**
   ```javascript
   // For debugging
   return <div>{JSON.stringify(user)}</div>;
   ```

3. **Map arrays properly:**
   ```javascript
   // Wrong
   const users = [{ name: 'Alice' }, { name: 'Bob' }];
   return <div>{users}</div>;  // Error!

   // Right
   return (
     <div>
       {users.map(user => <p key={user.name}>{user.name}</p>)}
     </div>
   );
   ```

4. **Check for Date objects:**
   ```javascript
   // Wrong
   const date = new Date();
   return <div>{date}</div>;  // Error!

   // Right
   return <div>{date.toLocaleDateString()}</div>;
   ```

**How to prevent it:**
- Use TypeScript to catch type mismatches
- Always map arrays to JSX elements
- Convert objects to strings when debugging

---

### "Too many re-renders"

**Error message:**
```
Error: Too many re-renders. React limits the number of renders to prevent an infinite loop.
```

**What it means:**
Your component is updating state during render, causing an infinite loop.

**How to fix it:**
1. **Don't call setState directly in render:**
   ```javascript
   // Wrong
   function Counter() {
     const [count, setCount] = useState(0);
     setCount(count + 1);  // Infinite loop!
     return <div>{count}</div>;
   }

   // Right - use useEffect for side effects
   function Counter() {
     const [count, setCount] = useState(0);
     useEffect(() => {
       // Only runs once on mount
     }, []);
     return <div>{count}</div>;
   }
   ```

2. **Pass function reference, not function call:**
   ```javascript
   // Wrong
   <button onClick={handleClick()}>Click</button>  // Called immediately!

   // Right
   <button onClick={handleClick}>Click</button>

   // Right - if you need to pass arguments
   <button onClick={() => handleClick(id)}>Click</button>
   ```

3. **Check useEffect dependencies:**
   ```javascript
   // Wrong - object recreated every render
   useEffect(() => {
     fetchData(options);
   }, [options]);  // If options is new object each render = infinite loop

   // Right - use specific values
   useEffect(() => {
     fetchData({ limit });
   }, [limit]);
   ```

**How to prevent it:**
- Never call setState during render
- Always pass function references to event handlers
- Use useMemo/useCallback for stable references

---

### "Cannot update a component while rendering"

**Error message:**
```
Warning: Cannot update a component (`Parent`) while rendering a different component (`Child`)
```

**What it means:**
A child component is updating parent state during its render phase.

**How to fix it:**
```javascript
// Wrong
function Child({ onMount }) {
  onMount();  // Updates parent during render!
  return <div>Child</div>;
}

// Right - use useEffect
function Child({ onMount }) {
  useEffect(() => {
    onMount();
  }, [onMount]);
  return <div>Child</div>;
}
```

**How to prevent it:**
- Use useEffect for any side effects
- Never call callbacks during render

---

### Blank white screen (check console)

**Symptom:**
Your React app shows a blank white page.

**How to debug:**
1. **Open browser DevTools (F12 or Cmd+Option+I)**

2. **Check Console tab for errors:**
   - JavaScript errors crash the app
   - Fix the error shown

3. **Check Elements tab:**
   - Is the root div empty?
   - Look for `<div id="root"></div>`

4. **Common causes:**
   ```javascript
   // Forgetting to export
   const App = () => <div>Hello</div>;
   // Missing: export default App;

   // Typo in import
   import App from './app';  // File is App.js

   // Error in component
   const App = () => {
     return <div>{undefined.property}</div>;  // Crashes
   };
   ```

5. **Add error boundary:**
   ```javascript
   class ErrorBoundary extends React.Component {
     state = { hasError: false };

     static getDerivedStateFromError(error) {
       return { hasError: true };
     }

     render() {
       if (this.state.hasError) {
         return <h1>Something went wrong.</h1>;
       }
       return this.props.children;
     }
   }
   ```

**How to prevent it:**
- Use error boundaries
- Check console frequently during development
- Use React Developer Tools extension

---

### Hot reload not working

**Symptom:**
Changes to code don't appear in the browser without manual refresh.

**How to fix it:**
1. **Check if dev server is running:**
   ```bash
   # Should see compilation messages
   npm run dev
   ```

2. **Check file is being watched:**
   - Is file in `src` directory?
   - Is file imported somewhere?

3. **Check for syntax errors:**
   - Errors can break hot reload
   - Check terminal and console

4. **Restart dev server:**
   ```bash
   # Ctrl+C to stop
   npm run dev
   ```

5. **Clear caches:**
   ```bash
   rm -rf node_modules/.vite
   rm -rf .next
   npm run dev
   ```

6. **Check for Windows/Mac path issues:**
   - File names are case-sensitive in imports

**How to prevent it:**
- Keep dev server terminal visible
- Watch for compilation errors
- Use consistent file naming

---

### Component not updating

**Symptom:**
State changes but the UI doesn't reflect the update.

**How to fix it:**
1. **Check if you're mutating state:**
   ```javascript
   // Wrong - mutating array
   const [items, setItems] = useState([1, 2, 3]);
   items.push(4);  // Mutation!
   setItems(items);  // Same reference, no re-render

   // Right - create new array
   setItems([...items, 4]);
   ```

2. **Check if you're mutating objects:**
   ```javascript
   // Wrong
   const [user, setUser] = useState({ name: 'Alice' });
   user.name = 'Bob';  // Mutation!
   setUser(user);  // Same reference

   // Right
   setUser({ ...user, name: 'Bob' });
   ```

3. **Check nested objects:**
   ```javascript
   // Wrong
   const [data, setData] = useState({ user: { name: 'Alice' } });
   setData({ ...data, user: { name: 'Bob' } });  // Wait, this is right

   // But this is wrong
   data.user.name = 'Bob';
   setData({ ...data });  // Nested object same reference

   // Right - deep copy or use immer
   setData({
     ...data,
     user: { ...data.user, name: 'Bob' }
   });
   ```

4. **Verify state is actually changing:**
   ```javascript
   useEffect(() => {
     console.log('State changed:', state);
   }, [state]);
   ```

**How to prevent it:**
- Always create new objects/arrays when updating state
- Use immer library for complex state
- Install React Developer Tools to inspect state

---

## TypeScript Issues

### "Type X is not assignable to type Y"

**Error message:**
```
Type 'string' is not assignable to type 'number'.
Type 'User | undefined' is not assignable to type 'User'.
```

**What it means:**
You're trying to use a value of one type where another type is expected.

**How to fix it:**
1. **Check the types match:**
   ```typescript
   // Wrong
   const age: number = "25";  // Error!

   // Right
   const age: number = 25;
   // or
   const age: number = parseInt("25");
   ```

2. **Handle undefined:**
   ```typescript
   // Wrong
   function getUser(): User | undefined { }
   const user: User = getUser();  // Error!

   // Right - handle undefined case
   const user = getUser();
   if (user) {
     // user is User here
   }

   // Or assert if you're sure
   const user = getUser()!;  // Non-null assertion
   ```

3. **Check function return types:**
   ```typescript
   // Error - function must return number
   function add(a: number, b: number): number {
     return String(a + b);  // Returns string!
   }
   ```

**How to prevent it:**
- Let TypeScript infer types when possible
- Use strict mode in tsconfig
- Read error messages carefully - they tell you exactly what's wrong

---

### "Property does not exist on type"

**Error message:**
```
Property 'name' does not exist on type 'User'.
Property 'foo' does not exist on type '{}'.
```

**What it means:**
You're accessing a property that TypeScript doesn't know about.

**How to fix it:**
1. **Add the property to the type:**
   ```typescript
   // Type is missing 'name'
   interface User {
     id: number;
   }

   // Add it
   interface User {
     id: number;
     name: string;
   }
   ```

2. **Check for typos:**
   ```typescript
   interface User {
     name: string;
   }

   const user: User = { name: 'Alice' };
   console.log(user.nmae);  // Typo!
   ```

3. **Type API responses:**
   ```typescript
   // Don't use any
   const data: any = await fetch('/api').then(r => r.json());

   // Define the type
   interface ApiResponse {
     users: User[];
     total: number;
   }
   const data: ApiResponse = await fetch('/api').then(r => r.json());
   ```

4. **For dynamic properties:**
   ```typescript
   interface Config {
     [key: string]: string;  // Index signature
   }
   ```

**How to prevent it:**
- Define interfaces for all data structures
- Use TypeScript's auto-complete to avoid typos
- Type external data (API responses)

---

### "Object is possibly undefined"

**Error message:**
```
Object is possibly 'undefined'.
Cannot invoke an object which is possibly 'undefined'.
```

**What it means:**
TypeScript knows the value might be undefined, and you need to handle that case.

**How to fix it:**
1. **Use optional chaining:**
   ```typescript
   // Error
   const name = user.profile.name;

   // Fix
   const name = user?.profile?.name;
   ```

2. **Use nullish coalescing:**
   ```typescript
   // Provide default value
   const name = user?.name ?? 'Anonymous';
   ```

3. **Add a guard:**
   ```typescript
   if (user && user.profile) {
     console.log(user.profile.name);  // Safe
   }
   ```

4. **Non-null assertion (use carefully):**
   ```typescript
   // Only if you're SURE it's defined
   const name = user!.profile!.name;
   ```

5. **Array access:**
   ```typescript
   const items = [1, 2, 3];
   const first = items[0];  // number | undefined

   if (first !== undefined) {
     console.log(first * 2);  // Safe
   }
   ```

**How to prevent it:**
- Enable strict null checks
- Handle undefined at the boundaries (API, user input)
- Use sensible defaults

---

### tsconfig.json problems

**Common issues and fixes:**

**Module resolution errors:**
```json
{
  "compilerOptions": {
    "moduleResolution": "node",
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true
  }
}
```

**Path aliases not working:**
```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```
Note: You also need to configure your bundler (Vite, webpack) to understand these paths.

**JSX errors:**
```json
{
  "compilerOptions": {
    "jsx": "react-jsx"  // For React 17+
  }
}
```

**Strict mode (recommended):**
```json
{
  "compilerOptions": {
    "strict": true
  }
}
```

**Include/exclude files:**
```json
{
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

---

### Missing type declarations (@types packages)

**Error message:**
```
Could not find a declaration file for module 'lodash'.
'lodash' implicitly has an 'any' type.
```

**What it means:**
The package doesn't include TypeScript types, and you need to install them separately.

**How to fix it:**
1. **Install @types package:**
   ```bash
   npm install --save-dev @types/lodash
   ```

2. **Check if types exist:**
   ```bash
   npm search @types/package-name
   ```

3. **If no @types package exists, create a declaration:**
   ```typescript
   // src/types/lodash.d.ts
   declare module 'lodash' {
     export function chunk<T>(array: T[], size: number): T[][];
     // Add more as needed
   }
   ```

4. **Or use any (last resort):**
   ```typescript
   // @ts-ignore
   import something from 'untyped-package';
   ```

**How to prevent it:**
- Check for TypeScript support before choosing packages
- Many modern packages include types
- Keep @types packages in devDependencies

---

## Database / PostgreSQL Issues

### "Connection refused" (server not running)

**Error message:**
```
Error: connect ECONNREFUSED 127.0.0.1:5432
FATAL: Connection refused
```

**What it means:**
The PostgreSQL server isn't running.

**How to fix it:**

**macOS (Homebrew):**
```bash
# Start PostgreSQL
brew services start postgresql

# Check status
brew services list

# If that doesn't work, try
pg_ctl -D /usr/local/var/postgres start
```

**Linux:**
```bash
sudo systemctl start postgresql
sudo systemctl status postgresql
```

**Check if running:**
```bash
pg_isready
```

**How to prevent it:**
- Set PostgreSQL to start on boot: `brew services start postgresql`
- Add database startup to your dev environment checklist

---

### "FATAL: role does not exist"

**Error message:**
```
FATAL: role "username" does not exist
```

**What it means:**
The database user (role) you're trying to connect as doesn't exist.

**How to fix it:**
1. **Connect as default superuser:**
   ```bash
   # macOS typically uses your username
   psql postgres

   # Or try
   psql -U postgres postgres
   ```

2. **Create the role:**
   ```sql
   CREATE ROLE myuser WITH LOGIN PASSWORD 'mypassword';

   -- If you need superuser privileges (dev only!)
   ALTER ROLE myuser WITH SUPERUSER;
   ```

3. **Create role with createdb permission:**
   ```sql
   CREATE ROLE myuser WITH LOGIN PASSWORD 'mypassword' CREATEDB;
   ```

**How to prevent it:**
- Document required database setup for your project
- Use migration scripts that check for roles

---

### "FATAL: database does not exist"

**Error message:**
```
FATAL: database "myapp" does not exist
```

**What it means:**
The database you're trying to connect to doesn't exist.

**How to fix it:**
1. **List existing databases:**
   ```bash
   psql -l
   # or
   psql postgres -c "\l"
   ```

2. **Create the database:**
   ```bash
   createdb myapp

   # Or in psql
   psql postgres -c "CREATE DATABASE myapp;"

   # With owner
   psql postgres -c "CREATE DATABASE myapp OWNER myuser;"
   ```

3. **Check your connection string:**
   ```
   postgresql://user:password@localhost:5432/myapp
                                              ^^^^^
                                              database name
   ```

**How to prevent it:**
- Include database creation in setup scripts
- Document database setup in README

---

### Port 5432 already in use

**Error message:**
```
FATAL: could not bind to address 127.0.0.1:5432: Address already in use
```

**What it means:**
Something is already using PostgreSQL's default port.

**How to fix it:**
1. **Find what's using the port:**
   ```bash
   lsof -i :5432
   ```

2. **Kill the process:**
   ```bash
   # Get the PID from lsof output
   kill <PID>

   # Force kill if needed
   kill -9 <PID>
   ```

3. **Or stop existing PostgreSQL:**
   ```bash
   brew services stop postgresql
   ```

4. **Use a different port:**
   ```bash
   # Start on different port
   postgres -D /usr/local/var/postgres -p 5433

   # Connect on different port
   psql -p 5433 mydb
   ```

**How to prevent it:**
- Properly shut down PostgreSQL when not using it
- Don't run multiple PostgreSQL installations

---

### psql command not found

**Error message:**
```
zsh: command not found: psql
```

**What it means:**
PostgreSQL isn't installed or isn't in your PATH.

**How to fix it:**
1. **Install PostgreSQL:**
   ```bash
   # macOS
   brew install postgresql

   # After install
   brew services start postgresql
   ```

2. **Add to PATH (if installed but not found):**
   ```bash
   # Add to ~/.zshrc
   export PATH="/usr/local/opt/postgresql/bin:$PATH"

   # Reload
   source ~/.zshrc
   ```

3. **Check installation:**
   ```bash
   brew list postgresql
   which psql
   ```

**How to prevent it:**
- Use Homebrew for consistent installation
- Restart terminal after installation

---

## Express / API Issues

### "EADDRINUSE: Port already in use"

**Error message:**
```
Error: listen EADDRINUSE: address already in use :::3000
```

**What it means:**
Another process is using the port your server wants to use.

**How to fix it:**
1. **Find and kill the process:**
   ```bash
   # Find what's using port 3000
   lsof -i :3000

   # Kill it
   kill -9 <PID>
   ```

2. **Use a different port:**
   ```javascript
   const PORT = process.env.PORT || 3001;
   ```

3. **On macOS, AirPlay uses port 5000:**
   - System Preferences > Sharing > Disable AirPlay Receiver
   - Or use a different port

**How to prevent it:**
- Always stop servers properly (Ctrl+C)
- Use environment variables for ports
- Add port-finding utility to your app

---

### CORS errors

**Error message (browser console):**
```
Access to fetch at 'http://localhost:3000/api' from origin 'http://localhost:5173'
has been blocked by CORS policy
```

**What it means:**
The browser is blocking requests from your frontend to a different origin (domain/port).

**How to fix it:**
1. **Install and configure cors middleware:**
   ```bash
   npm install cors
   ```

   ```javascript
   const cors = require('cors');

   // Allow all origins (development only!)
   app.use(cors());

   // Or configure specific origins
   app.use(cors({
     origin: 'http://localhost:5173',
     credentials: true
   }));
   ```

2. **For production, be specific:**
   ```javascript
   const corsOptions = {
     origin: process.env.FRONTEND_URL,
     credentials: true,
     methods: ['GET', 'POST', 'PUT', 'DELETE']
   };
   app.use(cors(corsOptions));
   ```

3. **Check the order of middleware:**
   ```javascript
   // CORS must come before routes
   app.use(cors());
   app.use(express.json());
   app.use('/api', routes);
   ```

**How to prevent it:**
- Set up CORS at the start of your project
- Use environment variables for allowed origins
- Understand CORS is a browser security feature

---

### 404 on valid routes

**Error message:**
```
Cannot GET /api/users
404 Not Found
```

**What it means:**
Express can't find a route handler for the requested path.

**How to fix it:**
1. **Check route path matches:**
   ```javascript
   // If you access /api/users, you need:
   app.get('/api/users', handler);

   // Not:
   app.get('/users', handler);  // Missing /api prefix
   ```

2. **Check route order:**
   ```javascript
   // Wrong - wildcard catches everything
   app.get('*', (req, res) => res.sendFile('index.html'));
   app.get('/api/users', handler);  // Never reached!

   // Right - specific routes first
   app.get('/api/users', handler);
   app.get('*', (req, res) => res.sendFile('index.html'));
   ```

3. **Check router mounting:**
   ```javascript
   // router.js
   router.get('/users', handler);

   // app.js
   app.use('/api', router);  // Routes are at /api/users
   ```

4. **Debug routes:**
   ```javascript
   app.use((req, res, next) => {
     console.log(`${req.method} ${req.path}`);
     next();
   });
   ```

**How to prevent it:**
- Keep route structure simple and documented
- Use consistent naming conventions
- Add logging middleware

---

### "Cannot GET /"

**Error message:**
```
Cannot GET /
```

**What it means:**
No route handler exists for the root path.

**How to fix it:**
1. **Add a root route:**
   ```javascript
   app.get('/', (req, res) => {
     res.json({ message: 'API is running' });
   });
   ```

2. **For SPA with client-side routing:**
   ```javascript
   // Serve static files
   app.use(express.static('dist'));

   // Handle client-side routes
   app.get('*', (req, res) => {
     res.sendFile(path.join(__dirname, 'dist', 'index.html'));
   });
   ```

3. **Check if server is running on expected port:**
   ```javascript
   app.listen(PORT, () => {
     console.log(`Server running on http://localhost:${PORT}`);
   });
   ```

---

### Request body undefined (missing middleware)

**Error message:**
```
TypeError: Cannot read property 'name' of undefined
// When accessing req.body.name
```

**What it means:**
Express isn't parsing the request body. You need body-parsing middleware.

**How to fix it:**
1. **Add body parsing middleware:**
   ```javascript
   // For JSON bodies
   app.use(express.json());

   // For URL-encoded forms
   app.use(express.urlencoded({ extended: true }));
   ```

2. **Make sure middleware is before routes:**
   ```javascript
   // Middleware first
   app.use(express.json());

   // Then routes
   app.post('/api/users', (req, res) => {
     console.log(req.body);  // Now works!
   });
   ```

3. **Check Content-Type header:**
   ```javascript
   // Client must send correct header
   fetch('/api/users', {
     method: 'POST',
     headers: {
       'Content-Type': 'application/json'
     },
     body: JSON.stringify({ name: 'Alice' })
   });
   ```

**How to prevent it:**
- Add body parsing middleware at the start of every Express app
- Create a boilerplate with common middleware

---

### JWT errors

**Common JWT errors and fixes:**

**"jwt malformed":**
```javascript
// Token is not valid JWT format
// Check you're sending just the token, not "Bearer token"
const token = authHeader.split(' ')[1];  // Extract token
```

**"jwt expired":**
```javascript
// Token has expired
// Either refresh the token or have user log in again

// When creating token, set appropriate expiry
jwt.sign(payload, secret, { expiresIn: '7d' });
```

**"invalid signature":**
```javascript
// Secret used to sign doesn't match secret used to verify
// Make sure JWT_SECRET is the same everywhere

// Wrong
jwt.sign(payload, 'secret1');
jwt.verify(token, 'secret2');  // Different secrets!

// Right - use environment variable
jwt.sign(payload, process.env.JWT_SECRET);
jwt.verify(token, process.env.JWT_SECRET);
```

**"jwt must be provided":**
```javascript
// Token is undefined or empty
// Check the Authorization header exists

const token = req.headers.authorization?.split(' ')[1];
if (!token) {
  return res.status(401).json({ error: 'No token provided' });
}
```

---

## Deployment Issues

### Build failures (Vercel, Railway)

**Common causes and fixes:**

**TypeScript errors:**
```bash
# Build fails due to type errors
# Fix all TypeScript errors locally first
npm run build

# Check for unused variables, implicit any, etc.
```

**Missing dependencies:**
```bash
# Check if all dependencies are in package.json
# Not devDependencies for runtime needs
npm install package-name --save
```

**Different Node version:**
```json
// package.json - specify Node version
{
  "engines": {
    "node": ">=18.0.0"
  }
}
```

**Case sensitivity:**
```javascript
// Local (macOS) is case-insensitive
// Linux servers are case-sensitive
import Component from './component';  // Fails if file is Component.js
```

**Environment variables:**
```bash
# Make sure all required env vars are set in deployment platform
# Don't commit .env files - set them in the platform's UI
```

---

### Environment variables not working

**Common issues:**

**Variable not defined:**
```javascript
// Check if variable exists
console.log('DB_URL:', process.env.DATABASE_URL);

// Provide fallback
const dbUrl = process.env.DATABASE_URL || 'default-url';
```

**Wrong variable name:**
```javascript
// In Vercel/Railway UI: DATABASE_URL
// In code: process.env.DATABASE_URL (exact match!)
```

**Frontend vs Backend:**
```javascript
// Vite: Must prefix with VITE_
// process.env.API_URL  <- won't work in frontend
// import.meta.env.VITE_API_URL  <- correct

// Next.js: Must prefix with NEXT_PUBLIC_ for client
// process.env.NEXT_PUBLIC_API_URL
```

**Not restarting after changes:**
```bash
# After changing env vars, restart the deployment
# Vercel: Redeploy
# Railway: Redeploy or restart
```

**How to debug:**
```javascript
// Temporarily log env vars (remove before production!)
console.log('Environment:', {
  nodeEnv: process.env.NODE_ENV,
  hasDbUrl: !!process.env.DATABASE_URL
});
```

---

### "Application error" on deployed site

**How to debug:**

1. **Check deployment logs:**
   - Vercel: Deployment > Functions > View Logs
   - Railway: Deployments > View Logs
   - Heroku: `heroku logs --tail`

2. **Common causes:**
   - Missing environment variables
   - Database connection issues
   - Build succeeded but runtime error
   - Port binding issues

3. **Check if server binds to correct port:**
   ```javascript
   // Use the provided PORT
   const PORT = process.env.PORT || 3000;

   // Bind to 0.0.0.0, not just localhost
   app.listen(PORT, '0.0.0.0', () => {
     console.log(`Server running on port ${PORT}`);
   });
   ```

4. **Add health check endpoint:**
   ```javascript
   app.get('/health', (req, res) => {
     res.json({ status: 'ok', timestamp: new Date() });
   });
   ```

---

### Database connection in production

**Common issues:**

**Connection string format:**
```javascript
// Development
postgresql://user:password@localhost:5432/dbname

// Production (with SSL)
postgresql://user:password@host:5432/dbname?sslmode=require
```

**SSL required:**
```javascript
// Most production databases require SSL
const pool = new Pool({
  connectionString: process.env.DATABASE_URL,
  ssl: process.env.NODE_ENV === 'production'
    ? { rejectUnauthorized: false }
    : false
});
```

**Connection pooling:**
```javascript
// Don't create new connections on every request
// Use connection pooling
const pool = new Pool({
  connectionString: process.env.DATABASE_URL,
  max: 20,  // Maximum pool size
});
```

**Prisma specific:**
```javascript
// schema.prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

// For serverless (Vercel, etc.)
// Add connection pooling via Prisma Data Proxy
// or use ?connection_limit=1&pool_timeout=20
```

**Testing connection:**
```javascript
// Add connection test on startup
pool.query('SELECT NOW()', (err, res) => {
  if (err) {
    console.error('Database connection failed:', err);
    process.exit(1);
  }
  console.log('Database connected:', res.rows[0].now);
});
```

---

## Quick Reference: Diagnostic Commands

```bash
# System
which <command>       # Find command location
echo $PATH           # Show PATH
env                  # Show all environment variables

# Node/npm
node --version       # Node version
npm --version        # npm version
npm ls               # List installed packages
npm ls <package>     # Check specific package

# nvm
nvm current          # Current Node version
nvm ls               # Installed versions
nvm use <version>    # Switch version

# Git
git status           # Repository status
git log --oneline    # Recent commits
git branch -a        # All branches
git remote -v        # Remote URLs

# Processes
lsof -i :<port>      # What's using a port
ps aux | grep node   # Find Node processes
kill -9 <PID>        # Force kill process

# PostgreSQL
pg_isready           # Check if running
psql -l              # List databases
brew services list   # Service status (macOS)
```

---

## When All Else Fails

1. **Read the error message carefully** - it usually tells you exactly what's wrong
2. **Google the exact error message** - someone has seen it before
3. **Check the documentation** - often has troubleshooting sections
4. **Look at GitHub Issues** - for package-specific problems
5. **Simplify and isolate** - create a minimal reproduction
6. **Ask for help** - with error message, what you tried, and minimal code

Remember: Every developer encounters these errors. The skill is learning to debug them systematically.
