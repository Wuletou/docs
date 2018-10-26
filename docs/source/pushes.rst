PUSH API
========
Add APNS token device
_____________________

.. code-block:: bash

    POST /api/v1/user-devices HTTP/1.0
    Host: api-wulet.unblocking.io

    {
      "account": "iostestddg11",
      "token": "c6a0cef6e29d7b38040c843d2296b7ecdf3d66f5d1b62e3cffb64a2edadd6d05"
    }

where:
    * ``account`` - EOS account of user used at Wulet Platform,
    * ``token`` - APNS device token of user.

Delete APNS token device
________________________

.. code-block:: bash

    DELETE /api/v1/user-devices/TOKEN?account=ACCOUNT HTTP/1.0
    Host: api-wulet.unblocking.io
    X-Signature: SIGNATURE

where:
    * ``TOKEN`` - EOS account of user used at Wulet Platform,
    * ``ACCOUNT`` - APNS device token of user,
    * ``SIGNATURE`` - APNS device token of user.