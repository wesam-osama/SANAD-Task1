SANAD Training Service — CI Pipeline Documentation
Objective: Establish an automated DevSecOps CI Pipeline for SANAD training services covering secrets detection, security vulnerability checks, and automated unit testing with isolated database execution.

Pipeline Configuration (.github/workflows/ci-pipeline.yml):

Secrets Detection Job: Executes Gitleaks to scan commit history and codebase for exposed hardcoded tokens, secret keys, or passwords.

Dependency & Security Checks Job: Uses NPM Audit to detect direct package vulnerabilities and Trivy to perform filesystem vulnerability analysis on high/critical security risks.

Automated Testing Job: Spins up a dedicated MongoDB container service (mongo:6.0) within the GitHub Actions runner, executes Jest unit/integration tests (npm test), and automatically archives coverage reports as pipeline artifacts upon completion.

Pipeline Execution Result: All security checks, dependency audits, and test suites completed successfully with zero leaks and 100% pass status.
