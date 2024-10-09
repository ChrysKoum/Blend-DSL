## Documentation for Configuring Blend File for React-Flow Representation

## Setup the Blend file
You must create a Blend file in the src/dsls/{dsl_name}/{dsl_name}.blend. If there no folder {dsl_name} make one.  (This Explaination is for the Locsys Architecture)

Explanation how to integrade and see live the Blend file working coming soon...

### Node Type Configuration

Each node type in the Blend file is configured with several attributes to define its properties, behavior, and interactions within the React-Flow interface. Below is a detailed explanation of each attribute used in the node type configuration:

### Basic Attributes

- **name (lowercase)**: The object name of the node type in lowercase.
- **title**: A string representing the title of the node type.
  - Example: `"title": "Automation"`
- **subtitle(Optional)**: A brief description (2-3 words) about the node type. 
  - Example: `"subtitle": "Automates tasks"`
- **icon**: An icon representing the node. Type: string.(the available icons you can use are in the very bottom)
  - Example: `"icon": "HdrAutoIcon "`
- **draggable**: A boolean indicating whether the node type can be dragged and dropped within the React-Flow interface.
  - Example: `"draggable": true`

### Parameters

- **parameters**: An array of objects representing the normal parameters with a single value. Attributes include:
  - **name**: The name of the parameter.
  - **prefix**: A string prefix added before the parameter value.
  - **type (Optional)**: The data type of the parameter value. Common types include `string`, `int`, `number`, `password`, `email`, `url`, `tel`, `search`, `date`, `time`, `datetime-local`, `month`, and `week`. If not specified, it defaults to `string`/`text`.
    
  - **inputProps (Optional)**: An object or an array of objects defining additional properties for the input element. This can be used to specify attributes like `step`, `max`, `min`, etc. If an array is provided, the objects will be merged. If not provided, it defaults to an empty object.
  - **inputType(Optional)**: The type of input component (e.g., `wideInput`, `slider`, `switch`, `autocomplete`, `dynamicInputs`). Default to wideInput if not specify.
  - **placeholder(Optional)**: A placeholder text that will be shown in the input for the parameter.
  - **default(Optional)**: The default value for the parameter.
  - **multiLine(Optional)**: A boolean indicating if the parameter supports multiLine input that mean if the input box exceed the width it will create a new line. Default to false
  - **options(Optional)**: An array of options for `autocomplete` input type that are static.
  - **dependency(Optional)**: An array of options for `autocomplete` input type that is used to return options from the dependencies.
  - **complexDependency**: An array of options for `autocomplete` input type that is used to return options from the complex dependencies that have a specific format.
  - **visibleCondition**: A condition that determines if the parameter should be visible based on the value or values of other parameters.
    - **example**: {"communication_protocols":"AMQP"} or {"communication_protocols":["AMQP","MQTT"]} or [{"communication_protocols":"AMQP"},{"ssl":"true"}] 
  - **helperType**: An array of helper types that generate additional parameters with options from `complexDependenciesOptions`.
  - **startDelimiter**: The delimiter to start capturing the parameter value (e.g., `{`).
  - **optionsDelimiter**: The delimiter used to separate multiple values within the parameter (e.g., ` `).
  - **endDelimiter**: The delimiter to end capturing the parameter value (e.g., `}`).
  - **marks(Optional/inputType=slider)**: Represents the slider marks which indicate the specific values on the slider. Typically used for defining intervals or key points on the slider.
  - **track(Optional/inputType=slider)**:  Indicates the track of the slider, which shows the selected range of values between the minimum and maximum defined points on the slider.
  - **min (Optional/inputType=slider)**: The minimum value of the slider, defining the lower bound of the selectable range.
  - **max (Optional/inputType=slider)**: The maximum value of the slider, defining the upper bound of the selectable range.

### Example JSON

```json
    {
      "name": "type",
      "prefix": "type:",
      "type": "string",
      "inputType": "wideInput",
      "placeholder": "Type",
      "default": "",
      "unQuoted": true,
      "multiLine": false
    },
    // You can minimize it and let the defaults values do the job
    { 
      "name": "topic",
      "prefix": "topic:",
    },
    {
      "name": "broker",
      "prefix": "broker:",
      "inputType": "autocomplete",
      "default": "",
      "unQuoted": true,
      "dependency": "broker" // This target the dependencies and put as options the available brokers
    },
    {
      "name": "condition",
      "prefix": "condition:",
      "helperType": ["sensor", "actuator"], // This target the dependencies
      "default": "",
      "unQuoted": true,
      "multiLine": true
    },
   {
					"name": "actions",
					"prefix": "actions",
					"type": "array",
					"inputType": "autocomplete",
					"startDelimiter": "{",
					"optionsDelimiter": " ",
					"endDelimiter": "}",
					"options": ["commands"],
					"complexDependency": ["commands"], 
          // Here i use the complexDependency to specify that on this parameter
          // theres a complex dependency commands={"format": "${commands.name}"}
					"multiple": true
				}
```

