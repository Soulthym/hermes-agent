# Development Install of the Gossip Hermes Fork

These instructions install the `feat/gossip-platform` branch from the
`Soulthym/hermes-agent` fork for local development.

## Ubuntu

### Prerequisites

```bash
sudo apt update
sudo apt install -y git curl build-essential nodejs npm python3
```

Install Hermes once with the official installer if `~/.hermes/bin/uv` does not
already exist:

```bash
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
```

### Clone the fork

```bash
git clone --branch feat/gossip-platform https://github.com/Soulthym/hermes-agent.git
cd hermes-agent
```

### Install Hermes in editable mode

Use the `uv` binary managed by Hermes, not a globally installed `uv`:

```bash
~/.hermes/bin/uv pip install -e ".[all,dev]"
```

This keeps the `hermes` command wired to the editable checkout, so changes made
in this repository are picked up without reinstalling the package.

If your shell cannot find `hermes`, add the Hermes bin directory to `PATH`:

```bash
export PATH="$HOME/.hermes/bin:$PATH"
```

### Install the Gossip sidecar dependencies

The Gossip integration uses the published npm package
`@massalabs/gossip-sdk`.

```bash
npm --prefix plugins/platforms/gossip/sidecar install
```

### Verify the development install

```bash
which hermes
hermes --help
```

`which hermes` should resolve under `~/.hermes/bin`.

## Windows

These commands are intended for PowerShell.

### Prerequisites

Install Git if it is not already available:

```powershell
winget install --id Git.Git
```

Install Hermes once with the official Windows installer if
`$env:LOCALAPPDATA\hermes\bin\uv.exe` does not already exist:

```powershell
iex (irm https://hermes-agent.nousresearch.com/install.ps1)
```

Restart PowerShell after the installer finishes.

### Clone the fork

```powershell
git clone --branch feat/gossip-platform https://github.com/Soulthym/hermes-agent.git
cd hermes-agent
```

### Install Hermes in editable mode

Use the `uv.exe` binary managed by Hermes, not a globally installed `uv`:

```powershell
& "$env:LOCALAPPDATA\hermes\bin\uv.exe" pip install -e ".[all,dev]"
```

This keeps the `hermes` command wired to the editable checkout, so changes made
in this repository are picked up without reinstalling the package.

If PowerShell cannot find `hermes`, add the Hermes bin directory to `PATH` for
the current session:

```powershell
$env:Path = "$env:LOCALAPPDATA\hermes\bin;$env:Path"
```

### Install the Gossip sidecar dependencies

```powershell
npm --prefix plugins/platforms/gossip/sidecar install
```

### Verify the development install

```powershell
Get-Command hermes
hermes --help
```

`Get-Command hermes` should resolve under
`$env:LOCALAPPDATA\hermes\bin`.

## Configure Gossip

Run the gateway setup and select `gossip` when prompted:

```bash
hermes gateway setup
```

During setup, Hermes will ask for the Gossip ID of the admin user. The Gossip
integration only replies to text DMs from that admin ID.

After setup, start or install the gateway service:

```bash
hermes gateway start
```

or:

```bash
hermes gateway install
```

## Check logs

```bash
hermes logs
```
