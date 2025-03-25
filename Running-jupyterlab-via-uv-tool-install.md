# Running jupyterlab via uv tool install

Simon Willison's TILs
[Running jupyterlab via uv tool install](https://til.simonwillison.net/jupyter/jupyterlab-uv-tool-install)

## Some notes on the uv tool

[uv - An extremely fast Python package and project manager, written in Rust.](https://docs.astral.sh/uv/)

**Installation**

Windows - 

`powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"`

Linux - 

`curl -LsSf https://astral.sh/uv/install.sh | sh`
(On WSL2 on Windows 11 Ubuntu 22.04)

This has added advantage that you can upgrade uv through itself - `uv self update`

Simply typing uv on the command line gives this:

`
PS C:\Users\shish\OneDrive\डॉक्यूमेंट्स\GitHub\notes-2025> uv

An extremely fast Python package manager.

Usage: uv.exe [OPTIONS] <COMMAND> 

and a long list of commands:`

Extra information is given by `uv help` - same as  above

**Shell autocompletion:** 

Very useful in day to day work

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

First clean up stored data(optional):

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

When used, it gives:

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

`jupyterlab`is already installed`

So tried with his formula:

`S C:\Users\shish\OneDrive\डॉक्यूमेंट्स\GitHub\notes-2025> uv touv tool install jupyterlab --force

Resolved 92 packages in 43ms

Uninstalled 1 package in 98ms

Installed 1 package in 396ms

 ~ jupyterlab==4.3.6

Installed 4 executables: jlpm.exe, jupyter-lab.exe, jupyter-labextension.exe, jupyter-labhub.exe`

Then start jupyterlab with
`jupyter-lab`
---------------------------------------------------------

## Getting %pip to work

Simon notes that getting `%pip install llm` to work -

"This was the biggest sticking point for me. Jupyter has a useful magic command for installing packages:

%pip install llm

When I tried to run this I got this error:

/Users/simon/.local/share/uv/tools/jupyterlab/bin/python: No module named pip

It turns out we have an installation with no pip binary."


Simon found that

There may be a better way to do this, but he found that this worked, 

run in a Jupyter notebook cell:

import subprocess, sys

subprocess.check_call([sys.executable, "-m", "ensurepip"])

After he ran this, the %pip magic command worked as expected - I didn't even need to restart the kernel

**I was unable to run this command as for now.**

In our trial, we got:

`%pip install llm`

%pip: The term '%pip' is not recognized as a name of a cmdlet, function, script file, or executable program.
Check the spelling of the name, or if a path was included, verify that the path is correct and try again.`

Let us get to the doumentation of this magic command.