- **nestedParameters**: An array of objects representing parameters nested within another parameter. Each object can have the following properties:
  - **label(Optional)**: A string representing the label of the nested parameter.
  - **name**: The name of the nested parameter.
  - **prefix**: A string prefix added before the nested parameter value.
  - **type(Optional)**: The data type of the nested parameter value (e.g., string, int, float, array).
  - **inputType**: Specifies the type of input. Use `dynamicInputs` for multiple variables.
  - **placeholder(Optional)**: A placeholder text for the nested parameter.
  - **multiLine(Optional)**: A boolean indicating if the parameter supports multiLine input.
  - **parameters**: An array of strings representing the names of the parameters.
  - **delimiter**: A string used to separate different parts of the nested parameter value.
  - **options**: An array of options for dropdown parameters. Options can be hardcoded values, dependencies, functions.
  - **types**: An array of strings indicating the type of input for each label (e.g., `input`, `dropdown`) adn will target some static option.
  - **inputTypes**: An array of strings indicating the types of input for each variable when using `dynamicInputs` will target some dependency.
  - **connectedLabels**: An array of strings representing parameters that are connected. When changing the name, you can restrict the type of the value based on the complex option.
  - **endDelimiter**: The delimiter to end capturing the end of the parameter value (e.g., `}`).

  Example:
  ```json
  "nestedParameters": {
    "attributes": [
      {
        "name": "attributes",
        "prefix": "- ",
        "type": "string",
        "delimiter": ":",
        "parameters": ["name", "type"],
        "options": ["float", "int", "string", "bool", "dist", "list"],
        "types": ["input", "dropdown"],
        "inputType": "dynamicInputs"
      }
    ],
    "actions": [
					{
						"name": "actions",
						"prefix": "- ",
						"delimiter": ":",
						"inputType": "dynamicInputs",
						"parameters": ["name", "value"],
						"inputTypes": ["dropdown", "dynamicInput"],
						"options": ["actuator", "getInputByType"],
						"connectedLabels": ["name", "value"]
					}
				],
    "timeConstraints": [
				{
					"label": "Time Constraints",
					"name": "timeConstraints",
					"unQuoted": true,
					"prefix": "- ",
					"delimiter": "(",
					"endDelimiter": ")",
					"parameters": ["type", "expression"],
					"inputType": "dynamicInputs",
					"types": ["dropdown", "input"],
					"options": ["FROM_APP_START", "FROM_GOAL_START"]
				}
      ]
  }
  ```
### Patterns and Keywords

- **startPattern**: Defines the static starting line of the node type for DSL to graphical transformation. Can be a single pattern or an array of patterns.
  - Example:
    ```json
    "startPattern": ["Goal<${goalType}> ${title}", "Goal<${goalType}Area> ${title}"]
    ```
  - **Regex Creation and Parameters**: The `startPattern` can contain placeholders in the format `${parameterName}`. These placeholders are replaced with `(\w+)` to create a regex pattern dynamically. The parameters are then extracted from the matched values in the line.
    - Example:
      - Given `startPattern`: `["Goal<${goalType}> ${title}"]`
      - Regex created: `Goal<(\\w+)> (\\w+)`
      - Parameters extracted: `goalType`, `title`

- **startPatternExceptions**: Specifies exceptions for the general regex pattern created from `startPattern`. Each exception can be a single object or an array of objects, detailing specific patterns and their conditions.
  - Example:
    ```json
    "startPatternExceptions": [
      {
        "goalType": "StraightLine",
        "order": 1
      },
      {
        "title": "areagoal1",
        "order": 1
      },
      {
        "goalType": "Rectangle",
        "order": 2
      }
    ]
    ```
    - Example:
      - Given `startPattern`: `["Goal<${goalType}> ${title}"]`
      - Given `startPatternExceptions`: `{
        "goalType": "StraightLine",
        "order": 1
      }`
      - Regex created: `Goal<(\\w+)> (\\w+)`
      - Parameters extracted: `goalType`, `title`
      - Condition if first (\\w+) that is the goalType is the same as the exception goalType.
      
  - **Usage**: When a line matches the `startPattern` regex, the `startPatternExceptions` are checked to see if any specific conditions are met. If an exception matches, check if the value of key that is the parameter is eqaul with match it get. 

- **endKeyword**: A keyword indicating the end of a node type.
  - Example: `"endKeyword": "end"`
### Handles

