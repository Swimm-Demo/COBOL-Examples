---
title: Reading Command Line Arguments (READ_CMD_LINE_ARGS)
---
# Program Overview

This document describes the flow for processing <SwmToken path="read_command_args/read_cmd_line_args.cbl" pos="22:11:13" line-data="           accept ws-cmd-args from command-line">`command-line`</SwmToken> arguments (READ_CMD_LINE_ARGS). The program displays instructions, shows all received arguments, and provides a special message if the '--test' flag is present.

```mermaid
flowchart TD
    node1["Processing Command-Line Arguments"] --> node2{"Was '--test' argument provided?"}
    click node1 goToHeading "Processing Command-Line Arguments"
    click node2 goToHeading "Processing Command-Line Arguments"
    node2 -->|"Yes"| node3["Processing Command-Line Arguments"]
    click node3 goToHeading "Processing Command-Line Arguments"
    node2 -->|"No"| node3
    click node3 goToHeading "Processing Command-Line Arguments"
```

# Program Workflow

# Processing Command-Line Arguments

```mermaid
%%{init: {"flowchart": {"defaultRenderer": "elk"}} }%%
flowchart TD
    node1["Display instructions to user"] --> node2["Read command-line arguments"]
    click node1 openCode "read_command_args/read_cmd_line_args.cbl:19:20"
    node2 --> node6["Display all command-line arguments"]
    click node2 openCode "read_command_args/read_cmd_line_args.cbl:22:23"
    node6 --> node3{"Was '--test' argument provided?"}
    click node6 openCode "read_command_args/read_cmd_line_args.cbl:23:25"
    node3 -->|"Yes"| node4["Display special message"]
    click node3 openCode "read_command_args/read_cmd_line_args.cbl:29:30"
    node3 -->|"No"| node5["Skip special message"]
    click node5 openCode "read_command_args/read_cmd_line_args.cbl:31:32"
    node4 --> node7["Display blank line"]
    click node4 openCode "read_command_args/read_cmd_line_args.cbl:33:34"
    node5 --> node7
    click node7 openCode "read_command_args/read_cmd_line_args.cbl:33:34"
    node7 --> node8["End program"]
    click node8 openCode "read_command_args/read_cmd_line_args.cbl:35:35"

classDef HeadingStyle fill:#777777,stroke:#333,stroke-width:2px;

%% Swimm:
%% %%{init: {"flowchart": {"defaultRenderer": "elk"}} }%%
%% flowchart TD
%%     node1["Display instructions to user"] --> node2["Read <SwmToken path="read_command_args/read_cmd_line_args.cbl" pos="22:11:13" line-data="           accept ws-cmd-args from command-line">`command-line`</SwmToken> arguments"]
%%     click node1 openCode "<SwmPath>[read_command_args/read_cmd_line_args.cbl](read_command_args/read_cmd_line_args.cbl)</SwmPath>:19:20"
%%     node2 --> node6["Display all <SwmToken path="read_command_args/read_cmd_line_args.cbl" pos="22:11:13" line-data="           accept ws-cmd-args from command-line">`command-line`</SwmToken> arguments"]
%%     click node2 openCode "<SwmPath>[read_command_args/read_cmd_line_args.cbl](read_command_args/read_cmd_line_args.cbl)</SwmPath>:22:23"
%%     node6 --> node3{"Was '--test' argument provided?"}
%%     click node6 openCode "<SwmPath>[read_command_args/read_cmd_line_args.cbl](read_command_args/read_cmd_line_args.cbl)</SwmPath>:23:25"
%%     node3 -->|"Yes"| node4["Display special message"]
%%     click node3 openCode "<SwmPath>[read_command_args/read_cmd_line_args.cbl](read_command_args/read_cmd_line_args.cbl)</SwmPath>:29:30"
%%     node3 -->|"No"| node5["Skip special message"]
%%     click node5 openCode "<SwmPath>[read_command_args/read_cmd_line_args.cbl](read_command_args/read_cmd_line_args.cbl)</SwmPath>:31:32"
%%     node4 --> node7["Display blank line"]
%%     click node4 openCode "<SwmPath>[read_command_args/read_cmd_line_args.cbl](read_command_args/read_cmd_line_args.cbl)</SwmPath>:33:34"
%%     node5 --> node7
%%     click node7 openCode "<SwmPath>[read_command_args/read_cmd_line_args.cbl](read_command_args/read_cmd_line_args.cbl)</SwmPath>:33:34"
%%     node7 --> node8["End program"]
%%     click node8 openCode "<SwmPath>[read_command_args/read_cmd_line_args.cbl](read_command_args/read_cmd_line_args.cbl)</SwmPath>:35:35"
%% 
%% classDef HeadingStyle fill:#777777,stroke:#333,stroke-width:2px;
```

