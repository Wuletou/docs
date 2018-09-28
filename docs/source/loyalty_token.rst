Loyalty
=====
Actions
-------
Burn
____
Destroys some amount of tokens

.. code-block:: json

    {
      "code": "TOKEN_ACCOUNT",
      "action": "transfer",
      "args": {
        "owner": "FROM_ACC",
        "value": "100.0000 TKN"
      }
    }

Where:
    * ``code`` - account where loyalty token code is deployed
    * ``owner`` - account who wants to burn tokens
    * ``value`` - how many tokens to burn
