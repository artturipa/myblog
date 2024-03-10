## Data resources for dummies
Data resources connect your UI Components to data structures that are in tables. By using data structures, one can develop components that can be used on variety of use cases. It does not matter what is the data structure in database, as data resources can query required data and transform it into valid form for the component. 

### Create New new data resource

1. UI Builder / Data Resources / New / Transform (most common data resource type)
2. Fill fields as below:
**Properties:** __can be empty as well__
    [
        {
            "name":"inputParameter",
            "label": "label to show in UI Builder",
            "description": "Description to show in UI Builder",
            "readOnly": false,
            "fieldType": "string",
            "mandatory":true,
            "defaultValue": "default value to show in UI Builder"
        }
    ]
**Script:**
    function transform(input) {
        var givenParameterValue = input.inputParameter;
        /* Good practice is to put heavier functions to dedicated Script Include */
        return givenParameterValue;
    }

3. Set up required ACL:
    * Type: ux_data_broker
    * Operation: Execute
    * Name: sys_id of sys_ux_data_broker -record created earlier (note that ACL form might show name in composite form that does not allow one to put sys_id there, then it can be set via background script.)
