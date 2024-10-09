# Blend DSL

**Blend DSL** is a dynamic Domain-Specific Language (DSL) designed for transforming textual DSLs into graphical representations using React Flow. This repository is structured to support flexible JSON schemas, powerful transformation algorithms, and thorough documentation, making it easy for users to contribute and extend the system. (This repository is incomplete as the real logic and interface is not integrated yet)

## Features

- **Flexible Metamodel**: Supports multiple DSL grammars with easy extensibility.
- **Dynamic Transformation**: Seamlessly converts textual DSL models into graphical representations.
- **Extensible**: New node types, parameters, and dependencies can be added effortlessly.
- **Backward Compatibility**: Ensures compatibility with older models while evolving.
- **Graphical Representation**: Visualize your DSL models using React Flow.

## Getting Started

### Installation

1. **Clone the repository**:

   ```bash
   git clone https://github.com/your-username/blend-dsl.git
   cd blend-dsl
   ```

### Usage

1. **Define Your DSL in JSON**: Create or modify a DSL in JSON format. Refer to the schema files in the `schemas/` directory for guidance.

2. **Run the Transformer (Not yet Integrated)**:

   Use the transformation script to convert your DSL to a graphical model:

   ```bash
   node src/index.js
   ```

3. **View the Graphical Model (Not yet Integrated)**: Open the React Flow interface to visualize your DSL's graphical representation. Not yet Avialable but you can test how it will be on the Locsys website after the Integration of my solution is in the live production website or on the [BlendXSync](https://github.com/ChrysKoum/BlendXSync) project.

## Documentation

- **[Metamodel Design](docs/metamodel_design.md)**: Information about the internal DSL metamodel.

## Contributing

We welcome contributions! Please read the [CONTRIBUTING.md](CONTRIBUTING.md) file for more details on how to get involved.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
