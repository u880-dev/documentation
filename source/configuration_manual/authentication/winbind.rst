.. _authentication-winbind:

==================
Winbind mechanisms
==================

Dovecot supports NTLM and GSS-SPNEGO authentication mechanisms using
`Samba <http://www.samba.org>`_'s winbind daemon. It is useful when you
need to authenticate users against a Windows domain (either AD or NT).

By default NTLM mechanism is handled internally. You can use winbind
instead by setting:

.. code-block:: none

   auth_use_winbind = yes

The usernames, returned by winbind, can contain some domain part (either
"DOMAIN\user" or "user@example.com"). Such usernames are always
transformed to the form of "user@domain". To strip domain part (to
obtain corresponding local username, for example), set:

.. code-block:: none

   auth_username_format = %n

Dovecot needs path to Samba's ``ntlm_auth`` binary to perform the
authentication. You can change the path with:

.. code-block:: none

   auth_winbind_helper_path = /usr/bin/ntlm_auth

Dovecot currently does blocking lookups, so if ``ntlm_auth`` is slow on
responding (e.g. network problems), Dovecot blocks all other
authentication requests until it's finished.
