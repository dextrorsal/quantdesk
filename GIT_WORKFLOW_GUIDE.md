# 🚀 QuantDesk Git Workflow Guide

## 📚 Table of Contents
1. [Git Basics](#git-basics)
2. [Branch Strategy](#branch-strategy)
3. [Commit Best Practices](#commit-best-practices)
4. [Pull Request Workflow](#pull-request-workflow)
5. [Security & Privacy](#security--privacy)
6. [GitHub Features](#github-features)
7. [Dependabot Management](#dependabot-management)
8. [Troubleshooting](#troubleshooting)

---

## 🔧 Git Basics

### **What is Git?**
Git is a **version control system** - think of it as a super-powered save system for your code that:
- Tracks every change you make
- Allows you to go back to any previous version
- Enables collaboration with others
- Provides a complete history of your project

### **Core Concepts**

#### **Repository (Repo)**
Your project folder with complete version history
```bash
/home/dex/Desktop/quantdesk/  # This is your repository
```

#### **Commits**
Snapshots of your code at specific moments in time
```bash
git commit -m "feat: add cross-collateralization system"
# Creates a snapshot with message "feat: add cross-collateralization system"
```

#### **Branches**
Different versions/experiments of your code
```bash
main          # Production-ready code
develop       # Integration branch
feature/xyz   # Individual feature development
hotfix/xyz    # Emergency fixes
```

#### **Remote (GitHub)**
Cloud backup + collaboration platform
```bash
origin/main   # Your code stored on GitHub
```

---

## 🌿 Branch Strategy

### **Professional Branch Structure**

```
main (production)
  ↑
develop (integration)
  ↑
feature/cross-collateral
feature/advanced-orders
feature/mobile-docs
hotfix/security-update
```

### **Branch Types**

#### **1. Main Branch**
- **Purpose**: Production-ready code
- **Protection**: Requires PRs for changes
- **Deployment**: Automatically deploys to production

#### **2. Develop Branch**
- **Purpose**: Integration branch for features
- **Usage**: Merge feature branches here first
- **Testing**: Integration testing happens here

#### **3. Feature Branches**
- **Naming**: `feature/description`
- **Examples**: 
  - `feature/cross-collateral`
  - `feature/oracle-integration`
  - `feature/mobile-ui`

#### **4. Hotfix Branches**
- **Naming**: `hotfix/description`
- **Purpose**: Emergency fixes for production
- **Examples**: `hotfix/security-patch`, `hotfix/critical-bug`

### **Branch Workflow Commands**

```bash
# Create and switch to new feature branch
git checkout -b feature/new-feature

# Switch between branches
git checkout main
git checkout develop
git checkout feature/new-feature

# List all branches
git branch -a

# Delete local branch
git branch -d feature/old-feature

# Delete remote branch
git push origin --delete feature/old-feature
```

---

## 📝 Commit Best Practices

### **Commit Message Format**

```
type(scope): description

feat: add cross-collateralization system
fix: resolve compilation errors in smart contract
docs: add comprehensive README for advanced features
refactor: optimize smart contract gas usage
test: add unit tests for liquidation logic
chore: update dependencies
```

### **Commit Types**

| Type | Description | Example |
|------|-------------|---------|
| **feat** | New features | `feat: add JIT liquidity system` |
| **fix** | Bug fixes | `fix: resolve PDA derivation error` |
| **docs** | Documentation | `docs: add API documentation` |
| **refactor** | Code improvements | `refactor: optimize gas usage` |
| **test** | Testing | `test: add integration tests` |
| **chore** | Maintenance | `chore: update dependencies` |
| **perf** | Performance | `perf: optimize oracle price updates` |
| **ci** | CI/CD | `ci: add automated testing` |

### **Commit Workflow**

```bash
# 1. Check status
git status

# 2. Stage changes
git add .                    # Stage all changes
git add specific-file.js     # Stage specific file
git add src/                 # Stage entire directory

# 3. Commit with message
git commit -m "feat: add cross-collateralization system"

# 4. Push to remote
git push origin feature/cross-collateral
```

### **Good vs Bad Commit Messages**

#### ✅ **Good Examples**
```
feat: add cross-collateralization system
fix: resolve compilation errors in smart contract
docs: add comprehensive README for advanced features
refactor: optimize smart contract gas usage
test: add unit tests for liquidation logic
```

#### ❌ **Bad Examples**
```
fixed stuff
update
changes
work in progress
asdf
```

---

## 🔄 Pull Request Workflow

### **Complete PR Workflow**

#### **1. Create Feature Branch**
```bash
# Start from main branch
git checkout main
git pull origin main

# Create feature branch
git checkout -b feature/oracle-integration
```

#### **2. Work on Feature**
```bash
# Make changes to code
# ... edit files ...

# Stage and commit changes
git add .
git commit -m "feat: integrate Pyth oracle feeds"

# Push branch to GitHub
git push origin feature/oracle-integration
```

#### **3. Create Pull Request**
1. Go to GitHub website
2. Click "Compare & pull request"
3. Fill out PR description:
   ```markdown
   ## 🚀 Feature: Oracle Integration
   
   ### What Changed
   - Integrated Pyth Network oracle feeds
   - Added price validation logic
   - Implemented staleness checks
   
   ### Testing
   - [ ] Unit tests pass
   - [ ] Integration tests pass
   - [ ] Manual testing completed
   
   ### Security
   - [ ] No sensitive data exposed
   - [ ] Input validation added
   - [ ] Error handling implemented
   ```

#### **4. Code Review Process**
- **Reviewer**: Checks code quality, security, performance
- **Approval**: Required before merging
- **Comments**: Discussion and feedback
- **Changes**: Address feedback and update PR

#### **5. Merge to Main**
```bash
# After PR approval, merge via GitHub UI
# Or merge locally:
git checkout main
git pull origin main
git merge feature/oracle-integration
git push origin main
```

### **PR Best Practices**

#### **PR Description Template**
```markdown
## 🚀 Feature: [Feature Name]

### 📋 What Changed
- [ ] Added new functionality
- [ ] Fixed existing bugs
- [ ] Updated documentation

### 🧪 Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing completed
- [ ] Edge cases tested

### 🔒 Security
- [ ] No sensitive data exposed
- [ ] Input validation added
- [ ] Error handling implemented
- [ ] Security review completed

### 📚 Documentation
- [ ] Code comments added
- [ ] README updated
- [ ] API docs updated

### 🚀 Deployment
- [ ] No breaking changes
- [ ] Database migrations (if needed)
- [ ] Environment variables (if needed)
```

---

## 🔒 Security & Privacy

### **What's Protected (.gitignore)**

#### **Never Commit These Files:**
```bash
# Environment variables
.env
.env.local
.env.production

# Private keys
*.key
*.pem
wallet.json
id.json

# Sensitive source code
/backend/src/
/frontend/src/
/contracts/smart-contracts/programs/
/admin-dashboard/src/

# Build outputs
dist/
build/
target/

# Logs
*.log
logs/
```

#### **Safe to Commit:**
```bash
# Documentation
*.md
docs/

# Configuration templates
.env.example
package.json

# Scripts
*.sh
scripts/

# Public configs
docker-compose.yml
Dockerfile
```

### **Security Checklist**

#### **Before Every Commit:**
- [ ] No `.env` files included
- [ ] No private keys included
- [ ] No sensitive data exposed
- [ ] No hardcoded secrets
- [ ] No debug logs with sensitive info

#### **Before Every PR:**
- [ ] Security review completed
- [ ] Input validation added
- [ ] Error handling implemented
- [ ] No SQL injection risks
- [ ] No XSS vulnerabilities

---

## 🚀 GitHub Features

### **1. Issues & Project Management**

#### **Creating Issues**
```markdown
## 🐛 Bug Report: [Title]

### Description
Clear description of the bug

### Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. See error

### Expected Behavior
What should happen

### Actual Behavior
What actually happens

### Environment
- OS: [e.g., Ubuntu 20.04]
- Browser: [e.g., Chrome 91]
- Version: [e.g., 1.0.0]
```

#### **Issue Labels**
- `bug`: Something isn't working
- `enhancement`: New feature or request
- `documentation`: Improvements to documentation
- `good first issue`: Good for newcomers
- `help wanted`: Extra attention needed
- `priority: high`: High priority
- `priority: low`: Low priority

### **2. Projects & Milestones**

#### **Project Boards**
- **To Do**: Planned work
- **In Progress**: Currently being worked on
- **Review**: Ready for review
- **Done**: Completed

#### **Milestones**
- **v1.0.0**: Initial release
- **v1.1.0**: Feature release
- **v1.1.1**: Bug fix release

### **3. Branch Protection Rules**

#### **Main Branch Protection**
- Require pull request reviews
- Require status checks to pass
- Require branches to be up to date
- Restrict pushes to main branch

---

## 🤖 Dependabot Management

### **What is Dependabot?**
Dependabot automatically creates PRs to update your dependencies when security vulnerabilities are found.

### **Dependabot PR Types**

#### **Security Updates (High Priority)**
```bash
# These should be merged quickly
dependabot/npm_and_yarn/package-name-version
```

#### **Version Updates (Lower Priority)**
```bash
# These can be reviewed and merged when convenient
dependabot/npm_and_yarn/package-name-version
```

### **Handling Dependabot PRs**

#### **1. Review the PR**
- Check what changed
- Verify it's safe to update
- Look for breaking changes

#### **2. Test the Changes**
```bash
# Checkout the Dependabot branch
git checkout dependabot/npm_and_yarn/package-name-version

# Install dependencies
npm install

# Run tests
npm test

# Build project
npm run build
```

#### **3. Merge or Close**
- **Merge**: If everything works
- **Close**: If there are issues
- **Comment**: Ask questions if unsure

### **Dependabot Configuration**

#### **Create `.github/dependabot.yml`**
```yaml
version: 2
updates:
  # Enable version updates for npm
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 10

  # Enable version updates for Docker
  - package-ecosystem: "docker"
    directory: "/"
    schedule:
      interval: "weekly"

  # Enable version updates for GitHub Actions
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
```

---

## 🛠️ Troubleshooting

### **Common Git Issues**

#### **1. Merge Conflicts**
```bash
# When you see merge conflicts
git status                    # See conflicted files
# Edit files to resolve conflicts
git add resolved-file.js      # Stage resolved files
git commit -m "resolve merge conflicts"
```

#### **2. Accidentally Committed Sensitive Data**
```bash
# Remove file from history
git filter-branch --force --index-filter \
  'git rm --cached --ignore-unmatch sensitive-file.txt' \
  --prune-empty --tag-name-filter cat -- --all

# Force push to update remote
git push origin --force --all
```

#### **3. Wrong Branch**
```bash
# Move last commit to different branch
git log --oneline -1          # Get commit hash
git reset --hard HEAD~1       # Remove from current branch
git checkout correct-branch   # Switch to correct branch
git cherry-pick commit-hash  # Apply commit to correct branch
```

#### **4. Undo Last Commit**
```bash
# Undo commit but keep changes
git reset --soft HEAD~1

# Undo commit and discard changes
git reset --hard HEAD~1
```

### **Git Aliases (Time Savers)**

#### **Add to `.gitconfig`**
```bash
[alias]
    st = status
    co = checkout
    br = branch
    ci = commit
    unstage = reset HEAD --
    last = log -1 HEAD
    visual = !gitk
    lg = log --oneline --decorate --graph --all
```

---

## 📊 Git Workflow Summary

### **Daily Workflow**
```bash
# 1. Start work
git checkout main
git pull origin main
git checkout -b feature/new-feature

# 2. Work on feature
# ... make changes ...
git add .
git commit -m "feat: add new feature"

# 3. Push and create PR
git push origin feature/new-feature
# Create PR on GitHub

# 4. After review and approval
git checkout main
git pull origin main
git branch -d feature/new-feature
```

### **Weekly Workflow**
```bash
# 1. Review Dependabot PRs
# 2. Update dependencies
# 3. Review and merge approved PRs
# 4. Clean up old branches
git branch -d feature/old-feature
```

### **Release Workflow**
```bash
# 1. Create release branch
git checkout -b release/v1.0.0

# 2. Final testing and bug fixes
# 3. Tag release
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0

# 4. Merge to main
git checkout main
git merge release/v1.0.0
git push origin main
```

---

## 🎯 Best Practices Summary

### **Do's**
- ✅ Use descriptive commit messages
- ✅ Create feature branches for new work
- ✅ Review code before merging
- ✅ Keep commits small and focused
- ✅ Test before pushing
- ✅ Use PRs for main branch changes
- ✅ Keep sensitive data out of commits

### **Don'ts**
- ❌ Commit directly to main branch
- ❌ Use vague commit messages
- ❌ Commit sensitive data
- ❌ Force push to shared branches
- ❌ Ignore Dependabot security updates
- ❌ Merge without review
- ❌ Leave branches unmerged

---

## 🔗 Resources

### **Git Documentation**
- [Official Git Documentation](https://git-scm.com/doc)
- [GitHub Documentation](https://docs.github.com)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)

### **Tools**
- [GitHub Desktop](https://desktop.github.com) - GUI for Git
- [GitKraken](https://www.gitkraken.com) - Advanced Git GUI
- [VS Code Git Integration](https://code.visualstudio.com/docs/editor/versioncontrol)

### **Learning**
- [Learn Git Branching](https://learngitbranching.js.org) - Interactive Git tutorial
- [GitHub Learning Lab](https://lab.github.com) - Hands-on Git training

---

**🎉 Congratulations!** You now have a complete understanding of professional Git workflow for QuantDesk development! 🚀
