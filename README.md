# Identity Service

Spring Boot 3 / Java 21 / Gradle service for user registration with BCrypt password hashing.

## Run

1. Create PostgreSQL database: `CREATE DATABASE identity_db;`
2. Set `DB_URL`, `DB_USERNAME`, and `DB_PASSWORD` if the defaults in `application.properties` do not match your local database.
3. Run `./gradlew bootRun`.

## Register

```bash
curl -i -X POST http://localhost:8080/api/auth/register \
  -H 'Content-Type: application/json' \
  -d '{"username":"alice","password":"secret123"}'
```

The response has status 201 and contains `id`, `username`, and `role` only. Duplicate usernames return 409. Check the database with `SELECT username, password FROM users;`; `password` contains a BCrypt hash, never the original value.
