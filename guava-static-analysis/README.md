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

2) Build the container (from the project root):
```
docker build -t guava-static-analysis:latest .
```
```

## Checkstyle extension
3) Start an interactive shell inside the container:
```
docker run --rm -it -v "$(pwd)":/workspace -w /workspace guava-static-analysis:latest bash
```
```

4) Run checkstyle inside the container using the google's checkstyle rules
```
java -jar /opt/tools/checkstyle-10.12.4-all.jar -c config/google_checks.xml guava/guava/src/com/google/common -f xml -o results/checkstyle/checkstyle_result.xml
```
```


## Notes
- Checkstyle output: `results/checkstyle/checkstyle_result.xml`
- Semgrep output: `results/semgrep/semgrep.json`
- CK outputs CSVs to `results/ck/`
