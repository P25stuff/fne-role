# FNE Ansible Role

## Description

Opinionated Ansible role to install the DVM Project FNE.

## Requirements

Debian or Ubuntu based system, `apt`, and an AMD64, ARM64 or ARM32 CPU.

## Role Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `install` | Set this variable to install/reinstall the DVM Project FNE to the host. This might be useful to turn off if you use the role to regenerate the configs. | `true` | No |
| `use_netbird` | Set this to true if Netbird is installed on the host | `false` | No |
| `dvm_folder` | Set this variable to use a custom folder name throughout the role | `dvm` | Yes |
| `dvmprov` | Set this variable to install the DVM Provisioning Manager to the FNE host | `true` | No |
| `rebuild` | Set this variable to force a rebuild using the GitHub action.  Rebuild will happen if the `dvmhost` project had changes since the last action run. *GitHub token is mandatory.* | `false` | No |
| `force_rebuild` | Set this variable to force the GitHub action to rebuild, regardless of whether the `dvmhost` project had changes since the last action run.  **`rebuild` *must* be set to `true` for this variable to be considered.** *GitHub token is mandatory.* | `false` | No |

## Limitations

It is **highly recommended** to set `install` to `true` if you make configuration changes, as it is possible the underlying binary has had changes.

## Example Playbook

*Please refer to the [ansible-deploy repo](https://github.com/p25stuff/ansible-deploy/) for a detailed playbook.*

The role is configured in a way every single configuration item can be overridden by defining the appropriate variable, while maintaining most default values as a baseline.  See the table below for a list of required FNE variables.  In the `ansible-deploy` repo, those variables are provided in the `group_vars/all.yml` and `host_vars/fne.hostname.yml` files.  These can contain any variation of the variables to be defined (or any other accepted way to provide variables to Ansible).

In addition, this role expects files for RIDs, talkgroups, and peerlist (if applicable).  The information can be provided in any way, but for security purposes, the `ansible-deploy` repo relies on the info being in a private repository - [provided as an example](https://github.com/p25stuff/system-info/) in public form.

The role will create a new directory at `./local_backups/fne/` and copy the generated configs locally upon running.

### FNE Important Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `dvm_folder` | Set this variable to use a custom folder name throughout the role | `dvm` | Yes |
| `peerId` | FNE Network Peer ID | None | Yes |
| `fne_port` | Port number for the FNE to listen on | None | Yes |
| `fne_password` | FNE Access Password | None | Yes |

Some variables are also required for peered FNEs.  Please refer to the [template](/templates/configs/configFNE.yml.j2) and the [dvmhost configuration example](https://github.com/DVMProject/dvmhost/blob/master/configs/fne-config.example.yml).
