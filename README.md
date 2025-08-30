# CSMS - Three separate projects: contracts + auth + transaction

This archive contains three independent Gradle projects:

- `csms-contracts` — Avro schemas and generated DTOs. Publish to Maven Local.
- `csms-authentication-service` — Authentication service (Kafka consumer + producer).
- `csms-transaction-service` — Transaction service (REST) that uses Kafka request/response.

## Quickstart

1. Build & publish contracts to local Maven repo:
```bash
cd csms-contracts
./gradlew clean build publishToMavenLocal
```

2. Start Kafka + Schema Registry:
```bash
docker-compose up -d
# wait for kafka and schema-registry to be healthy on ports 9092 and 8081
```

3. Start services (in separate terminals):
```bash
cd csms-authentication-service
./gradlew bootRun

cd ../csms-transaction-service
./gradlew bootRun
```

4. Call the transaction endpoint:
```bash
curl -X POST http://localhost:8080/transaction/authorize -H "Content-Type: application/json" -d '{"stationUuid":"25aac66b-6051-478a-95e2-6d3aa343b025","driverIdentifier":{"id":"aaaaaaaaaaaaaaaaaaaa"}}'
```
