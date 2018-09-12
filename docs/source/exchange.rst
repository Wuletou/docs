Exchange
========
Tables
------
Pairs
_____
To get a list of exchangeable pairs on the exchange, you need to:

.. code-block:: bash

    curl --request POST \
      --url https://api-wullet.unblocking.io:18888/v1/chain/get_table_rows \
      --data '{"code":"EXCH_ACCOUNT","scope":"EXCH_ACCOUNT","limit":LIMIT,"table":"pairs","json":true}'

where:
 * ``EXCH_ACCOUNT`` — exchange account,
 * ``LIMIT`` — max rows count.

You will get response like:

.. code-block:: json

    {
      "rows": [
        {
          "id": 0,
          "base_symbol": {
            "sym": "4,WU",
            "contract": "wu.deployer"
          },
          "quote_symbol": {
            "sym": "4,B",
            "contract": "wu.deployer"
          }
        },
        {
          "id": 1,
          "base_symbol": {
            "sym": "4,B",
            "contract": "wu.deployer"
          },
          "quote_symbol": {
            "sym": "4,WU",
            "contract": "wu.deployer"
          }
        }
      ],
      "more": false
    }


Markets
_______
To get a list of offers on the exchange, filtered by pair, you need to:

.. code-block:: bash

    curl --request POST \
      --url https://api-wullet.unblocking.io:18888/v1/chain/get_table_rows \
      --data '{"code":"EXCH_ACCOUNT","scope":"PAIR_ID","limit":LIMIT",table":"markets","index_position":"2","key_type":"float64","json":true}'

where:
 * ``EXCH_ACCOUNT`` — exchange account,
 * ``PAIR_ID`` — id of exchangeble pair,
 * ``LIMIT`` — max rows count.

You will get response like:

.. code-block:: json

    {
      "rows": [
        {
          "id": 0,
          "manager": "buyer1",
          "base": {
            "quantity": "2.0000 WU",
            "contract": "wu.deployer"
          },
          "quote": {
            "quantity": "10.0000 B",
            "contract": "wu.deployer"
          },
          "price": "0.20000000000000001"
        },
        {
          "id": 1,
          "manager": "buyer1",
          "base": {
            "quantity": "3.0000 WU",
            "contract": "wu.deployer"
          },
          "quote": {
            "quantity": "19.0000 B",
            "contract": "wu.deployer"
          },
          "price": "0.15789473684210525"
        },
        {
          "id": 2,
          "manager": "buyer1",
          "base": {
            "quantity": "1.0000 WU",
            "contract": "wu.deployer"
          },
          "quote": {
            "quantity": "8.0000 B",
            "contract": "wu.deployer"
          },
          "price": "0.12500000000000000"
        }
      ],
      "more": false
    }

Actions
-------
Add trade
_________

To add new trade to exchange you need to push action:

.. code-block:: json

    {
      "code": "EXCH_ACCOUNT",
      "action": "createx",
      "args": {
        "creator": "YOUR_ACC",
        "base_deposit": {
          "quantity": "BASE_QUANT",
          "contract": "BASE_ACC"
        },
        "quote_deposit": {
          "quantity": "QUOTE_QUANT",
          "contract": "QUOTE_ACC"
        }
      }
    }

where:
 * ``EXCH_ACCOUNT`` — exchange account,
 * ``YOUR_ACC`` — your account,
 * ``BASE_QUANT`` — base tokens asset (ex. ``10.5402 WU``),
 * ``BASE_ACC`` — account of contract of base token (ex. ``wu.deployer``),
 * ``QUOTE_QUANT`` — quote tokens asset (ex. ``50.3000 AIR``),
 * ``QUOTE_ACC`` — account of contract of quote token (ex. ``lt.deployer``),

Accept specified trade
______________________

To accept specified trade you need to push action:

.. code-block:: json

    {
      "code": "EXCH_ACCOUNT",
      "action": "spec.trade",
      "args": {
        "id": ID,
        "seller": "YOUR_ACC",
        "receive": {
          "quantity": "BASE_QUANT",
          "contract": "BASE_ACC"
        },
        "sell": {
          "quantity": "QUOTE_QUANT",
          "contract": "QUOTE_ACC"
        }
      }
    }

where:
 * ``EXCH_ACCOUNT`` — exchange account,
 * ``ID`` — id of trade,
 * ``YOUR_ACC`` — your account,
 * ``BASE_QUANT`` — base tokens asset (ex. ``10.5402 WU``),
 * ``BASE_ACC`` — account of contract of base token (ex. ``wu.deployer``),
 * ``QUOTE_QUANT`` — quote tokens asset (ex. ``50.3000 AIR``),
 * ``QUOTE_ACC`` — account of contract of quote token (ex. ``lt.deployer``),

Market order trade
__________________

To get specified amount of tokens (market order) you need to push action:

.. code-block:: json

    {
      "code": "EXCH_ACCOUNT",
      "action": "market.trade",
      "args": {
        "seller": "YOUR_ACC",
        "receive": {
          "quantity": "BASE_QUANT",
          "contract": "BASE_ACC"
        },
        "sell_symbol": {
          "sym": "QUOTE_SYM",
          "contract": "QUOTE_ACC"
        }
      }
    }

where:
 * ``EXCH_ACCOUNT`` — exchange account,
 * ``YOUR_ACC`` — your account,
 * ``BASE_QUANT`` — base tokens asset (ex. ``10.5402 WU``),
 * ``BASE_ACC`` — account of contract of base token (ex. ``wu.deployer``),
 * ``QUOTE_SYM`` — symbol of quote token with precision and name (ex. ``4,AIR``),
 * ``QUOTE_ACC`` — account of contract of quote token (ex. ``lt.deployer``),

Limit order trade
_________________

To get tokens for specified amount of another tokens (limit order) you need to push action:

.. code-block:: json

    {
      "code": "EXCH_ACCOUNT",
      "action": "limit.trade",
      "args": {
        "seller": "YOUR_ACC",
        "receive_symbol": {
          "sym": "BASE_SYM",
          "contract": "BASE_ACC"
        },
        "sell": {
          "quantity": "QUOTE_QUANT",
          "contract": "QUOTE_ACC"
        }
      }
    }

where:
 * ``EXCH_ACCOUNT`` — exchange account,
 * ``YOUR_ACC`` — your account,
 * ``BASE_SYM`` — symbol of base token with precision and name (ex. ``4,WU``),
 * ``BASE_ACC`` — account of contract of base token (ex. ``wu.deployer``),
 * ``BASE_QUANT`` — quote tokens asset (ex. ``10.5402 AIR``),
 * ``QUOTE_ACC`` — account of contract of quote token (ex. ``lt.deployer``),

Cancel trade
____________

To cancel your trade you need to push action:

.. code-block:: json

    {
      "code": "EXCH_ACCOUNT",
      "action": "cancelx",
      "args": {
        "id": ID,
        "base_symbol": {
          "sym": "BASE_SYM",
          "contract": "BASE_ACC"
        },
        "quote_symbol": {
          "sym": "QUOTE_SYM",
          "contract": "QUOTE_ACC"
        }
      }
    }

where:
 * ``EXCH_ACCOUNT`` — exchange account,
 * ``ID`` — id of the canceled trade,
 * ``BASE_SYM`` — symbol of base token with precision and name (ex. ``4,WU``),
 * ``BASE_ACC`` — account of contract of base token (ex. ``wu.deployer``),
 * ``QUOTE_SYM`` — symbol of quote token with precision and name (ex. ``4,AIR``),
 * ``QUOTE_ACC`` — account of contract of quote token (ex. ``lt.deployer``).
