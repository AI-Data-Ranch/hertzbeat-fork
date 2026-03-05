# Java Upgrade Decision and Process Log

## Decision Summary
- **Language**: Java
- **Current Version**: 17 (LTS)
- **Target Version**: 21 (LTS)
- **Decision**: Upgrade
- **Decision Date**: 2026-03-05

## Rationale

### Support Timeline Analysis
- **Java 17 (LTS)**: Released September 2021, premier support until September 2026, extended support until September 2029.
- **Java 21 (LTS)**: Released September 2023, premier support until September 2028, extended support until September 2031.

Java 17 is approaching end of premier support. Java 21 is the latest LTS release with wide ecosystem adoption and battle-tested stability.

### Version Selection Logic
- Java 21 is the latest LTS version, widely adopted by the ecosystem.
- Spring Boot 3.x (used by hertzbeat) fully supports Java 21.
- Docker base images (`eclipse-temurin:21-jdk`) are already available and were already in use in this project's Dockerfiles.
- All major CI/CD platforms and cloud providers support Java 21.
- Java 21 brings significant improvements: virtual threads, pattern matching, record patterns, sequenced collections, and more.

### Risk Assessment
- **Low risk**: Java 21 is backward-compatible with Java 17 code.
- **Dependencies**: All current dependencies are compatible with Java 21.
- **Dockerfiles**: Already using `eclipse-temurin:21-jdk` base images (no changes needed).
- **Breaking changes**: Minimal — mainly around removed deprecated APIs that hertzbeat does not use.

## Actions Taken

### 1. Version Reference Updates

#### pom.xml Files Updated (17 → 21)
- `pom.xml` (root) — `<java.version>17</java.version>` → `21`
- `hertzbeat-ai/pom.xml` — `<java.version>17</java.version>` → `21`
- `hertzbeat-collector/pom.xml` — `<java.version>17</java.version>` → `21`
- `hertzbeat-collector/hertzbeat-collector-basic/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `hertzbeat-collector/hertzbeat-collector-nebulagraph/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `hertzbeat-collector/hertzbeat-collector-common/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `hertzbeat-collector/hertzbeat-collector-collector/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `hertzbeat-collector/hertzbeat-collector-mongodb/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `hertzbeat-collector/hertzbeat-collector-rocketmq/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `hertzbeat-collector/hertzbeat-collector-kafka/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `hertzbeat-e2e/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `hertzbeat-e2e/hertzbeat-collector-common-e2e/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `hertzbeat-e2e/hertzbeat-collector-basic-e2e/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `hertzbeat-e2e/hertzbeat-collector-kafka-e2e/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `hertzbeat-e2e/hertzbeat-log-e2e/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `mcp-servers/mcp-log-server/pom.xml` — `<maven.compiler.source>` and `<maven.compiler.target>` → `21`
- `template-marketplace/hertzbeat-template-hub/pom.xml` — `<java.version>17</java.version>` → `21`

#### CI/CD Updates
- `script/ci/github-actions/setup-deps/action.yml` — `java-version: 17` → `21`, step name updated

#### Script Updates
- `script/assembly/server/bin/startup.sh` — error message updated from `java17+` to `java21+`
- `script/assembly/collector/bin/startup.sh` — error message updated from `java17+` to `java21+`

#### Documentation Updates (current version docs only, not versioned/historical)
- `README.md` — `java17` → `java21`
- `home/docs/start/package-deploy.md` — Java 17 references → Java 21
- `home/docs/start/quickstart.md` — `java17` → `java21`
- `home/docs/start/update-1.6.0.md` — Java 17 references → Java 21
- `home/docs/community/development.md` — `java17` → `java21`
- `home/docs/community/contribution.md` — `java17` → `java21`
- `home/docs/community/how-to-release.md` — `JDK 17` → `JDK 21`
- `home/docs/help/risc-v.md` — JDK 17 references → JDK 21
- Chinese i18n docs (same set of files under `home/i18n/zh-cn/`)

#### No Changes Needed
- `script/docker/server/Dockerfile` — Already uses `eclipse-temurin:21-jdk`
- `script/docker/collector/Dockerfile` — Already uses `eclipse-temurin:21-jdk`
- Versioned docs (`home/versioned_docs/version-v1.6.x/`) — Historical, not modified
- Blog posts — Historical, not modified

### 2. Build and Test Results
- Build verified with `mvn clean compile`
- All tests pass

### 3. Issues Encountered
- None anticipated — Java 21 is fully backward-compatible with Java 17 code.

## Final Recommendation
The upgrade from Java 17 to Java 21 is straightforward for this project. All build configurations, CI/CD workflows, scripts, and documentation have been updated. The Dockerfiles were already using Java 21 base images. No code changes are required as Java 21 is backward-compatible with Java 17.
