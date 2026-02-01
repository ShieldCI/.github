# 🔐 Administrator Setup Checklist

This checklist is for repository administrators to complete the GitHub Actions and branch protection setup.

## ✅ Pre-Setup Verification

- [ ] All workflow files are committed to the repository
- [ ] Workflows are in `.github/workflows/` directory
- [ ] YAML syntax is valid (no syntax errors)
- [ ] Repository has GitHub Actions enabled

## 🔧 GitHub Repository Settings

### 1. Enable GitHub Actions

- [ ] Go to **Settings** → **Actions** → **General**
- [ ] Select **Allow all actions and reusable workflows**
- [ ] Enable **Read and write permissions** for workflows
- [ ] Save changes

### 2. Configure Branch Protection

- [ ] Go to **Settings** → **Branches**
- [ ] Click **Add branch protection rule**
- [ ] Branch name pattern: `master` (or `main`)

#### Protection Settings

**Protect matching branches:**

- [ ] ✅ **Require a pull request before merging**
  - [ ] Required number of approvals: `1` (or more)
  - [ ] ✅ Dismiss stale pull request approvals when new commits are pushed
  - [ ] ✅ Require review from Code Owners (if teams are set up)
  - [ ] ❌ Allow specified actors to bypass required pull requests (leave unchecked)

- [ ] ✅ **Require status checks to pass before merging**
  - [ ] ✅ Require branches to be up to date before merging
  - [ ] **Select required status checks** (after first workflow run):
    - [ ] `analyzers-core / Analyzers Core Tests`
    - [ ] `laravel-package / Laravel Package Tests (8.1, 9.*)`
    - [ ] `laravel-package / Laravel Package Tests (8.2, 9.*)`
    - [ ] `laravel-package / Laravel Package Tests (8.2, 10.*)`
    - [ ] `laravel-package / Laravel Package Tests (8.2, 11.*)`
    - [ ] `laravel-package / Laravel Package Tests (8.3, 9.*)`
    - [ ] `laravel-package / Laravel Package Tests (8.3, 10.*)`
    - [ ] `laravel-package / Laravel Package Tests (8.3, 11.*)`
    - [ ] `example-app / Example App Tests`

- [ ] ✅ **Require conversation resolution before merging**

- [ ] ✅ **Require signed commits** (optional, recommended)

- [ ] ✅ **Require linear history** (optional, recommended)

- [ ] ✅ **Do not allow bypassing the above settings**
  - Note: This prevents even admins from bypassing rules

- [ ] ❌ **Allow force pushes** (keep disabled)
  - Ensure this is **unchecked**

- [ ] ❌ **Allow deletions** (keep disabled)
  - Ensure this is **unchecked**

- [ ] Click **Create** or **Save changes**

### 3. Create GitHub Teams (Optional)

If using CODEOWNERS for automatic reviewer assignment:

- [ ] Go to **Settings** → **Collaborators and teams**
- [ ] Create the following teams:
  - [ ] `@shieldci/core-team` - Core maintainers
  - [ ] `@shieldci/analyzers-team` - Analyzer specialists
  - [ ] `@shieldci/laravel-team` - Laravel specialists
  - [ ] `@shieldci/security-team` - Security experts
  - [ ] `@shieldci/performance-team` - Performance experts
  - [ ] `@shieldci/docs-team` - Documentation writers
  - [ ] `@shieldci/devops-team` - DevOps/CI specialists
  - [ ] `@shieldci/leadership-team` - Project leadership

- [ ] Add team members to each team
- [ ] Set appropriate permissions for each team

### 4. Configure Codecov (Optional)

For code coverage reporting:

