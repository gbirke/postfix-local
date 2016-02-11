# Setup up postfix to deliver all outgoing mails to a local user

This configuration is for test and development machines that must be configured to never really send out but deliver them to a local user.

Instructions come from http://askubuntu.com/questions/206766/local-only-sendmail-that-delivers-all-mail-to-a-directory


## Using the role
Here is an example playbook that uses the role for setting up mail delivery on a vagrant machine:

```yml
---
- hosts: all
  become: true
  vars:
      postfix_local_delivery_user: vagrant
      use_maildir: true
  roles:
      - { role: birke.postfix-local }
```

## Setting the aliases
After installation, make sure that the file `/etc/aliases` contains an alias for the user where the mail will be delivered to. Otherwise you will get an error.

## Reading the mail
You can either set up an IMAP server that can serve the mail in the maildir, or read it locally on the terminal, for example with [mutt](http://www.mutt.org/).

For tutorials on dovecot see
- https://www.digitalocean.com/community/tutorials/how-to-set-up-a-postfix-e-mail-server-with-dovecot  
-  https://thomas-leister.de/internet/mailserver-ubuntu-server-dovecot-postfix-mysql/ (German)

## Warning
This role is still largely untested.
It won't work on non-Debian systems.
It has no meta-information.
