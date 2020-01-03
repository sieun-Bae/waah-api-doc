Tutorial
^^^^^^^^

This section covers how to use *Deeply API*.


Quickstart
==================
You can query *Deeply API* with any HTTP client. We'll show you how to send HTTP request using Python.

.. code-block:: python
    :linenos:

    import requests
    from random import randint

    audio_data = [randint(1, 100) for _ in range(16000)]
    res = requests.post('https://api.deeplycorp.com/aed', json={"audio": audio_data})
    print(res.text)
