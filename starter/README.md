# CIB seven Quarkus - Starter Example

This is a simple Quarkus application that demonstrates BPMN process execution using CIB seven process engine.

## What's included

- **BPMN Process** (`src/main/resources/process.bpmn`): A simple process with start → service task → end
- **Service Delegate** (`ServiceDelegate.java`): Java delegate that executes during the service task
- **Process Starter** (`ProcessStarterResource.java`): REST endpoint to start process instances
- **Process Deployer** (`ProcessDeployer.java`): Automatically deploys the BPMN process on startup

## Prerequisites

- Java 17 or later
- Maven 3.8+ 

## Building

From the project root:

```bash
mvn clean compile -pl starter
```

Or from the `starter/` directory:

```bash
mvn clean compile
```

## Running

### Development Mode (with hot reload)

```bash
mvn quarkus:dev -pl starter
```

Or from the `starter/` directory:

```bash
mvn quarkus:dev
```

### Production Mode

Build and run the application:

```bash
mvn clean package -pl starter
java -jar starter/target/quarkus-app/quarkus-run.jar
```

## Testing the Application

Once running (default port 8080), you can:

1. **Start a process instance:**
   ```bash
   curl -X POST http://localhost:8080/process/start
   ```

2. **Check application health:**
   ```bash
   curl http://localhost:8080/q/health
   ```

The service task will execute the `ServiceDelegate`, which logs a message and sets a process variable.

## Process Details

The BPMN process (`process.bpmn`) contains:
- **Process ID**: `process`
- **Service Task**: Uses delegate expression `#{serviceDelegate}`
- **History TTL**: 1 day

The `ServiceDelegate` demonstrates basic process variable manipulation and logging.