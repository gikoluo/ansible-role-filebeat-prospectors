# Ansible Role: Filebeat for ELK Stack

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-filebeat.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-filebeat)

An Ansible Role that installs [Filebeat](https://www.elastic.co/products/beats/filebeat) on Linux, installed with tar.gz.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    filebeat_prospectors:
      - input_type: log
        paths:
          - "/var/log/*.log"

Prospectors that will be listed in the `prospectors` section of the Filebeat configuration. Read through the [Filebeat Prospectors configuration guide](https://www.elastic.co/guide/en/beats/filebeat/current/configuration-filebeat-options.html) for more options.

    filebeat_output_elasticsearch_enabled: false
    filebeat_output_elasticsearch_hosts:
      - "localhost:9200"

Whether to enable Elasticsearch output, and which hosts to send output to.

    filebeat_output_logstash_enabled: true
    filebeat_output_logstash_hosts:
      - "localhost:5000"

Whether to enable Logstash output, and which hosts to send output to.

    filebeat_ssl_dir: /etc/pki/logstash

The path where certificates and keyfiles will be stored.

    filebeat_ssl_certificate_file: ""
    filebeat_ssl_key_file: ""

Local paths to the SSL certificate and key files, which will be copied into the `filebeat_ssl_dir`.

For utmost security, you should use your own valid certificate and keyfile, and update the `filebeat_ssl_*` variables in your playbook to use your certificate.

To generate a self-signed certificate/key pair, you can use use the command:

    $ sudo openssl req -x509 -batch -nodes -days 3650 -newkey rsa:2048 -keyout filebeat.key -out filebeat.crt

Note that filebeat and logstash may not work correctly with self-signed certificates unless you also have the full chain of trust (including the Certificate Authority for your self-signed cert) added on your server. See: https://github.com/elastic/logstash/issues/4926#issuecomment-203936891

## Dependencies

None.

## Example Playbook

    - hosts: logs
      roles:
        - gikoluo.orcal-java
        - gikoluo.elasticsearch
        - gikoluo.logstash
        - gikoluo.filebeat

## License

MIT / BSD

## Author Information

This role was created in 2017 by [Giko Luo](http://www.luochunhui.com/), author of [Jfpal.com](https://www.jfpal.com/).
