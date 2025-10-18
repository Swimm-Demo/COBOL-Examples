---
title: Generating JSON from Records (JSON-GENERATE-EXAMPLE)
---
# Program Overview

This document explains the flow for generating a JSON representation from a COBOL data record (JSON-GENERATE-EXAMPLE). The program prepares a record, converts it to JSON using custom key mappings, and displays both the record and the JSON output for verification.

```mermaid
flowchart TD
    node1["Preparing and Generating JSON Output"]
    click node1 goToHeading "Preparing and Generating JSON Output"
    node1 --> node2{"Was JSON generation successful?"}
    node2 -->|"Yes"|node3["Preparing and Generating JSON Output"]
    node2 -->|"No"|node4["Preparing and Generating JSON Output"]
    click node3 goToHeading "Preparing and Generating JSON Output"
    click node4 goToHeading "Preparing and Generating JSON Output"
```

# Program Workflow

# Preparing and Generating JSON Output

```mermaid
%%{init: {"flowchart": {"defaultRenderer": "elk"}} }%%
flowchart TD
    node1["Prepare record: name='Test Name', value='Test Value', enabled=true"]
    click node1 openCode "json_generate/json_generate.cbl:38:40"
    node1 --> node2["Generate JSON from record"]
    click node2 openCode "json_generate/json_generate.cbl:42:54"
    node2 --> node3{"Was JSON generation successful?"}
    click node3 openCode "json_generate/json_generate.cbl:49:53"
    node3 -->|"Yes"| node4["Display success message"]
    click node4 openCode "json_generate/json_generate.cbl:53:53"
    node4 --> node5["Display record"]
    click node5 openCode "json_generate/json_generate.cbl:56:56"
    node5 --> node6["Display generated JSON and character count"]
    click node6 openCode "json_generate/json_generate.cbl:58:60"
    node6 --> node7["Display 'Done'"]
    click node7 openCode "json_generate/json_generate.cbl:61:62"
    node3 -->|"No"| node8["Display error message and stop process"]
    click node8 openCode "json_generate/json_generate.cbl:50:51"

classDef HeadingStyle fill:#777777,stroke:#333,stroke-width:2px;

%% Swimm:
%% %%{init: {"flowchart": {"defaultRenderer": "elk"}} }%%
%% flowchart TD
%%     node1["Prepare record: name='Test Name', value='Test Value', enabled=true"]
%%     click node1 openCode "<SwmPath>[json_generate/json_generate.cbl](json_generate/json_generate.cbl)</SwmPath>:38:40"
%%     node1 --> node2["Generate JSON from record"]
%%     click node2 openCode "<SwmPath>[json_generate/json_generate.cbl](json_generate/json_generate.cbl)</SwmPath>:42:54"
%%     node2 --> node3{"Was JSON generation successful?"}
%%     click node3 openCode "<SwmPath>[json_generate/json_generate.cbl](json_generate/json_generate.cbl)</SwmPath>:49:53"
%%     node3 -->|"Yes"| node4["Display success message"]
%%     click node4 openCode "<SwmPath>[json_generate/json_generate.cbl](json_generate/json_generate.cbl)</SwmPath>:53:53"
%%     node4 --> node5["Display record"]
%%     click node5 openCode "<SwmPath>[json_generate/json_generate.cbl](json_generate/json_generate.cbl)</SwmPath>:56:56"
%%     node5 --> node6["Display generated JSON and character count"]
%%     click node6 openCode "<SwmPath>[json_generate/json_generate.cbl](json_generate/json_generate.cbl)</SwmPath>:58:60"
%%     node6 --> node7["Display 'Done'"]
%%     click node7 openCode "<SwmPath>[json_generate/json_generate.cbl](json_generate/json_generate.cbl)</SwmPath>:61:62"
%%     node3 -->|"No"| node8["Display error message and stop process"]
%%     click node8 openCode "<SwmPath>[json_generate/json_generate.cbl](json_generate/json_generate.cbl)</SwmPath>:50:51"
%% 
%% classDef HeadingStyle fill:#777777,stroke:#333,stroke-width:2px;
```

This section is responsible for preparing a data record, generating a JSON representation with custom key mappings, and displaying both the record and the JSON output for verification. It also handles error messaging if JSON generation fails.

| Category       | Rule Name                        | Description                                                                                    |
| -------------- | -------------------------------- | ---------------------------------------------------------------------------------------------- |
| Business logic | Display JSON and character count | The generated JSON string and its character count must be displayed for verification purposes. |

<SwmSnippet path="/json_generate/json_generate.cbl" line="36">

---

Main-procedure kicks off the flow by setting up <SwmToken path="json_generate/json_generate.cbl" pos="38:11:13" line-data="           move &quot;Test Name&quot; to ws-record-name">`ws-record`</SwmToken> with fixed values and enabling the flag. Then it generates a JSON string from <SwmToken path="json_generate/json_generate.cbl" pos="38:11:13" line-data="           move &quot;Test Name&quot; to ws-record-name">`ws-record`</SwmToken>, mapping COBOL field names to custom JSON keys using the NAME OF clause. After that, it prints the record, the JSON output, and its character count for verification. If JSON generation fails, it displays an error and stops.

```cobol
       main-procedure.

           move "Test Name" to ws-record-name
           move "Test Value" to ws-record-value
           set ws-record-flag-enabled to true

           json generate ws-json-output
               from ws-record
               count in ws-json-char-count
               name of
                   ws-record-name is "name",
                   ws-record-value is "value",
                   ws-record-flag is "enabled"
               on exception
                   display "Error generating JSON error " JSON-CODE
                   stop run
               not on exception
                   display "JSON document successfully generated."
           end-json

           display "Generated JSON for record: " ws-record
           display "----------------------------"
           display function trim(ws-json-output)
           display "----------------------------"
           display "JSON output character count: " ws-json-char-count
           display "Done."
           stop run.


       end program json-generate-example.
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ09CT0wtRXhhbXBsZXMlM0ElM0FTd2ltbS1EZW1v" repo-name="COBOL-Examples"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