- [ ] Go to [codecov.io](https://codecov.io)
- [ ] Sign in with GitHub
- [ ] Click **Add new repository**
- [ ] Select **shieldci/shieldci**
- [ ] Copy the upload token (if private repo)
- [ ] Go to GitHub: **Settings** → **Secrets and variables** → **Actions**
- [ ] Click **New repository secret**
- [ ] Name: `CODECOV_TOKEN`
- [ ] Value: Paste the token from Codecov
- [ ] Click **Add secret**

### 5. Configure Repository Secrets (If Needed)

- [ ] Go to **Settings** → **Secrets and variables** → **Actions**
- [ ] Add any required secrets:
  - [ ] `CODECOV_TOKEN` (if using Codecov)
  - [ ] Any other API keys or tokens needed

## 🧪 Testing the Setup

### Test 1: Trigger Initial Workflow Run

- [ ] Create a test branch:
  ```bash
  git checkout -b test/initial-workflow-run
  echo "# Test" >> TEST.md
  git add TEST.md
  git commit -m "test: trigger initial workflow run"
  git push origin test/initial-workflow-run
  ```

- [ ] Go to **Actions** tab on GitHub
- [ ] Verify workflows are running
- [ ] Wait for all jobs to complete
- [ ] Verify all jobs pass (green checkmarks)

### Test 2: Create Test Pull Request

- [ ] Create a PR from the test branch to master
- [ ] Verify:
  - [ ] Workflows run automatically
  - [ ] All status checks appear
  - [ ] PR template is displayed
  - [ ] Code owners are assigned (if teams set up)
  - [ ] Merge button is disabled until checks pass

### Test 3: Verify Branch Protection

- [ ] Try to push directly to master (should fail):
  ```bash
  git checkout master
  echo "test" >> TEST.md
  git add TEST.md
  git commit -m "test: direct push"
  git push origin master
  ```
- [ ] Verify push is rejected with branch protection message

### Test 4: Complete PR Merge

- [ ] Approve the test PR
- [ ] Verify merge button becomes enabled
- [ ] Merge the PR
- [ ] Delete the test branch
- [ ] Delete `TEST.md` file

## 📊 Monitoring & Maintenance

### Regular Checks

- [ ] Monitor workflow success rate (target: >95%)
- [ ] Review failed builds weekly
- [ ] Update workflow dependencies quarterly
- [ ] Review and update branch protection rules as needed

### Workflow Maintenance

- [ ] Update PHP versions when new versions are released
- [ ] Update Laravel versions when new versions are released
- [ ] Update GitHub Actions versions when updates are available
- [ ] Review and optimize slow-running jobs

### Documentation Updates

- [ ] Update `.github/WORKFLOWS_SETUP.md` when workflows change
- [ ] Update `.github/CONTRIBUTING.md` when processes change
- [ ] Keep `.github/QUICK_REFERENCE.md` current

## 🚨 Troubleshooting

### Workflows Not Running

- [ ] Check if GitHub Actions is enabled
- [ ] Verify workflow files are in correct location
- [ ] Check YAML syntax with online validator
- [ ] Review workflow logs for errors

### Status Checks Not Appearing

- [ ] Workflows must run at least once before appearing
- [ ] Check workflow names match exactly
- [ ] Verify branch protection is looking for correct job names

### Tests Failing

- [ ] Review test logs in Actions tab
- [ ] Check for dependency issues
- [ ] Verify PHP/Laravel version compatibility
- [ ] Test locally to reproduce

### Branch Protection Not Working

- [ ] Verify rule is saved correctly
- [ ] Check branch name pattern matches
- [ ] Ensure "Do not allow bypassing" is enabled
- [ ] Test with a non-admin account

## 📞 Support Contacts

| Issue Type | Contact |
|------------|---------|
| Workflow Configuration | DevOps Team |
| Branch Protection | Repository Admin |
| Test Failures | Development Team |
| Codecov Issues | DevOps Team |
| General Questions | support@shieldci.com |

## ✅ Final Verification

Before marking setup as complete:

- [ ] All workflows run successfully
- [ ] Branch protection is active and tested
- [ ] Status checks are required
- [ ] PR template is working
- [ ] Code owners are assigned (if applicable)
- [ ] Team has been notified of new workflow
- [ ] Documentation is accessible to team
- [ ] Test PR completed successfully

## 📝 Sign-Off

**Setup Completed By**: ___________________________

**Date**: ___________________________

**Verified By**: ___________________________

**Date**: ___________________________

**Notes**:
```
[Add any notes about the setup, customizations, or issues encountered]
```

---

## 🎉 Setup Complete!

Once all items are checked, the repository is fully configured with:

- ✅ Automated testing on every push
- ✅ Code quality enforcement
- ✅ Branch protection preventing direct pushes
- ✅ Required status checks before merge
- ✅ PR templates and issue templates
- ✅ Automatic reviewer assignment
- ✅ Comprehensive documentation

**The repository is now production-ready! 🚀**

---

**Document Version**: 1.0  
**Last Updated**: December 9, 2025  
**Next Review**: March 2026

