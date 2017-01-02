Ansible Nagios Plugins Role
===========================

This [Ansible](http://www.ansible.com/home) role supports the deployment and configuration of the Nagios plugins agent where the agent will be built from source.

## Table of Contents

* [Supported Platforms](#supported-platforms)
* [User Manual](#user-manual)
  * [Basic usage](#basic-usage)
  * [Alternative source download location](#alternative-source-download-location)
  * [Plugins version management](#plugins-version-management)
* [Configuration](#configuration)
  * [Configurable variables](#configurable-variables)

## Supported Platforms

See [meta info](meta/main.yml).

## User Manual

### Basic usage

* Configure this role as ansible-galaxy dependency (e.g. requirements.yml)
* Add the following lines to your Ansible playbook's role section (sample):
```
roles:
  - role: "ansible-nagios-plugins"
    ansible_nagios_plugins_plugin_version: "2.1.1"
```
* This will instruct the role to install the Nagios plugins, assuming the NRPE agent has already been installed (see [Ansible NRPE Role](https://github.com/polster/ansible-nagios-nrpe))

### Alternative source download location

* By default, this role will try to download the needed Nagios plugin sources from the official [Nagios Github repo](https://github.com/nagios-plugins)
* In case you need to provide the sources on an internal repo server, this is doable by simply overriding the following variable:
```
roles:
  - role: "ansible-nagios-plugins"
    ansible_nagios_plugins_plugin_version: "2.1.1"
    ansible_nagios_plugins_download_url: "https://repo.example.com/path/to/plugins/sources"
```
* Where the implementation will expect the download file to be in the following format:
```
https://repo.example.com/path/to/plugins/sources/release-{{ ansible_nagios_plugins_version }}.tar.gz
```

### Plugins version management

* Being executed for the first time, this role will create a self managed version file on each target host:
```
{{ ansible_nagios_plugins_nagios_path }}/nagios-plugins.version
```
* Next time the role will be executed, the currently installed version will be fetched and compared against the value being defined by the variable {{ ansible_nagios_plugins_version }}
* In case of a mismatch, the role will try to install the version as defined by the variable {{ ansible_nagios_plugins_version }}

## Configuration

### Configurable variables

See [defaults](defaults/main.yml).
