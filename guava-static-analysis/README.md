# Guava Static Analysis (Dockerized)

Reproducible static-analysis environment for the Google Guava (Java, JRE flavor) codebase using Checkstyle, Semgrep, and CK metrics.

## Scope
- Target repository: google/guava
- Analyzed source: `guava/src/com/google/common`
- Excluded: Android, GWT, tests, benchmarks, generated artifacts
- Language: Java
- Java version: OpenJDK 17 (via Docker)
- Execution environment: Linux (Docker container)

## Directory layout
```
guava-static-analysis/
├── Dockerfile
├── README.md
├── guava/                  # Google Guava repo (git submodule or cloned)
├── config/
├── scripts/
├── results/
│   ├── checkstyle/
│   ├── semgrep/
│   └── ck/
└── logs/
```

## Setup
1) Clone Guava into `guava-static-analysis/guava` (as a normal clone or submodule):
```
cd guava-static-analysis
git clone https://github.com/google/guava.git guava
```

2) Build the container:
```
docker build -t guava-static-analysis:latest .
```
```

## Notes
- The scripts target `guava/src/com/google/common` only, matching the scope definition.
- Checkstyle output: `results/checkstyle/checkstyle.xml`
- Semgrep output: `results/semgrep/semgrep.json`
- CK outputs CSVs to `results/ck/`
- If CK argument conventions change, adjust `scripts/run-ck.sh` to match your preferred CK invocation.
