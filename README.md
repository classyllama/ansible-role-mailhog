# Ansible Role: Mailhog installation for outgoing email catching

Installs [MailHog](https://github.com/mailhog/MailHog) to catch outgoing emails into single mailbox for temp/dev environments.

## Requirements

None.

## Role Variables

Use `mailhog_http_user`, `mailhog_http_password` to enable HTTP Auth (by default username is set to `qa`).
See `defaults/main.yml` for details.

## Dependencies

None.

## Example Playbook

    - hosts: all
      vars:
        mailhog_http_password: mypass
      roles:
         - { role: classyllama.mailhog, tags: mailhog, when: use_classyllama_mailhog | default(false) }

## Notes

This role replaces the PHP value for `sendmail_path` variable in `/etc/php.d/20-mailhog.ini` to `/usr/bin/msmtp --read-recipients -a default`.

Look for captured email in the browser at http://mydomain:8025  (eg: http://my-temp.cldev.io:8025/)

On DigitalOcean environment incoming port 1025 must be opened using the following Terraform code:

    allow_incoming_ports = [
     {
      protocol         = "tcp"
      port_range       = "8025"
      source_addresses = ["1.2.3.4/32"]
     },
    ]

## License

This work is licensed under the MIT license. See LICENSE file for details.

