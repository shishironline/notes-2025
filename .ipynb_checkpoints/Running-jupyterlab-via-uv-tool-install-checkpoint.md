# Running jupyterlab via uv tool install

Simon Willison's TILs
[Running jupyterlab via uv tool install](https://til.simonwillison.net/jupyter/jupyterlab-uv-tool-install)

## Some note on the uv tool

[uv - An extremely fast Python package and project manager, written in Rust.](https://docs.astral.sh/uv/)

**Installation**
Windows - `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"`
Linux - `curl -LsSf https://astral.sh/uv/install.sh | sh`
(On WSL2 on Windows 11 Ubuntu 22.04)

This has added advantage that you can upgrade uv through itself - `uv self update`

Simply typing uv on the command line gives this:

`
PS C:\Users\shish\OneDrive\डॉक्यूमेंट्स\GitHub\notes-2025> uv

An extremely fast Python package manager.

Usage: uv.exe [OPTIONS] <COMMAND>

Commands:
  run      Run a command or script
  init     Create a new project
  add      Add dependencies to the project
  remove   Remove dependencies from the project
  sync     Update the project's environment
  lock     Update the project's lockfile
  export   Export the project's lockfile to an alternate format
  tree     Display the project's dependency tree
  tool     Run and install commands provided by Python packages
  python   Manage Python versions and installations
  pip      Manage Python packages with a pip-compatible interface
  venv     Create a virtual environment
  build    Build Python packages into source distributions and wheels
  publish  Upload distributions to an index
  cache    Manage uv's cache
  self     Manage the uv executable
  version  Display uv's version
  help     Display documentation for a command

Cache options:
  -n, --no-cache               Avoid reading from or writing to the cache, instead using a temporary directory for the duration of the operation [env:
                               UV_NO_CACHE=]
      --cache-dir <CACHE_DIR>  Path to the cache directory [env: UV_CACHE_DIR=]

Python options:
      --managed-python       Require use of uv-managed Python versions [env: UV_MANAGED_PYTHON=]
      --no-managed-python    Disable use of uv-managed Python versions [env: UV_NO_MANAGED_PYTHON=]
      --no-python-downloads  Disable automatic downloads of Python. [env: "UV_PYTHON_DOWNLOADS=never"]

Global options:
  -q, --quiet                                      Do not print any output
  -v, --verbose...                                 Use verbose output
      --color <COLOR_CHOICE>                       Control the use of color in output [possible values: auto, always, never]
      --native-tls                                 Whether to load TLS certificates from the platform's native certificate store [env: UV_NATIVE_TLS=]
      --offline                                    Disable network access [env: UV_OFFLINE=]
      --allow-insecure-host <ALLOW_INSECURE_HOST>  Allow insecure connections to a host [env: UV_INSECURE_HOST=]
      --no-progress                                Hide all progress outputs [env: UV_NO_PROGRESS=]
      --directory <DIRECTORY>                      Change to the given directory prior to running the command
      --project <PROJECT>                          Run the command within the given project directory
      --config-file <CONFIG_FILE>                  The path to a `uv.toml` file to use for configuration [env: UV_CONFIG_FILE=]
      --no-config                                  Avoid discovering configuration files (`pyproject.toml`, `uv.toml`) [env: UV_NO_CONFIG=]
  -h, --help                                       Display the concise help for this command
  -V, --version                                    Display the uv version

Use `uv help` for more details.
PS C:\Users\shish\OneDrive\डॉक्यूमेंट्स\GitHub\notes-2025>`

Let us see what extra information is given by `uv help` - same as  above

**Shell autocompletion:** Very useful in day to day work

Bash: `echo 'eval "$(uv generate-shell-completion bash)"' >> ~/.bashrc`
for uvx: `echo 'eval "$(uvx --generate-shell-completion bash)"' >> ~/.bashrc`
Restart your shell or source your config file: `source ~/.bashrc`

Powershell: `if (!(Test-Path -Path $PROFILE)) {
  New-Item -ItemType File -Path $PROFILE -Force
}
Add-Content -Path $PROFILE -Value '(& uv generate-shell-completion powershell) | Out-String | Invoke-Expression'`

For uvx: `if (!(Test-Path -Path $PROFILE)) {
  New-Item -ItemType File -Path $PROFILE -Force
}
Add-Content -Path $PROFILE -Value '(& uvx --generate-shell-completion powershell) | Out-String | Invoke-Expression'`

Restart your shell or source your config file.

**Uninstallation:**
Clean up stored data:
`uv cache clean
rm -r "$(uv python dir)"
rm -r "$(uv tool dir)"`

Linux: `rm ~/.local/bin/uv ~/.local/bin/uvx`
Windows: `$ rm $HOME\.local\bin\uv.exe
$ rm $HOME\.local\bin\uvx.exe`

## uv tool install jupyterlab

`uv tool install jupyterlab`
Installed 4 executables: jlpm.exe, jupyter-lab.exe, jupyter-labextension.exe, jupyter-labhub.exe

Simon had a warning about PATH
So he used `uv tool ensure-path`
When used, it fives:
`uv tool ensure-path
error: unrecognized subcommand 'ensure-path'

  tip: a similar subcommand exists: 'ensurepath'`

On running
`uv tool ensurepath 
Executable directory C:\Users\shish\.local\bin is already in PATH`

Let us see the contents of ~/.local/bin
`ls ~/.local/bin

    Directory: C:\Users\shish\.local\bin

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a---           3/25/2025  8:26 AM          40998 jlpm.exe
-a---           3/25/2025  8:26 AM          40997 jupyter-lab.exe
-a---           3/25/2025  8:26 AM          41004 jupyter-labextension.exe
-a---           3/25/2025  8:26 AM          41000 jupyter-labhub.exe
-a---           3/20/2025  9:04 PM       48523264 uv.exe
-a---           3/20/2025  9:04 PM         335872 uvx.exe`

Simon also faced a problem on one of his machines because it refused to overwrite older installation, which he fixed with
`uv tool install jupyterlab --force`

When we try it:
`uv tool install jupyterlab
`jupyterlab` is already installed`

So tried with his formula:
`S C:\Users\shish\OneDrive\डॉक्यूमेंट्स\GitHub\notes-2025> uv touv tool install jupyterlab --force
Resolved 92 packages in 43ms                                                                                                                                           
Uninstalled 1 package in 98ms
Installed 1 package in 396ms
 ~ jupyterlab==4.3.6
Installed 4 executables: jlpm.exe, jupyter-lab.exe, jupyter-labextension.exe, jupyter-labhub.exe`

Then he started jupyterlab with
`jupyter-lab`
