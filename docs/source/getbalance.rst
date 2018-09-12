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
            "balance": "100.000000 WU",
            "blocked": 20000000
        }],
        "more": false
    }

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
