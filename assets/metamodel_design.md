## Documentation for Configuring JSON File for React-Flow Representation

### Setup the json file
You must create a json file in the src/dsls/{dsl_name}/{dsl_name}.json. If there no folder {dsl_name} make one.
- If you are going to use the syntax of the simple Metamodel that the grammar and interface settings are different you need to make a file with the name like this "src/dsls/{dsl_name}/{dsl_name}_simple.json" with the "_simple" 

### Node Type Configuration

Each node type in the JSON file is configured with several attributes to define its properties, behavior, and interactions within the React-Flow interface. Below is a detailed explanation of each attribute used in the node type configuration, along with examples.

### Basic Attributes

- **name (lowercase)**: The object name of the node type in lowercase.
  - Example: `"name": "automation"`
  
- **title**: A string representing the title of the node type.
  - Example: `"title": "Automation"`
  
- **subtitle (Optional)**: A brief description (2-3 words) about the node type.
  - Example: `"subtitle": "Automates tasks"`
  
- **icon**: An icon representing the node. The available icons can be found at the bottom of this document.
  - Example: `"icon": "HdrAutoIcon"`
  
- **draggable**: A boolean indicating whether the node type can be dragged and dropped within the React-Flow interface.
  - Example: `"draggable": true`

### Parameters

Parameters define the various inputs or configurations for the node type. These can be single values or complex nested structures.

#### Single Value Parameters

- **parameters**: An array of objects representing the parameters with a single value. Each parameter object can have the following attributes:

  - **name**: The name of the parameter.
  - **prefix**: A string prefix added before the parameter value.
  - **type (Optional)**: The data type of the parameter value. Common types include `string`, `int`, `number`, `password`, `email`, etc.
  - **inputProps (Optional)**: Additional properties for the input element, such as `step`, `max`, `min`, etc.
  - **inputType (Optional)**: The type of input component (e.g., `wideInput`, `slider`, `switch`, `autocomplete`, `dynamicInputs`). Defaults to `wideInput`.
  - **placeholder (Optional)**: Placeholder text shown in the input.
  - **default (Optional)**: The default value for the parameter.
  - **multiLine (Optional)**: A boolean indicating if the input should support multiline input. Defaults to `false`.
  - **options (Optional)**: An array of options for `autocomplete` input type that are static.
  - **dependency (Optional)**: An array of options for `autocomplete` input type based on dependencies.
  - **complexDependency (Optional)**: Options for `autocomplete` input type from complex dependencies with a specific format.
  - **visibleCondition**: A condition that determines if the parameter should be visible based on other parameters' values.
  - **helperType (Optional)**: An array of helper types that generate additional parameters with options from `complexDependenciesOptions`.
  - **startDelimiter (Optional)**: The delimiter to start capturing the parameter value (e.g., `{`).
  - **optionsDelimiter (Optional)**: The delimiter used to separate multiple values within the parameter (e.g., ` `).
  - **endDelimiter (Optional)**: The delimiter to end capturing the parameter value (e.g., `}`).
  - **marks (Optional/inputType=slider)**: Represents specific values on a slider.
  - **track (Optional/inputType=slider)**: Indicates the selected range on a slider.
  - **min (Optional/inputType=slider)**: The minimum value of the slider.
  - **max (Optional/inputType=slider)**: The maximum value of the slider.

**Example JSON/Grammar for Single Value Parameters:**

**Example 1 Grammar:**

```plaintext
broker: <broker_name>
broker: default_broker
```
**Example 1 JSON:**
```json
{
  "name": "broker",
  "prefix": "broker:",
  "inputType": "autocomplete",
  "default": "",
  "unQuoted": true,
  "dependency": "broker" 
}
```
**Example 2 Grammar:**

```plaintext
type: <entity_type>
type: sensors
```
**Example 2 JSON:**
```json
{
    "name": "entityType",
    "prefix": "type:",
    "type": "string",
    "inputType": "wideInput",
    "placeholder": "Type",
    "default": "",
    "unQuoted": true,
    "multiLine": false
  },
```

**Example 3 Grammar:**

```plaintext
actions <actions>
actions {<action> <action> <action> <action>}
actions {unlockDoor lockPanel} //is from the dependencie commands name
```
**Example 3 JSON:**
```json
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
  "dependencies": {
      "commands": {
        "format": "${commands.name}"
      }
    }
```
#### Nested Parameters

Nested parameters allow you to define parameters that have multiple sub-parameters.

- **nestedParameters**: An array of objects representing nested parameters within another parameter. Each nested parameter object can have the following attributes:

  - **label (Optional)**: A string representing the label of the nested parameter.
  - **name**: The name of the nested parameter.
  - **prefix**: A string prefix added before the nested parameter value.
  - **type (Optional)**: The data type of the nested parameter value (e.g., string, int, float, array).
  - **inputType**: Specifies the type of input, e.g., `dynamicInputs` for multiple variables.
  - **placeholder (Optional)**: A placeholder text for the nested parameter.
  - **multiLine (Optional)**: A boolean indicating if the input should support multiline input.
  - **parameters**: An array of strings representing the names of the sub-parameters.
  - **empty**: If the value can also be empty in the grammar
  - **unquoteOuter**: Is if you dont want to capitulate the output value with outer quotes
  - **delimiter**: A string used to separate different parts of the nested parameter value.
  - **options**: An array of options for dropdown parameters.
  - **types**: An array of strings indicating the type of input for each label (e.g., `input`, `dropdown`).
  - **inputTypes**: An array of strings indicating the types of input for each variable when using `dynamicInputs`.
  - **connectedLabels**: An array of strings representing parameters that are connected.
  - **endDelimiter**: The delimiter to end capturing the parameter value (e.g., `}`).

