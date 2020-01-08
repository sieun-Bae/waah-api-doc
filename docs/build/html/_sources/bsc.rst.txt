Baby-crying state classification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section covers how to use *Baby-crying state classification API*.


Quick Start
===========
You can query *Baby-crying state classification API* with any HTTP client. We'll show you how to send HTTP request using Python.

.. code-block:: python
    :linenos:

    import requests
    from random import randint

    raw_audio_data = [random.randint(1, 100) for _ in range(16000 * 30)]
    res = requests.post('https://api.deeplycorp.com/bsc', json={"audio": raw_audio_data})
    print(res.text)

    # {
    #   "outputs": {
    #     "outputs": {
    #       "tensorShape": {
    #         "dim": [
    #           {
    #             "size": "1"
    #           },
    #           {
    #             "size": "4"
    #           }
    #         ]
    #       },
    #       "dtype": "DT_FLOAT",
    #       "floatVal": [
    #         0.5540047287940979,
    #         0.037925444543361664,
    #         0.08041844516992569,
    #         0.32765132188796997
    #       ]
    #     }
    #   },
    #   "modelSpec": {
    #     "signatureName": "serving_default",
    #     "version": "1",
    #     "name": "bsc"
    #   }
    # }

The response above shows JSON result of Baby-crying state classification. This JSON schema follows `Tensorflow Serving API's proto <https://github.com/tensorflow/serving/blob/master/tensorflow_serving/apis/predict.proto>`_.
What you should pay attention to are *floatVal* and *tensorShape*.

* *floatVal*: Probability of Baby-crying state classification based on given dataset.
* *tensorShape*: Result tensor shape.

***Notice*** Currently you should only pass one dataset with shape (1, 16000 * 30), otherwise API fails and returns HTTP status code 500.

The API preprocess the audio data from client, so just provide raw audio data with proper shape. If you preprocess yourself, incorrect inference may occurs frequently. 