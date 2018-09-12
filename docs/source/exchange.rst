Exchange
========
Tables
------
Pairs
_____
To get a list of exchangeable pairs on the exchange, you need to:

.. code-block:: bash

    curl --request POST \
      --url http://jungle.cryptolions.io:18888/v1/chain/get_table_rows \
      --data '{"code":"EXCH_ACCOUNT","scope":"EXCH_ACCOUNT","table":"pairs"}'

where ``EXCH_ACCOUNT`` is exchange account.

Markets
_______
To get a list of offers on the exchange, filtered by pair, you need to:

.. code-block:: bash

    curl --request POST \
      --url http://jungle.cryptolions.io:18888/v1/chain/get_table_rows \
      --data '{"code":"EXCH_ACCOUNT","scope":"PAIR_ID","table":"markets","index_position":"2","key_type":"float64"}'

where ``EXCH_ACCOUNT`` is exchange account, ``PAIR_ID`` is id of exchangeble pair.