**Example JSON/Grammar for Nested Parameters:**

**Example 1 Grammar:**


```plaintext
  attributes:
      - <name>: <type>
      - <name>: <type>
      
  attributes:
      - temperature: int
      - humidity: int
      - smoke: bool
```
**Example 1 JSON:**
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
  ]
}
```
**Example 2 Grammar:**


```plaintext
  actions:
      - <name>: <value>
      - <name>: <value>
      
  actions:
    - ef_thermostat_8.temperature:7
    - ef_thermostat_8.state:false
    - ef_thermostat_8.brightness:3
```
**Example 2 JSON:**
```json
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
```

**Example 3 Grammar:**


```plaintext
      
  initial 3, 1
  up 4
  left 9
  down
  right 1
```
**Example 3 JSON:**
```json
  "commands": [
    {
      "name": "commands",
      "parameterStart": null, // There no start Patrern like commands:
      "prefix": "",
      "empty": true,   // As we can see on the down lien there no value
      "delimiter": " ",
      "parameters": ["command", "code"],
      "inputType": "dynamicInputs",
      "placeholder": "Commands",
      "types": ["dropdown", "input"],
      "options": ["initial","up", "down", "left", "right"]
    }
  ]
```
### Patterns and Keywords

Patterns and keywords define the structure of the node type for DSL to graphical transformations.

- **startPattern**: Defines the static starting line of the node type for DSL to graphical transformation. It can be a single pattern or an array of patterns.

**Example JSON for startPattern:**

```json
"startPattern": ["Goal<${goalType}> ${title}", "Goal<${goalType}Area> ${title}"]
```

**Example Grammar:**

```plaintext
Goal<StraightLine> areagoal_1  // goalType=StraightLine , this needs extra cation because overlaps with other nodeTypes startPattrn.
Goal<RectangleArea> areagoal_2  // goalType=Rectangle


```

- **startPatternExceptions**: Specifies exceptions for the general regex pattern created from `startPattern`.

**Example JSON/Grammar for startPatternExceptions:**

**Example 1 Grammar:**


```plaintext
Goal<StraightLine> areagoal_1 
Goal<goalType> title (with exceptions)
```
**Example 1 JSON:**

```json
"startPatternExceptions": [
  {
    "goalType": "StraightLine",
    "order": 1
  },
]
```
**Example 2 Grammar:**


```plaintext
Goal<Pose> pose_1
Goal<Position> position_1
Goal<Orientation> orientation_1
```
**Example 2 JSON:**
```json
"startPatternExceptions": [
				{
					"goalType": "Position"
				},
				{
					"goalType": "Orientation"
				},
				{
					"goalType": "Pose"
				}
			],
```


- **endKeyword**: A keyword indicating the end of a node type.
  - Example: `"endKeyword": "end"`

### Handles

Handles define the connection points between nodes within the React-Flow interface.

- **handles (Optional)**: Defines the handles for connecting nodes. Each handle object can have the following attributes:

  - **type**: Specifies the type of handle, either `source` or `target`.
  - **style**: Defines the visual style of the handle, including properties like `top` (position) and `background` (color).
  - **parameterDependency**: Specifies the dependency parameter that will change its value if a connection is made.
  - **target**: Defines the allowable target nodes for connections.
  - **connectionLimit**: Specifies the connection limits for different target node types.

**Example JSON for Handles:**

```json
"handles": [
				{
					"type": "source",
					"style": { "top": 20, "background": "#00FF00" },
					"parameterDependency": "starts",
					"handleTarget": "automation",
					"connectionLimit": {"automation": "-1", "starts": "-1"}
				},
				{
					"type": "source",
					"style": { "top": 40, "background": "#00FF00" },
					"parameterDependency": "stops",
					"handleTarget": "automation",
					"connectionLimit": {"automation": "-1", "stops": "-1"}
				},
				{
					"type": "source",
					"style": { "top": 60, "background": "#00FF00" },
					"parameterDependency": "after",
					"handleTarget": "automation",
					"connectionLimit": {"automation": "-1", "stops": "-1"}
				},
				{ "type": "target" }
			],
```

**Example Grammar:**

```plaintext
Automation:
    'Automation' name=ID
        (
        ('condition:' condition=Condition)
        ('description:' description=STRING)?
        ('actions:' actions*=Action)?
        ('freq:' freq=INT)?
        ('enabled:' enabled=BOOL)?
        ('continuous:' continuous=BOOL)?
        ('checkOnce:' checkOnce=BOOL)?
        ('delay:' delay=FLOAT)?
        ('starts:' '-' starts*=[Automation:FQN|+pm:automations]['-'])?
        ('stops:' '-' stops*=[Automation:FQN|+pm:automations]['-'])?
        ('after:' '-' after*=[Automation:FQN|+pm:automations]['-'])?
        )#
    'end'
