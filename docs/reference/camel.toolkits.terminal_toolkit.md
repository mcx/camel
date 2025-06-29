<a id="camel.toolkits.terminal_toolkit"></a>

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit"></a>

## TerminalToolkit

```python
class TerminalToolkit(BaseToolkit):
```

A toolkit for terminal operations across multiple operating systems.

This toolkit provides a set of functions for terminal operations such as
searching for files by name or content, executing shell commands, and
managing terminal sessions.

**Parameters:**

- **timeout** (Optional[float]): The timeout for terminal operations.
- **shell_sessions** (Optional[Dict[str, Any]]): A dictionary to store shell session information. If None, an empty dictionary will be used. (default: :obj:`{}`)
- **working_dir** (str): The working directory for operations. If specified, all execution and write operations will be restricted to this directory. Read operations can access paths outside this directory.(default: :obj:`"./workspace"`)
- **need_terminal** (bool): Whether to create a terminal interface. (default: :obj:`True`)
- **use_shell_mode** (bool): Whether to use shell mode for command execution. (default: :obj:`True`)
- **clone_current_env** (bool): Whether to clone the current Python environment.(default: :obj:`False`)
- **safe_mode** (bool): Whether to enable safe mode to restrict operations. (default: :obj:`True`)

**Note:**

Most functions are compatible with Unix-based systems (macOS, Linux).
For Windows compatibility, additional implementation details are
needed.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit.__init__"></a>

### __init__

```python
def __init__(
    self,
    timeout: Optional[float] = None,
    shell_sessions: Optional[Dict[str, Any]] = None,
    working_dir: str = './workspace',
    need_terminal: bool = True,
    use_shell_mode: bool = True,
    clone_current_env: bool = False,
    safe_mode: bool = True
):
```

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit._setup_file_output"></a>

### _setup_file_output

```python
def _setup_file_output(self):
```

Set up file output to replace GUI, using a fixed file to simulate
terminal.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit._clone_current_environment"></a>

### _clone_current_environment

```python
def _clone_current_environment(self):
```

Create a new Python virtual environment.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit._create_terminal"></a>

### _create_terminal

```python
def _create_terminal(self):
```

Create a terminal GUI. If GUI creation fails, fallback
to file output.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit._update_terminal_output"></a>

### _update_terminal_output

```python
def _update_terminal_output(self, output: str):
```

Update terminal output and send to agent.

**Parameters:**

- **output** (str): The output to be sent to the agent

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit._is_path_within_working_dir"></a>

### _is_path_within_working_dir

```python
def _is_path_within_working_dir(self, path: str):
```

Check if the path is within the working directory.

**Parameters:**

- **path** (str): The path to check

**Returns:**

  bool: Returns True if the path is within the working directory,
otherwise returns False

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit._enforce_working_dir_for_execution"></a>

### _enforce_working_dir_for_execution

```python
def _enforce_working_dir_for_execution(self, path: str):
```

Enforce working directory restrictions, return error message
if execution path is not within the working directory.

**Parameters:**

- **path** (str): The path to be used for executing operations

**Returns:**

  Optional[str]: Returns error message if the path is not within
the working directory, otherwise returns None

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit._copy_external_file_to_workdir"></a>

### _copy_external_file_to_workdir

```python
def _copy_external_file_to_workdir(self, external_file: str):
```

Copy external file to working directory.

**Parameters:**

- **external_file** (str): The path of the external file

**Returns:**

  Optional[str]: New path after copying to the working directory,
returns None on failure

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit.file_find_in_content"></a>

### file_find_in_content

```python
def file_find_in_content(
    self,
    file: str,
    regex: str,
    sudo: bool = False
):
```

Search for matching text within file content.

**Parameters:**

- **file** (str): Absolute path of the file to search within.
- **regex** (str): Regular expression pattern to match.
- **sudo** (bool, optional): Whether to use sudo privileges. Defaults to False. Note: Using sudo requires the process to have appropriate permissions.

**Returns:**

  str: Matching content found in the file.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit.file_find_by_name"></a>

### file_find_by_name

```python
def file_find_by_name(self, path: str, glob: str):
```

Find files by name pattern in specified directory.

**Parameters:**

- **path** (str): Absolute path of directory to search.
- **glob** (str): Filename pattern using glob syntax wildcards.

**Returns:**

  str: List of files matching the pattern.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit._sanitize_command"></a>

### _sanitize_command

```python
def _sanitize_command(self, command: str, exec_dir: str):
```

Check and modify command to ensure safety.

**Parameters:**

- **command** (str): The command to check
- **exec_dir** (str): The directory to execute the command in

**Returns:**

  Tuple: (is safe, modified command or error message)

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit.shell_exec"></a>

### shell_exec

```python
def shell_exec(self, id: str, command: str):
```

Execute commands. This can be used to execute various commands,
such as writing code, executing code, and running commands.

**Parameters:**

- **id** (str): Unique identifier of the target shell session.
- **command** (str): Shell command to execute.

**Returns:**

  str: Output of the command execution or error message.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit.shell_view"></a>

### shell_view

```python
def shell_view(self, id: str):
```

View the content of a specified shell session.

**Parameters:**

- **id** (str): Unique identifier of the target shell session.

**Returns:**

  str: Current output content of the shell session.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit.shell_wait"></a>

### shell_wait

```python
def shell_wait(self, id: str, seconds: Optional[int] = None):
```

Wait for the running process in a specified shell session to
return.

**Parameters:**

- **id** (str): Unique identifier of the target shell session.
- **seconds** (Optional[int], optional): Wait duration in seconds. If None, wait indefinitely. Defaults to None.

**Returns:**

  str: Final output content after waiting.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit.shell_write_to_process"></a>

### shell_write_to_process

```python
def shell_write_to_process(
    self,
    id: str,
    input: str,
    press_enter: bool
):
```

Write input to a running process in a specified shell session.

**Parameters:**

- **id** (str): Unique identifier of the target shell session.
- **input** (str): Input content to write to the process.
- **press_enter** (bool): Whether to press Enter key after input.

**Returns:**

  str: Status message indicating whether the input was sent.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit.shell_kill_process"></a>

### shell_kill_process

```python
def shell_kill_process(self, id: str):
```

Terminate a running process in a specified shell session.

**Parameters:**

- **id** (str): Unique identifier of the target shell session.

**Returns:**

  str: Status message indicating whether the process was terminated.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit.ask_user_for_help"></a>

### ask_user_for_help

```python
def ask_user_for_help(self, id: str):
```

Pauses agent execution to ask a human for help in the terminal.

This function should be called when an agent is stuck or needs
assistance with a task that requires manual intervention (e.g.,
solving a CAPTCHA or complex debugging). The human will take over the
specified terminal session to execute commands and then return control
to the agent.

**Parameters:**

- **id** (str): Identifier of the shell session for the human to interact with. If the session does not yet exist, it will be created automatically.

**Returns:**

  str: A status message indicating that the human has finished,
including the number of commands executed.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit.__del__"></a>

### __del__

```python
def __del__(self):
```

Clean up resources when the object is being destroyed.
Terminates all running processes and closes any open file handles.

<a id="camel.toolkits.terminal_toolkit.TerminalToolkit.get_tools"></a>

### get_tools

```python
def get_tools(self):
```

**Returns:**

  List[FunctionTool]: A list of FunctionTool objects representing the
functions in the toolkit.
