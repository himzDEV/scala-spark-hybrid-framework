# Scala Spark Config-Driven Framework Documentation
GPT Name - "Scala Spark Framework"
## Overview
This is a **modular, reusable, config-driven data processing framework** built on **Scala + Apache Spark**, designed to allow teams to process data dynamically with minimal code by feeding configuration files. The framework is packaged as a **JAR** and can be extended by other teams through custom Scala objects and config files.

## Design Approach
### Hybrid Architecture:
- **OOP** → Define module boundaries via traits (`Source`, `Transformer`, `Validator`, `Sink`) for extensibility.
- **FP** → Use pure functions and immutability within each module for reliability and testability.

## Key Components
| Module         | Responsibility                             |
|----------------|---------------------------------------------|
| `config`      | Parsing and validating the config files     |
| `source`      | Reading from data sources (GCS, JDBC, etc.) |
| `transformation`| Apply configurable transformations        |
| `validation`  | Run data quality checks                     |
| `sink`        | Write processed data to targets             |
| `errorhandler`| Error capture and handling                  |
| `notifier`    | Send notifications (email, Slack)           |
| `core`        | Orchestration (via `PipelineRunner`)        |

## User Input
- **Config file (YAML/JSON/HOCON)** that specifies:
  - Source details
  - Transformations
  - Validations
  - Target sink
  - Error handling and notifications

- **Optional runtime parameters** (like date overrides, environment).

## Usage
1. User writes config file.
2. User creates a small Scala object:

   ```scala
   object CustomerPipelineApp {
     def main(args: Array[String]): Unit = {
       PipelineRunner.run(args(0))
     }
   }
   ```

3. User submits the job using Spark.

## Extensibility
- Add new transformations, sources, or sinks by:
  1. Implementing the respective trait.
  2. Registering in the corresponding factory.
  3. Documenting usage for others.

## Deployment
- The framework is packaged as a **fat JAR** and stored in a shared artifact repository (like Nexus/Artifactory).
- Users depend on this JAR and build lightweight projects on top of it.

## Next Steps
- Scaffold SBT project  
- Build core modules  
- Provide sample configs  
- Write contributor guidelines  

