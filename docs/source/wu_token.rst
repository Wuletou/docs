WU
=====
Actions
-------
Transfer
________
Transfer tokens from one account to another

.. code-block:: json

    {
      "code": "TOKEN_ACCOUNT",
      "action": "transfer",
      "args": {
        "from": "FROM_ACC",
        "to": "TO_ACC",
        "quantity": "100.0000 WU"
      }
    }

Where:
    * ``code`` - account where token code is deployed
    * ``from`` - from account
    * ``to`` - to account
    * ``quantity`` - how many tokens to transfer
