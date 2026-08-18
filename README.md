# Unstray Config Server

A Spring Cloud Config Server for the Unstray Platform microservices architecture. This server provides centralized configuration management for all microservices in the ecosystem.

## Overview

The Unstray Config Server is a centralized configuration service that enables dynamic configuration management across the microservices platform. It serves configuration files for:

- **API Gateway** - Central API entry point
- **Eureka Server** - Service discovery and registration
- **Item Service** - Item/product management service
- **Media Service** - Media handling and storage service
- **User Service** - User management service

## Technology Stack

- **Java 25** - Latest Java runtime
- **Spring Boot 4.1.0** - Application framework
- **Spring Cloud Config Server 2025.1.2** - Centralized configuration management
- **Spring Cloud Discovery Client** - Service discovery integration
- **Maven** - Build and dependency management

## Prerequisites

Before you begin, ensure you have the following installed:

- **JDK 25** or higher
- **Maven 3.8.0** or higher
- **Git** (for version control)

## Installation & Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd unstray-config-server
```

### 2. Build the Project

```bash
./mvnw clean build
```

Or on Windows:

```bash
mvnw.cmd clean build
```

### 3. Configuration

The configuration settings are defined in `src/main/resources/application.yaml`. Key properties:

```yaml
spring:
  application:
    name: config-server
  cloud:
    config:
      server:
        git:
          # Configure git repository for config files
          uri: <git-repository-url>
```

## Running the Application

### Development Mode

```bash
./mvnw spring-boot:run
```

### Production Mode (JAR)

```bash
./mvnw clean package
java -jar target/config-server-0.0.1-SNAPSHOT.jar
```

The server will start on the default port (typically **8888**).

## Configuration Files

The server manages configuration for the following services:

```
src/main/resources/config/
├── api-gateway.yaml
├── eureka-server.yaml
├── item-service.yaml
├── media-service.yaml
├── user-service.yaml
└── application.yaml
```

Each YAML file contains service-specific configuration that can be retrieved by the respective microservices at runtime.

## API Endpoints

### Retrieve Configuration

```
GET /{application}/{profile}/{label}
GET /{application}/{profile}
GET /{application}/{label}
GET /{application}
```

**Example:**

```bash
curl http://localhost:8888/item-service/production/main
```

### Actuator Endpoints (Health & Monitoring)

```
GET /actuator
GET /actuator/health
GET /actuator/env
```

## Project Structure

```
src/
├── main/
│   ├── java/
│   │   └── com/unstray/platform/config_server/
│   │       └── ConfigServerApplication.java
│   └── resources/
│       ├── application.yaml
│       └── config/
│           ├── api-gateway.yaml
│           ├── eureka-server.yaml
│           ├── item-service.yaml
│           ├── media-service.yaml
│           └── user-service.yaml
└── test/
    └── java/
        └── com/unstray/platform/config_server/
            └── ConfigServerApplicationTests.java
```

## Building & Testing

### Run Tests

```bash
./mvnw test
```

### Build JAR

```bash
./mvnw clean package
```

The packaged JAR will be available at `target/config-server-0.0.1-SNAPSHOT.jar`

## Monitoring & Health Checks

The application includes Spring Boot Actuator for monitoring:

- **Health Endpoint**: `GET /actuator/health` - Check application status
- **Environment Endpoint**: `GET /actuator/env` - View environment properties
- **Metrics Endpoint**: `GET /actuator/metrics` - Application metrics

## Service Discovery

This config server integrates with Eureka for service discovery. Ensure the Eureka server is running and properly configured in `application.yaml` for the config server to register itself.

## Troubleshooting

### Config Server Won't Start

- Verify Java 25 is installed: `java -version`
- Check Maven installation: `mvn -version`
- Ensure no port conflicts on port 8888

### Configuration Not Loading

- Verify the git repository URI is correct
- Check network connectivity to the config repository
- Review logs for authentication/permission issues

### Service Discovery Issues

- Ensure Eureka server is running
- Verify Eureka server URL in `application.yaml`
- Check network connectivity between services

## Contributing

When adding new service configurations:

1. Create a new YAML file in `src/main/resources/config/`
2. Follow the naming convention: `{service-name}.yaml`
3. Test the configuration by retrieving it through the API
4. Update this README with the new service details

## License

[Add your license information here]

## Support

For issues and questions, please contact the Unstray Platform team.

---

**Last Updated**: 2026-08-18  
**Version**: 0.0.1-SNAPSHOT  
**Status**: Development
