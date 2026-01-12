# CIB Seven Quarkus Examples

This repository contains examples demonstrating how to use CIB seven process engine with Quarkus framework.

## Examples

### [Starter Example](starter/)

A basic Quarkus application showing:
- BPMN process deployment and execution
- Service task implementation with Java delegates
- REST API for process instance management
- Process variable handling

**Quick start:**
```bash
cd starter/
mvn quarkus:dev
curl -X POST http://localhost:8080/start-process
```

See [starter/README.md](starter/README.md) for detailed instructions.

## License

This project is licensed under the Apache 2.0 License – see the [LICENSE](LICENSE) file for details.

CIB seven uses and includes third-party dependencies published under various licenses. By downloading and using CIB seven artifacts, you agree to their terms and conditions. Refer to https://docs.cibseven.org/manual/latest/introduction/third-party-libraries/ for an overview of third-party libraries and particularly important third-party licenses we want to make you aware of.