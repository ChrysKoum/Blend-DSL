# Blend DSL

**Blend DSL** is a dynamic Domain-Specific Language (DSL) designed for transforming textual DSLs into graphical representations using React Flow. This repository is structured to support flexible JSON schemas, powerful transformation algorithms, and thorough documentation, making it easy for users to contribute and extend the system.

## Features

- **Flexible Metamodel**: Supports multiple DSL grammars with easy extensibility.
- **Dynamic Transformation**: Seamlessly converts textual DSL models into graphical representations.
- **Extensible**: New node types, parameters, and dependencies can be added effortlessly.
- **Backward Compatibility**: Ensures compatibility with older models while evolving.
- **Graphical Representation**: Visualize your DSL models using React Flow.

## Repository Structure

```
blend-dsl/
├── README.md                  # Project overview and usage instructions
├── LICENSE                    # License information (MIT)
├── CONTRIBUTING.md             # Guidelines for contributing
├── .gitignore                  # Files and directories to ignore in version control
├── schemas/                    # JSON schemas for DSL definitions
│   ├── json_schema.json        # Primary DSL JSON schema
│   └── new_json_schema.json    # Updated DSL JSON schema
├── src/                        # Source code for transformations
│   ├── transformers/           # Transformers to convert DSLs to graphical models
│   │   ├── transformer_dsl_obj.js
│   │   └── transformNewToOldJson.js
│   └── index.js                # Entry point for transformation logic
├── examples/                   # Example DSL files demonstrating usage
│   ├── example1.dsl
│   └── example2.dsl
├── docs/                       # Project documentation
│   ├── setup.md                # Setup instructions
│   ├── usage.md                # Usage guide
│   └── metamodel_design.md     # Details on the DSL metamodel design
├── tests/                      # Unit and integration tests
│   ├── transformer.test.js
│   └── example.test.js
└── images/                     # Diagrams and visuals for documentation
    ├── meta_model_blenddsl.png
    └── new_meta_model_blenddsl.png
```

## Getting Started

### Installation

1. **Clone the repository**:

   ```bash
   git clone https://github.com/your-username/blend-dsl.git
   cd blend-dsl
   ```

### Usage

1. **Define Your DSL in JSON**: Create or modify a DSL in JSON format. Refer to the schema files in the `schemas/` directory for guidance.

2. **Run the Transformer**:

   Use the transformation script to convert your DSL to a graphical model:

   ```bash
   node src/index.js
   ```

3. **View the Graphical Model**: Open the React Flow interface to visualize your DSL's graphical representation.

### Example

An example DSL file is provided in the `examples/` directory. You can test it by running the transformer script.

```dsl
Goal<Rectangle> Build Bridge
type: infrastructure
broker: mainBroker
condition: sensor
actions: {command1, command2}
```

## Documentation

- **[Setup Guide](docs/setup.md)**: Instructions for setting up the project locally.
- **[Usage Guide](docs/usage.md)**: Detailed usage instructions for Blend DSL.
- **[Metamodel Design](docs/metamodel_design.md)**: Information about the internal DSL metamodel.

## Contributing

We welcome contributions! Please read the [CONTRIBUTING.md](CONTRIBUTING.md) file for more details on how to get involved.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
