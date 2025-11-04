Ansible role: nullmailer
========================

Installs nullmailer, a simple relay-only mail transport agent, and configures it.

Role Variables
--------------

```
ENTRY POINT: *main* - Install and configure nullmailer MTA

          Installs nullmailer, a simple relay-only mail transport
          agent, and configures it.

Options (= indicates it is required):

- nullmailer_adminaddr  All recipients to users at either "localhost"
                         or the canonical host name (from
                         /etc/mailname) are remapped to this address.
                         To send to multiple addresses, put them all
                         on one line separated by a comma.
          default: null
          type: str

- nullmailer_allmailfrom  This value will override the envelope
                           sender on all messages
          default: null
          type: str

- nullmailer_defaultdomain  The default domain is appended to any
                             host name that does not contain a period
                             (except localhost)
          default: The domain name component of inventory_hostname
          type: str

- nullmailer_maxpause  The maximum time to pause between successive
                        queue runs, in seconds, or leave empty to use
                        the default value
          default: null
          type: int

- nullmailer_pausetime  The minimum time to pause between successive
                         queue runs when there are messages in the
                         queue, in seconds, or leave empty to use the
                         default value
          default: null
          type: int

- nullmailer_queuelifetime  The maximum time a message is allowed to
                             live in the queue before being considered
                             permanently failed, in seconds, or leave
                             empty to use the default value
          default: null
          type: int

- nullmailer_remotes  List of remote servers to which to send each
                       message
          default: []
          elements: str
          no_log: true
          type: list

- nullmailer_sendtimeout  The time to wait for a remote module listed
                           above to complete sending a message before
                           killing it and trying again, in seconds, or
                           leave empty to use the default value
          default: null
          type: int
```

Installation
------------

This role can either be installed manually with the ansible-galaxy CLI tool:

    ansible-galaxy install git+https://github.com/wandansible/nullmailer,main,wandansible.nullmailer
     
Or, by adding the following to `requirements.yml`:

    - name: wandansible.nullmailer
      src: https://github.com/wandansible/nullmailer

Roles listed in `requirements.yml` can be installed with the following ansible-galaxy command:

    ansible-galaxy install -r requirements.yml

Example Playbook
----------------

    - hosts: all
      roles:
         - role: wandansible.nullmailer
           become: true
           vars:
             nullmailer_adminaddr: admin@example.org
             nullmailer_allmailfrom: nullmailer@example.org
             nullmailer_remotes:
               - smtp.gmail.com smtp --port=465 --auth-login --user=gmail_address --pass=password --ssl