;
AutomationDependency:
    automation=[Automation:FQN|+pm:automations] ('on' exitStatus=BOOL)?
;
```

### Color Configuration

Color configuration defines the visual styling of the connections between nodes to better visualize different node connections .

- **colorConfig**: An object specifying color configurations for the edges connecting nodes.

**Example JSON for Color Configuration:**

```json
"colorConfig": {
  "starts": { "startColor": "#6bbf59", "endColor": "#b0f7a6" },
  "stops": { "startColor": "#d15959", "endColor": "#f7a6a6" },
  "after": { "startColor": "#ff9900", "endColor": "#ffcc66" }
}
```

### Dependencies

Dependencies specify relationships between different node types, used primarily for parameters with autocomplete and dropdown options.

- **dependencies**: An object of objects specifying dependencies with other node types. Each dependency object can have the following attributes:

  - **parameter**: The name of the dependent parameter.
  - **format**: A string format used for complex dependencies.
  - **initFormat**: A string format used to initialize the dependency value.


**Example Grammar:**

```plaintext
Automation:
    'Automation' name=ID
        (
        ('condition:' condition=Condition)
        ('description:' description=STRING)?
        ('actions:' actions*=Action)?
        ('freq:' freq=INT)?
        ('enabled:' enabled=BOOL)?
        ('continuous:' continuous=BOOL)?
        ('checkOnce:' checkOnce=BOOL)?
        ('delay:' delay=FLOAT)?
        ('starts:' '-' starts*=[Automation:FQN|+pm:automations]['-'])?
        ('stops:' '-' stops*=[Automation:FQN|+pm:automations]['-'])?
        ('after:' '-' after*=[Automation:FQN|+pm:automations]['-'])?
        )#
    'end'
;
AutomationDependency:
    automation=[Automation:FQN|+pm:automations] ('on' exitStatus=BOOL)?
;

// === Actions ===
Action:
    FloatAction | IntAction | BoolAction | StringAction | ListAction | DictAction
;

IntAction:
    ('-' attribute=[IntAttribute:FQN|+pm:entities.attributes] ':' value=INT)
;

FloatAction:
    ('-' attribute=[FloatAttribute:FQN|+pm:entities.attributes] ':' value=STRICTFLOAT)
;

StringAction:
    ('-' attribute=[StringAttribute:FQN|+pm:entities.attributes] ':' value=STRING)
;

BoolAction:
    ('-' attribute=[BoolAttribute:FQN|+pm:entities.attributes] ':' value=BOOL)
;

ListAction:
    ('-' attribute=[ListAttribute:FQN|+pm:entities.attributes] ':' value=List)
;

DictAction:
    ('-' attribute=[DictAttribute:FQN|+pm:entities.attributes] ':' value=Dict)
;
```

*So here we undersrand that will need to put on condition will need dependency of the entity sensors, and the actions will need the dependency of the entity actuator, also on the after, starts, stops will need the dependency of the Automation.*

**Example JSON for Dependencies:**

```json
"dependencies": {
  "broker": {
    "parameter": "title"
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

Defines the constraints and rules applied to the node types.

- **maxInstances (Optional)**: Specifies the maximum number of instances of a node type. If `-1`, it is unlimited.
  - Example: `"maxInstances": -1`

- **Duplicate Parameters**: Becarefull to not have duplicate names on the parameters name or on the parameter of the nestedParameter because the algorithm will not know how to identify them.

- **Connection Limits (Handles)**: Specifies connection conditions on how many nodes can be connected is specified in the **handles**. If -1, it is unlimited.
  - Example:
    ```json
    "connectionLimit": {
      "broker": "1",
      "sensor": "-1"
    }
    ```

- **parameterException**: Used if the starting pattern of the node type is the same as another node type and needs a parameter to specify the nodeType we use parameterException. Is required to be first parameter after the startingPattern to catch it early to know how to parse the others parameters.
  - Example: `"parameterException": "entityType"`

### Icons Available:

- HdrAutoIcon
- SensorsIcon
- LeakAddIcon
- PlayForWorkIcon
- SwapHorizIcon
- GroupWorkIcon
- FlagIcon
- AllOutIcon
- SmartToyIcon
- AirlineStopsIcon
- WorkspacesIcon
- EmojiEventsIcon
- CodeIcon
- ControlCameraIcon
- RestartAltIcon
- Default: SensorsIcon (if no match)

**Tips:**
- [View Available Icons](https://mui.com/material-ui/material-icons/)
- You can add more icons in the `src/components/create-graph/utils/transformer_dsl_obj.js` file if necessary.

---

This comprehensive guide provides detailed explanations and examples for configuring the JSON file that represents nodes in React-Flow. Each attribute and its purpose are explained with JSON and grammar examples to help you create accurate and detailed configurations.