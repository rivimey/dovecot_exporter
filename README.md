Ansible Role: dovecot\_exporter
==========================

[![Build Status](https://travis-ci.org/atosatto/ansible-dovecot_exporter.svg?branch=master)](https://travis-ci.org/atosatto/ansible-dovecot_exporter)
[![Galaxy](https://img.shields.io/badge/galaxy-atosatto.dovecot_exporter-blue.svg?style=flat-square)](https://galaxy.ansible.com/atosatto/dovecot_exporter)

Install and configure Prometheus dovecot\_exporter.

Requirements
------------

An Ansible 2.2 or higher installation.<br />
This role makes use of the Ansible `json_filter` that requires `jmespath` to be installed on the Ansible machine.
See the `requirements.txt` file for further details on the specific version of `jmespath` required by the role.

Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml):

    dovecot_exporter_release_tag: "latest"

The dovecot\_exporter release to be installed.
By default, the latest release published at https://github.com/prometheus/dovecot\_exporter/releases.

    dovecot_exporter_release_url: ""

If set, the role will download dovecot-exporter from the provided URL instead of using the download URL indicated in the dovecot\_exporter Github release metadata.

    dovecot_exporter_user: "dovecot_exporter"
    dovecot_exporter_group: "dovecot_exporter"

dovecot\_exporter system user and group.

    dovecot_exporter_install_path: "/opt"

Directory containing the downloaded dovecot\_exporter release artifacts.

    dovecot_exporter_bin_path: "/usr/local/bin"

Directory to which the dovecot\_exporter binaries will be symlinked.

    dovecot_exporter_listen_address: "127.0.0.1:9100"

The dovecot\_exporter WebServer listen ip address and port.<br/>
**NOTE**: the dovecot\_exporter metrics will be available at `{{ dovecot_exporter_listen_address }}/metrics`.

    dovecot_exporter_log_level: "info"

dovecot\_exporter logs verbosity level.

    dovecot_exporter_collector_textfile_path: "/var/lib/dovecot_exporter/textfile-collector/"

Directory used by the dovecot\_exporter's textfile collector to look for `*.prom` metrics files to be
exposed by the exporter.
See https://github.com/prometheus/dovecot_exporter#textfile-collector.

    dovecot_exporter_additional_cli_args: ""

Additional command-line arguments to be added to the dovecot\_exporter service unit.
For the complete refence of the available CLI arguments please refer to the output
of the `dovecot_exporter --help` command.

Dependencies
------------

None.

Example Playbooks
-----------------

    $ cat playbook.yml
    - name: "Install and configure Prometheus dovecot_exporter"
      hosts: all
      roles:
        - { role: atosatto.dovecot_exporter }

Testing
-------

Tests are automated with [Molecule](http://molecule.readthedocs.org/en/latest/).

    $ pip install tox

To test all the scenarios run

    $ tox

To run a custom molecule command

    $ tox -e py27-ansible29 -- molecule test -s dovecot_exporter-latest

License
-------

MIT

Author Information
------------------

Andrea Tosatto ([@\_hilbert\_](https://twitter.com/_hilbert_))