- **handles (Optional)**: Defines the handles for connecting nodes. Attributes include `type` (source or target), `style` (background and top for position), `parameterDependency`, `target`, and `connectionLimit`. This can be omitted if the node does not have any graphical connections with other nodes.
  - **type**: Specifies the type of handle, either `source` or `target`.
  - **style**: Defines the visual style of the handle, including properties like `top` (position) and `background` (color).
  - **parameterDependency**: Specifies the dependency parameter that will change its value if a connection is made. This can be a string that indicates which parameter in the node data will be affected by the connection.
  - **target**: Defines the allowable target nodes for connections. This can be a string or an array of strings, limiting which other nodes can connect to this handle.
  - **connectionLimit**: Specifies the connection limits for different target node types. It is an object where keys are node types and values are the maximum number of connections allowed (`-1` for unlimited).
  - Example:
    ```json
    "handles": [
      {
        "type": "source",
        "style": { "top": 20, "background": "#00FF00" },
        "parameterDependency": "starts",
        "target": "automation",
        "connectionLimit": {"automation": "-1", "starts": "-1"}
      },
      {
        "type": "source",
        "style": { "top": 40, "background": "#00FF00" },
        "parameterDependency": "stops",
        "target": "automation",
        "connectionLimit": {"automation": "-1", "stops": "-1"}
      },
      {
        "type": "source",
        "style": { "top": 60, "background": "#00FF00" },
        "parameterDependency": "after",
        "target": "automation",
        "connectionLimit": {"automation": "-1", "stops": "-1"}
      },
      { 
        "type": "target" 
      }
    ]
    // Complex dependencied of handles
    "handles": [
				{
					"type": "source",
					"style": { "top": 20, "background": "#00FF00" },
					"parameterDependency": "transitions.event",
					"handleTarget": {"nodeType": "events", "parameter": "events.name"},
					"connectionLimit": {"state": "-1", "events": "-1"}
				},
				{
					"type": "source",
					"style": { "top": 40, "background": "#00FF00" },
					"parameterDependency": "actions",
					"handleTarget": {"nodeType": "commands", "parameter": "commands.name"},
					"connectionLimit": {"state": "-1", "commands": "-1"}
				},
				{
					"type": "source",
					"style": { "top": 60, "background": "#00FF00" },
					"parameterDependency": "transitions.state",
					"handleTarget": "state",
					"connectionLimit": {"state": "-1"}
				},
				{ "type": "target" }
			],
    ```

### Explanation:

- **String Dependency**:
  - `"dependency": "starts"`: A single dependency parameter named `starts`.

- **Array of Strings Dependency**:
  - `"dependency": ["broker", "goals"]`: Multiple dependency parameters, `broker` and `goals`.

- **Object Dependency**:
  - `"dependency": { "broker": "broker", "goals": ["complexgoal", "entitygoal", "trajectorygoal", "posegoal", "areagoal"] }`: Nested dependency parameters where `broker` is a single dependency and `goals` is an array of possible dependencies.


### Color Configuration

- **colorConfig**: An object specifying color configurations for the edges connecting nodes. Each object has a startColor and endColor that will form a gradient.
  - Example:
    ```json
    "colorConfig": {
      "starts": { "startColor": "#6bbf59", "endColor": "#b0f7a6" },
      "stops": { "startColor": "#d15959", "endColor": "#f7a6a6" },
      "after": { "startColor": "#ff9900", "endColor": "#ffcc66" }
    }
    ```

### Dependencies

- **dependencies**: An object of objects specifying dependencies with other node types, used for parameters with autocomplete and options to fetch their dependency options. This can also be used for complex dependencies if there are `parameter`, `format`, and `initFormat` attributes that will be used for nested parameters dropdowns.

  - **parameter**: The name of the dependent parameter. This can be dynamic and use placeholders to reference values on the dependent node.
  - **format**: A string format used for complex dependencies. This format can include placeholders to dynamically generate the dependency value if is also nested can handle it.
  - **initFormat**: A string format used to initialize the dependency value with placeholders. This can reference both the current node's data(with this ) and the dependent node's data.

  - Example:
    ```json
    "dependencies": {
      "broker": {
        "parameter": "title",
      },
      "metadata": {
        "initFormat": "${name}.sensor.${this.title}"
      },
      "actuator": {
        "format": "${title}.${attributes.name}"
      }
    }
    ```

### Limits and Types

- **maxInstances(Optional), {On Hold Feature}**: Specifies the maximum number of instances of a node type. If -1, it is unlimited.
  - Example: `"maxInstances": -1`. Default if draggable is true set to -1, if is false set 1.
- **connectionLimit**: Specifies connection conditions on how many nodes can be connected is specified in the **handles**. If -1, it is unlimited.
  - Example:
    ```json
    "connectionLimit": {
      "broker": "1",
      "sensor": "-1"
    }
    ```
- **parameterException**: Used if the starting pattern of the node type is the same as another node type and needs a parameter to specify the nodeType.
  - Example: `"parameterException": "type"`

- **Icons Available**:
	HdrAutoIcon,
	SensorsIcon,
	LeakAddIcon,
	PlayForWorkIcon,
	SwapHorizIcon,
	GroupWorkIcon,
	FlagIcon,
	AllOutIcon,
	SmartToyIcon,
	AirlineStopsIcon,
	WorkspacesIcon,
	EmojiEventsIcon,
	CodeIcon,
	ControlCameraIcon,
	RestartAltIcon,
	default: SensorsIcon, // Default icon if none matches

  **Tips:**
  - [Here is where you can See what Icons are](https://mui.com/material-ui/material-icons/)
  - In the file src\components\create-graph\utils\transformer_dsl_obj.js you can add more icons if you want someone else from the mui material icons.

This documentation provides a comprehensive guide to configuring the JSON file for representing nodes in React-Flow. Each attribute and its purpose are explained with examples to help you create detailed and accurate configurations.