Exchange
========
Tables
------
Pairs
_____
To get a list of exchangeable pairs on the exchange, you need to get table:

.. code-block:: bash

    POST /v1/chain/get_table_rows HTTP/1.0
    Host: api-wulet.unblocking.io

    {
      "code": "exch.account",
      "scope": "exch.account",
      "table": "pairs",
      "lower_bound": "",
      "upper_bound": "",
      "limit": 10,
      "json": true
    }

where:
 * ``code`` — account of exchange,
 * ``scope`` — should be same as exchange account,
 * ``table`` — name of requested table, should be ``pairs``,
 * ``lower_bound`` — JSON representation of lower bound value of key, defaults to first,
 * ``upper_bound`` — JSON representation of upper bound value value of key, defaults to last,
 * ``limit`` — the maximum number of rows to return,
 * ``json`` — returns JSON if ``true`` and binary if ``false``,

You will get response like:

.. code-block:: json

    {
      "rows": [
        {
          "id": 0,
          "base_symbol": "4,WU",
          "quote_symbol": "4,A"
        },
        {
          "id": 1,
          "base_symbol": "4,A",
          "quote_symbol": "4,WU"
        }
      ],
      "more": false
    }

where:
 * ``rows`` — an array of pairs exchanged on the exchange,
 * ``id`` — id of pair,
 * ``base_symbol`` — precision and symbol name of base currency,
 * ``quote_symbol`` — precision and symbol name of quote currency.

Markets
_______
To get a list of offers on the exchange, filtered by pair, you need to:

.. code-block:: bash

    POST /v1/chain/get_table_rows HTTP/1.0
    Host: api-wulet.unblocking.io

    {
      "code": "exch.account",
      "scope": 123,
      "table": "markets",
      "index_position": "2",
      "key_type": "float64",
      "lower_bound": "",
      "upper_bound": "",
      "limit": 10,
      "json": true
    }

where:
 * ``code`` — account of exchange,
 * ``scope`` — id of exchanged pair from Pairs table,
 * ``table`` — name of requested table, should be ``markets``,
 * ``index_position`` — index number to sort rows: ``1`` to sort by id, ``2`` to sort by price,
 * ``key_type`` — key type of index: ``i64`` for ``1`` index, ``float64`` for ``2`` index,
 * ``lower_bound`` — JSON representation of lower bound value of key, defaults to first,
 * ``upper_bound`` — JSON representation of upper bound value value of key, defaults to last,
 * ``limit`` — the maximum number of rows to return,
 * ``json`` — returns JSON if ``true`` and binary if ``false``,


You will get response like:

.. code-block:: json

    {
      "rows": [
        {
          "id": 0,
          "manager": "buyer1",
          "base": "2.0000 WU",
          "quote": "10.0000 A",
          "price": "0.20000000000000000"
        },
        {
          "id": 1,
          "manager": "buyer1",
          "base": "3.0000 WU",
          "quote": "19.0000 A",
          "price": "0.15789473684210525"
        },
        {
          "id": 2,
          "manager": "buyer1",
          "base": "1.0000 WU",
          "quote": "8.0000 A",
          "price": "0.12500000000000000"
        }
      ],
      "more": false
    }

where:
 * ``rows`` — an array of trades on the exchange,
 * ``id`` — id of trade,
 * ``manager`` — account name of user who created the trade offer,
 * ``base`` — base currency,
 * ``quote`` — quote currency,
 * ``price`` — price of the base currency against the quote,

Actions
-------
Add trade
_________

To add new trade to exchange you need to push action:

.. code-block:: json

    {
      "code": "exch.account",
      "action": "createx",
      "args": {
        "creator": "buyeraccount",
        "base_deposit": "10.1000 WU",
        "quote_deposit": "50.3000 AIR"
      }
    }

where:
 * ``code`` — account of exchange contract,
 * ``action`` — performed action. should be ``createx``,
 * ``creator`` — your account,
 * ``base_deposit`` — base currency in special format (as in example),
 * ``quote_deposit`` — quote currency in same format,

Accept specified trade
______________________

To accept specified trade you need to push action:

.. code-block:: json

    {
      "code": "exch.account",
      "action": "spec.trade",
      "args": {
        "id": 123,
        "seller": "buyeraccount",
        "sell": "50.3000 AIR",
        "receive": "10.1000 WU"
      }
    }

where:
 * ``code`` — account of exchange contract,
 * ``action`` — performed action. should be ``spec.trade``,
 * ``id`` — id of trade,
 * ``seller`` — your account,
 * ``sell`` — quote currency in same format,
 * ``receive`` — base currency in special format (as in example).

Market order trade
__________________

To get specified amount of tokens (market order) you need to push action:

.. code-block:: json

    {
      "code": "exch.account",
      "action": "market.trade",
      "args": {
        "seller": "buyeraccount",
        "sell_symbol": "4,AIR",
        "receive": "10.1000 WU"
      }
    }

where:
 * ``code`` — account of exchange contract,
 * ``action`` — performed action. should be ``market.trade``,
 * ``seller`` — your account,
 * ``sell_symbol`` — precision and symbol name of quote currency in special format (as in example),
 * ``receive`` — base currency you want to receive in special format (as in example).

Limit order trade
_________________

To get tokens for specified amount of another tokens (limit order) you need to push action:

.. code-block:: json

    {
      "code": "exch.account",
      "action": "limit.trade",
      "args": {
        "seller": "buyeraccount",
        "sell": "50.3000 AIR",
        "receive_symbol": "4,WU"
      }
    }

where:
 * ``code`` — account of exchange contract,
 * ``action`` — performed action. should be ``limit.trade``,
 * ``seller`` — your account,
 * ``sell`` — quote currency you want to receive in special format (as in example),
 * ``receive_symbol`` — precision and symbol name of base currency in special format (as in example).

Cancel trade
____________

To cancel your trade you need to push action:

.. code-block:: json

    {
      "code": "exch.account",
      "action": "cancelx",
      "args": {
        "id": 123,
        "base_symbol": "4,WU",
        "quote_symbol": "4,AIR"
      }
    }

where:
 * ``code`` — account of exchange contract,
 * ``action`` — performed action. should be ``cancelx``,
 * ``id`` — id of the canceled trade,
 * ``base_symbol`` — precision and symbol name of base currency in special format (as in example),
 * ``quote_symbol`` — precision and symbol name of quote currency in special format (as in example).