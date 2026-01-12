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
   curl http://localhost:8080/start-process
   ```

2. **Check application health:**
   ```bash
   curl http://localhost:8080/q/health
   ```

The service task will execute the `ServiceDelegate`, which logs a message and sets a process variable.

## Testing with Local Kubernetes Cluster (kind)

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed and running
- [kind](https://kind.sigs.k8s.io/docs/user/quick-start/#installation) installed
- [kubectl](https://kubernetes.io/docs/tasks/tools/) installed

### Steps

1. **Build the application:**
   ```bash
   mvn clean package -DskipTests
   ```

2. **Build Docker image:**
   ```bash
   docker build -f src/main/docker/Dockerfile.jvm -t cibseven/cibseven-quarkus-example:local .
   ```

3. **Create kind cluster (if not exists):**
   ```bash
   kind create cluster --name cibseven-local
   ```

4. **Load Docker image into kind:**
   ```bash
   kind load docker-image cibseven/cibseven-quarkus-example:local --name cibseven-local
   ```

5. **Deploy to Kubernetes:**
   ```bash
   kubectl apply -f src/main/docker/deployment.yaml
   ```

6. **Verify deployment:**
   ```bash
   kubectl get pods
   kubectl get svc
   ```

7. **Test the application:**
   ```bash
   kubectl port-forward svc/cibseven-quarkus-example 8080:8080 &
   curl http://localhost:8080/start-process
   pkill -f "kubectl port-forward"
   ```

8. **View logs:**
   ```bash
   kubectl logs -l app=cibseven-quarkus-example
   ```

### Cleanup

To remove the deployment:
```bash
kubectl delete -f src/main/docker/deployment.yaml
```

To delete the kind cluster:
```bash
kind delete cluster --name cibseven-local
```

## Process Details

The BPMN process (`process.bpmn`) contains:
- **Process ID**: `process`
- **Service Task**: Uses delegate expression `#{serviceDelegate}`
- **History TTL**: 1 day

The `ServiceDelegate` demonstrates basic process variable manipulation and logging.