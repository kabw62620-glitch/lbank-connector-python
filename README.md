
# Installation
* pip install --upgrade lbank-connector-python -i https://pypi.org/simple
## Contract Call
* You need to apply for the corresponding api_key and api_secret
* The api_key and sign parameters will be encapsulated and added to the request parameters internally, users do not need to worry about it.
* API example
```python
from lbank.old_api import BlockHttpClient
import logging
api_key = ""
api_secret = ""
# service address
base_url = "https://api.lbkex.com/"
# Encryption method
sign_method = "RSA"
client = BlockHttpClient(
    sign_method=sign_method,
    api_key=api_key,
    api_secret=api_secret,
    base_url=base_url,
    log_level=logging.DEBUG,
)
# Pairs api
api_url = "v2/currencyPairs.do"
res = client.http_request("get", api_url)
print(res)
# withdrawConfigs api
api_url = "v2/withdrawConfigs.do"
payload = {
    "assetCode": "btc"
}
res = client.http_request("get", api_url, payload=payload)
print(res)
payload = {}
response = client.http_request("post", "v2/user_info.do", payload=payload)
print(response)
```
* Websocket example
```python
from lbank.websocket.websocket_client import LbankWebsocketClient
def sub_deep_data():
    ws_client = LbankWebsocketClient(
        base_url="",
        on_message=on_message,
    )
    subscribe_msg = {
    }
    ws_client.send(subscribe_msg)


def on_message(ws_client, msg):
    print(f"msg:{msg}")


if __name__ == '__main__':
    sub_deep_data()
````
