ansible-test-template-lookup
----------------------------

This repository can be used to test issues with Ansible ``lookup("template")``
lookup. The issue started after `fix for CVE-2016-9587 <https://github.com/ansible/ansible/commit/ec84ff6de6eca9224bf3f22b752bb8da806611ed>`_ commit and is present in current Ansible ``stable-2.1`` and ``stable-2.2`` branches.

the issue is present in the ``devel`` branch as well, introduced by the `fix for CVE-2016-9587 <https://github.com/ansible/ansible/commit/a6fff93967763c45370b2215f79a8050e6e6486a>`_ commit.

To perform the test, run in a terminal:

.. code-block:: console

   ./playbook.yml

The output with Ansible errors:

.. code-block:: console

   PLAY [Test lookup remplate] ****************************************************

   TASK [Gather data from passwd] *************************************************
   ok: [localhost]

   TASK [Check home directories] **************************************************
   fatal: [localhost]: FAILED! => {"failed": true, "msg": "An unhandled exception occurred while running the lookup plugin 'template'. Error was a <class 'yaml.representer.RepresenterError'>, original message: cannot represent an object: /root"}
   ...ignoring

   TASK [Check home directories] **************************************************
   ok: [localhost] => (item=/root)
   ok: [localhost] => (item=/var/backups)

   PLAY RECAP *********************************************************************
   localhost                  : ok=3    changed=0    unreachable=0    failed=0   

The correct output:

.. code-block:: console

   PLAY [Test lookup remplate] ****************************************************

   TASK [Gather data from passwd] *************************************************
   ok: [localhost]

   TASK [Check home directories] **************************************************
   ok: [localhost] => (item=/root)
   ok: [localhost] => (item=/var/backups)

   TASK [Check home directories] **************************************************
   ok: [localhost] => (item=/root)
   ok: [localhost] => (item=/var/backups)

   PLAY RECAP *********************************************************************
   localhost                  : ok=3    changed=0    unreachable=0    failed=0
