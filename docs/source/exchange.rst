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



