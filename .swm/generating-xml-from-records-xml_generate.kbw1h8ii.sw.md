---
title: Generating XML from Records (XML_GENERATE)
---
# Program Overview

This document explains the flow of generating XML from record data (XML-GENERATE-EXAMPLE). The program transforms structured record data into a well-formed XML document using custom mapping rules and displays the result to the user.

```mermaid
flowchart TD
    node1["Generating and Outputting XML from Record Data"] --> node2{"Was XML generated successfully?"}
    click node1 goToHeading "Generating and Outputting XML from Record Data"
    node2 -->|"XML available"|node3["Generating and Outputting XML from Record Data"]
    node2 -->|"Error"|node3
    click node3 goToHeading "Generating and Outputting XML from Record Data"
```

# Program Workflow

# Generating and Outputting XML from Record Data

```mermaid
%%{init: {"flowchart": {"defaultRenderer": "elk"}} }%%
flowchart TD
    node1["Prepare record: name ('Test Name'), value ('Test Value'), enabled flag (true)"] --> node2["Generate XML document (includes XML declaration, maps fields, flag as attribute, suppresses empty fields)"]
    click node1 openCode "xml_generate/xml_generate.cbl:37:39"
    node2 --> node3{"Was XML generated successfully?"}
    click node2 openCode "xml_generate/xml_generate.cbl:41:51"
    node3 -->|"Yes"| node4["Display XML output, trimmed result, character count, and separator"]
    click node3 openCode "xml_generate/xml_generate.cbl:51:56"
    click node4 openCode "xml_generate/xml_generate.cbl:58:63"
    node3 -->|"No"| node5["Display XML generation error"]
    click node5 openCode "xml_generate/xml_generate.cbl:52:53"
    node4 --> node6["End program"]
    click node6 openCode "xml_generate/xml_generate.cbl:64:67"
    node5 --> node6
classDef HeadingStyle fill:#777777,stroke:#333,stroke-width:2px;

%% Swimm:
%% %%{init: {"flowchart": {"defaultRenderer": "elk"}} }%%
%% flowchart TD
%%     node1["Prepare record: name ('Test Name'), value ('Test Value'), enabled flag (true)"] --> node2["Generate XML document (includes XML declaration, maps fields, flag as attribute, suppresses empty fields)"]
%%     click node1 openCode "<SwmPath>[xml_generate/xml_generate.cbl](xml_generate/xml_generate.cbl)</SwmPath>:37:39"
%%     node2 --> node3{"Was XML generated successfully?"}
%%     click node2 openCode "<SwmPath>[xml_generate/xml_generate.cbl](xml_generate/xml_generate.cbl)</SwmPath>:41:51"
%%     node3 -->|"Yes"| node4["Display XML output, trimmed result, character count, and separator"]
%%     click node3 openCode "<SwmPath>[xml_generate/xml_generate.cbl](xml_generate/xml_generate.cbl)</SwmPath>:51:56"
%%     click node4 openCode "<SwmPath>[xml_generate/xml_generate.cbl](xml_generate/xml_generate.cbl)</SwmPath>:58:63"
%%     node3 -->|"No"| node5["Display XML generation error"]
%%     click node5 openCode "<SwmPath>[xml_generate/xml_generate.cbl](xml_generate/xml_generate.cbl)</SwmPath>:52:53"
%%     node4 --> node6["End program"]
%%     click node6 openCode "<SwmPath>[xml_generate/xml_generate.cbl](xml_generate/xml_generate.cbl)</SwmPath>:64:67"
%%     node5 --> node6
%% classDef HeadingStyle fill:#777777,stroke:#333,stroke-width:2px;
```

This section is responsible for transforming record data into a well-formed XML document, applying custom naming conventions, handling empty fields, and reporting the result or any errors to the user.

| Category       | Rule Name                 | Description                                                                                                                                            |
| -------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Business logic | XML Declaration Inclusion | The XML output must include an XML declaration at the beginning of the document.                                                                       |
| Business logic | Custom Field Mapping      | The record's 'name', 'value', and 'enabled' flag must be mapped to XML elements and attributes using custom names: 'name', 'value', and 'enabled'.     |
| Business logic | Flag as Attribute         | The 'enabled' flag must be represented as an XML attribute, not an element.                                                                            |
| Business logic | Suppress Empty Fields     | Any record field that is empty or contains only spaces must be suppressed and not appear in the XML output.                                            |
| Business logic | Result Display            | Upon successful XML generation, the system must display the trimmed XML output, a separator, the character count of the XML, and a completion message. |

<SwmSnippet path="/xml_generate/xml_generate.cbl" line="35">

---

Main-procedure kicks off the flow by populating <SwmToken path="xml_generate/xml_generate.cbl" pos="37:11:13" line-data="           move &quot;Test Name&quot; to ws-record-name">`ws-record`</SwmToken> fields, sets <SwmToken path="xml_generate/xml_generate.cbl" pos="39:3:7" line-data="           set ws-record-flag-enabled to true">`ws-record-flag`</SwmToken> to 'true' using the <SwmToken path="xml_generate/xml_generate.cbl" pos="39:3:9" line-data="           set ws-record-flag-enabled to true">`ws-record-flag-enabled`</SwmToken> condition name, then generates XML from <SwmToken path="xml_generate/xml_generate.cbl" pos="37:11:13" line-data="           move &quot;Test Name&quot; to ws-record-name">`ws-record`</SwmToken> with custom element and attribute names. It handles exceptions, displays the generated XML and its character count, and stops the run. The XML GENERATE statement uses options to control naming and suppress empty fields, and the flag is set using COBOL's idiomatic 88-level condition name for clarity.

```cobol
       main-procedure.

           move "Test Name" to ws-record-name
           move "Test Value" to ws-record-value
           set ws-record-flag-enabled to true

           xml generate ws-xml-output
               from ws-record
               count in ws-xml-char-count
               with xml-declaration
               name of
                   ws-record-name is "name",
                   ws-record-value is "value",
                   ws-record-flag is "enabled"
               type of ws-record-flag is attribute
               suppress when spaces
               on exception
                   display "Error generating xml error " XML-CODE
                   stop run
               not on exception
                   display "XML document successfully generated."
           end-xml

           display "Generated xml for record: " ws-record
           display "----------------------------"
           display function trim(ws-xml-output)
           display "----------------------------"
           display "XML output character count: " ws-xml-char-count
           display "Done."
           stop run.


       end program xml-generate-example.
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ09CT0wtRXhhbXBsZXMlM0ElM0FTd2ltbS1EZW1v" repo-name="COBOL-Examples"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
