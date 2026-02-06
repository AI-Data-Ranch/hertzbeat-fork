Local Test Evidence - Java 21 Upgrade

Timestamp (UTC): 2026-02-06T07:22:00Z

Backend
- Command: JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64 mvn spring-boot:run -Dspring-boot.run.jvmArguments="--add-opens=java.base/java.nio=org.apache.arrow.memory.core,ALL-UNNAMED"
- Logs: devin-logs/java21-upgrade_20260205_230035124/build-backend.log
- Result: Started successfully (H2 migrations applied, services initialized)

Frontend
- Command: pnpm install && pnpm start
- Result: Angular dev server listening at http://localhost:4200 (Compiled successfully)

UI Verification
- Steps: Navigated to http://localhost:4200, logged in with admin/hertzbeat, reached Dashboard
- Recording: /home/ubuntu/screencasts/rec-afaa36d9673446b4814661fce6eb90d0-edited.mp4

Notes
- VM option --add-opens applied as required
- No runtime errors observed during smoke test