This section governs how <SwmToken path="read_command_args/read_cmd_line_args.cbl" pos="22:11:13" line-data="           accept ws-cmd-args from command-line">`command-line`</SwmToken> arguments are processed, displayed, and how special flags like '--test' trigger additional messaging for the user.

| Category       | Rule Name                    | Description                                                                                                                                                                                                                                                                |
| -------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Business logic | User instruction prompt      | Always display instructions to the user indicating that passing '--test' will result in a special message.                                                                                                                                                                 |
| Business logic | Show raw arguments           | Display all <SwmToken path="read_command_args/read_cmd_line_args.cbl" pos="22:11:13" line-data="           accept ws-cmd-args from command-line">`command-line`</SwmToken> arguments exactly as received from the user.                                                    |
| Business logic | Special message for '--test' | If the '--test' argument is present in the <SwmToken path="read_command_args/read_cmd_line_args.cbl" pos="22:11:13" line-data="           accept ws-cmd-args from command-line">`command-line`</SwmToken> input (case-insensitive), display a special message to the user. |
| Business logic | End with blank line          | After processing <SwmToken path="read_command_args/read_cmd_line_args.cbl" pos="22:11:13" line-data="           accept ws-cmd-args from command-line">`command-line`</SwmToken> arguments and any special messages, always display a blank line before ending the program. |

<SwmSnippet path="/read_command_args/read_cmd_line_args.cbl" line="18">

---

In <SwmToken path="read_command_args/read_cmd_line_args.cbl" pos="18:1:3" line-data="       main-procedure.">`main-procedure`</SwmToken>, we kick off by displaying a prompt about the '--test' argument, then grab the full <SwmToken path="read_command_args/read_cmd_line_args.cbl" pos="22:11:13" line-data="           accept ws-cmd-args from command-line">`command-line`</SwmToken> input into <SwmToken path="read_command_args/read_cmd_line_args.cbl" pos="22:3:7" line-data="           accept ws-cmd-args from command-line">`ws-cmd-args`</SwmToken>. We show the raw arguments, convert them to lowercase, and use INSPECT with TALLYING to count how many times '--test' appears. This sets up the logic for handling special <SwmToken path="read_command_args/read_cmd_line_args.cbl" pos="22:11:13" line-data="           accept ws-cmd-args from command-line">`command-line`</SwmToken> flags.

```cobol
       main-procedure.
           display space
           display "Pass arg '--test' for special message".

           accept ws-cmd-args from command-line
           display "Full command line args: " ws-cmd-args

           inspect function lower-case(ws-cmd-args)
               tallying ws-test-arg-count
               for all "--test"
```

---

</SwmSnippet>

<SwmSnippet path="/read_command_args/read_cmd_line_args.cbl" line="29">

---

If '--test' is found, we show a special message, then end the program.

```cobol
           if ws-test-arg-count > 0 then
               display "You entered the '--test' cmd arg!"
           end-if

           display space

           stop run.
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ09CT0wtRXhhbXBsZXMlM0ElM0FTd2ltbS1EZW1v" repo-name="COBOL-Examples"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
