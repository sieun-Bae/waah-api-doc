Audio Event Detection
^^^^^^^^^^^^^^^^^^^^^

This section covers how to use *Audio Event Detection API*.


Quick Start
===========
You can query *Audio Event Detection API* with any HTTP client. We'll show you how to send HTTP request using Python.

.. code-block:: python
    :linenos:

    import requests
    from random import randint

    raw_audio_data = [randint(1, 100) for _ in range(16000)]
    res = requests.post('https://api.deeplycorp.com/aed', json={"audio": raw_audio_data})
    print(res.text)

    #   {
    #       "modelSpec": {
    #           "signatureName": "serving_default",
    #           "version": "5",
    #           "name": "AED"
    #       },
    #       "outputs": {
    #           "outputs": {
    #               "floatVal": [
    #                   0.00034675668575800955
    #               ],
    #               "dtype": "DT_FLOAT",
    #               "tensorShape": {
    #                   "dim": [
    #                       {
    #                           "size": "1"
    #                       },
    #                       {
    #                           "size": "1"
    #                       }
    #                   ]
    #               }
    #           }
    #       }
    #   }

The response above shows JSON result of Cry Event Detection. This JSON schema follows `Tensorflow Serving API's proto <https://github.com/tensorflow/serving/blob/master/tensorflow_serving/apis/predict.proto>`_.
What you should pay attention to are *floatVal* and *tensorShape*.

* *floatVal*: Probability of Cry Event Detection based on given dataset.
* *tensorShape*: Result tensor shape.

***Notice*** Currently you should only pass one dataset with shape (1, 16000), otherwise API fails and returns HTTP status code 500.

The API preprocess the audio data from client, so just provide raw audio data with proper shape. If you preprocess yourself, incorrect inference may occurs frequently. 