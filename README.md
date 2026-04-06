# Quantum Viper GitHub Action

**Automated Security Scanning for GitHub CI/CD** — by [Quantum Tiger](https://quantumviper.com)

[![Version](https://img.shields.io/badge/version-4.0.0-blue.svg)](https://github.com/chiragnahata/Quantum-Viper)

---

## Quick Start

```yaml
name: Security Scan
on: [push, pull_request]

jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: quantumtiger/quantum-viper-action@v4
        with:
          scan-type: static
          fail-on-critical: true
```

## Inputs

| Input | Default | Description |
|-------|---------|-------------|
| `scan-type` | `static` | Scan type: `static`, `web-scan`, `ai-scan`, `sca`, `secrets`, `iac` |
| `path` | `.` | Path to scan |
| `language` | auto-detect | Target language |
| `fail-on-critical` | `false` | Fail workflow on critical findings |
| `fail-threshold` | — | Minimum severity to fail: `low`, `medium`, `high`, `critical` |
| `sarif-output` | `true` | Generate SARIF report |
| `baseline` | — | Path to `.quantumviper-baseline.json` |
| `api-key` | — | Quantum Viper API key (for cloud features) |
| `slack-webhook` | — | Slack notification webhook URL |
| `sbom-upload` | `false` | Upload SBOM as artifact |

## Outputs

| Output | Description |
|--------|-------------|
| `vulnerability-count` | Total vulnerabilities found |
| `critical-count` | Critical severity count |
| `security-score` | A-F security grade |
| `sarif-file` | Path to SARIF report |

## Examples

### PR Security Gate
```yaml
- uses: quantumtiger/quantum-viper-action@v4
  with:
    scan-type: static
    fail-on-critical: true
    sarif-output: true

- uses: github/codeql-action/upload-sarif@v3
  with:
    sarif_file: quantum-viper-results.sarif
```

### Multi-Scan Pipeline
```yaml
- uses: quantumtiger/quantum-viper-action@v4
  with:
    scan-type: static

- uses: quantumtiger/quantum-viper-action@v4
  with:
    scan-type: sca

- uses: quantumtiger/quantum-viper-action@v4
  with:
    scan-type: secrets
```

### Baseline Suppression
```yaml
- uses: quantumtiger/quantum-viper-action@v4
  with:
    scan-type: static
    baseline: .quantumviper-baseline.json
```

### Slack Notifications
```yaml
- uses: quantumtiger/quantum-viper-action@v4
  with:
    scan-type: static
    slack-webhook: ${{ secrets.SLACK_WEBHOOK }}
```

## Migration from v3

```yaml
# Old (v3)
- uses: quantumviper/quantum-viper-action@v3

# New (v4)
- uses: quantumtiger/quantum-viper-action@v4
```

## License

Proprietary — © 2025-2026 Quantum Tiger. All rights reserved.
