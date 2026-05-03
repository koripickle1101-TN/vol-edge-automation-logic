# Newcomer Guide

## 1) Objective
Create a complete, beginner friendly setup that covers GitHub CLI installation and a production safe branch ruleset for the main branch.

## 2) Step by step execution

Step 1: Install GitHub CLI from official source
- Use official packages from cli.github.com.
- Verify package signing keys before install.

Step 2: Validate GitHub CLI access
- Run gh --version.
- Run gh auth login.
- Run gh repo view.

Step 3: Create a new branch ruleset in repository settings
- Open Settings, then Rulesets, then New branch ruleset.
- Set Ruleset Name to protect-main-v1.
- Set Enforcement status to Active.
- Keep Bypass list empty.

Step 4: Configure target branches
- In Target branches, click Add target.
- Set Branch targeting criteria to main.
- Confirm branch targeting is configured.

Step 5: Apply required branch rules
Turn on these rules:
- Restrict deletions
- Require a pull request before merging
- Require status checks to pass if CI exists
- Block force pushes

Set pull request approvals to minimum 1.

Leave these rules off for a minimal baseline:
- Restrict creations
- Restrict updates
- Require linear history
- Require deployments to succeed
- Require signed commits
- Require code scanning results
- Require code quality results
- Automatically request Copilot code review

Step 6: Validate policy behavior
- Try direct push to main and confirm it is blocked by policy.
- Open a pull request from a feature branch and confirm merge path works.

## 3) Tools (free only)
- GitHub CLI
- GitHub repository settings page
- Git
- Bash shell

## 4) Copy paste output

Ruleset Name: protect-main-v1
Enforcement status: Active
Bypass list: empty
Target branches:
- Branch targeting criteria: main

Rules ON:
- Restrict deletions
- Require a pull request before merging
- Required approvals: 1
- Require status checks to pass: ON if CI exists
- Block force pushes

Rules OFF:
- Restrict creations
- Restrict updates
- Require linear history
- Require deployments to succeed
- Require signed commits
- Require code scanning results
- Require code quality results
- Automatically request Copilot code review

CLI setup checks:
- gh --version
- gh auth login
- gh repo view

## 5) Expected result
- Every contributor can install and use GitHub CLI quickly.
- Main branch has a reproducible and safe protection baseline.
- Team uses pull request workflow by default and can scale collaboration safely.
