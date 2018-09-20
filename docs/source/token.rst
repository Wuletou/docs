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

Get token info
______________

.. code-block:: bash

    curl --request POST \
      --url http://api-wullet.unblocking.io:18888/v1/chain/get_table_rows \
      --data '{"code": "TOKEN_ACCOUNT", "scope": "TOKEN_SYMBOL", "table": "accounts", "json": true}'

Where:
    * ``TOKEN_ACCOUNT`` — token account
    * ``TOKEN_SYMBOL`` — symbol for which to get info

You will get response like:

.. code-block:: json

    {
      "rows": [{
          "supply": "30000.00 TEST",
          "max_supply": "100000.00 TEST",
          "issuer": "testowner",
          "info": {
            "name": "Symbol for API demonstration",
            "url": "https://wulet.readthedocs.io/en/develop/",
            "logo_url": "https://www.lenta.com/public/2015/img/icons/lenta_logo.png"
          }
        }
      ],
      "more": false
    }

* ``supply`` field contains tokens that are already distributed
* ``max_supply`` field contains maximum number of tokens that can be distributed
* ``issuer`` field contains token owner that can distribute undistributed tokens
* ``info`` field contains token information

    * ``name`` is a full token name
    * ``url`` is a link to the store that distributes this token
    * ``logo_url`` is a link to the token logo

Get tokens list
_______________________

.. code-block:: bash

    curl --request POST \
      --url http://api-wullet.unblocking.io:18888/v1/chain/get_table_rows \
      --data '{"code": "TOKEN_ACCOUNT", "scope": "TOKEN_ACCOUNT", "table": "symbols", "json": true}'

Where:
    * ``TOKEN_ACCOUNT`` — token account

You will get response like:

.. code-block:: json

    {
      "rows": [{
          "symbol": "6,TEST"
        },{
          "symbol": "4,FOO"
        },{
          "symbol": "2,BAR"
        }
      ],
      "more": false
    }

``symbol`` field contains token name and its precision

Actions
-------
Transfer
________
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
