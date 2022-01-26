# Ansible Role: Mailhog installation for outgoing email catching

Installs [MailHog](https://github.com/mailhog/MailHog) to catch outgoing emails into single mailbox for temp/dev environments.

## Requirements

None.

## Role Variables

See `defaults/main.yml` for details.

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
         - { role: classyllama.mailhog, tags: mailhog, when: use_classyllama_mailhog | default(false) }

## Notes

This role replaces the PHP value for `sendmail_path` variable in `/etc/php.d/20-mailhog.ini` to `/usr/bin/msmtp --read-recipients -a default`.

Look for captured email in the browser at http://mydomain:1025  (eg: http://my-temp.cldev.io:1025/)

On DigitalOcean environment incoming port 1025 must be opened using the following Terraform code:

    allow_incoming_ports = [
     {
      protocol         = "tcp"
      port_range       = "1025"
      source_addresses = ["1.2.3.4/32"]
     },
    ]

## License

This work is licensed under the MIT license. See LICENSE file for details.

