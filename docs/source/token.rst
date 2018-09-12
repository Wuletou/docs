Token
=====
Tables
------
Get balance
___________

.. code-block:: bash

    curl --request POST \
      --url http://api-wullet.unblocking.io:18888/v1/chain/get_table_rows \
      --data '{"code": "TOKEN_ACCOUNT", "scope": "USER_ACCOUNT", "table": "accounts", "json": true}'

Where:
    * ``TOKEN_ACCOUNT`` — token account
    * ``USER_ACCOUNT`` — user whose balance should be received

You will get response like:

.. code-block:: json

    {
      "rows": [{
          "balance": "100.000000 TEST",
          "blocked": 20000000
        },{
          "balance": "10.0000 FOO",
          "blocked": 25000
        },{
          "balance": "1.00 BAR",
          "blocked": 75
        }
      ],
      "more": false
    }

* ``balance`` field contains tokens that user have with symbol and precision
* ``blocked`` field contains blocked tokens without symbol and precision

To get available tokens that user can spend, ``blocked`` should be subtracted from ``balance``. In the example above available user balances are ``80.000000 TEST``, ``7.5000 FOO`` and ``0.25 BAR``.
