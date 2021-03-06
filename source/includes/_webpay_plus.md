# Webpay Plus

<img src="images/webpay_plus_banner.jpg" class="full-width-image" />

El sistema permite generar cobros con Webpay Plus.




## Generar un cobro webpay plus

> Ejemplo de llamada

```shell
curl --request POST "https://api.qvo.cl/webpay_plus/charge" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA" \
  -d amount=2000 \
  -d return_url="http://www.example.com/return" \
  -d customer_id="cus_VhiEhjVHoYui_6ykz9fOsg" \
  -d description="Cobro de Prueba"
```

````javascript
const fetch = require('node-fetch-json');

fetch('https://api.qvo.cl/webpay_plus/charge', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  },
  body: {
    amount: 2000,
    return_url: "http://www.example.com/return",
    customer_id: "cus_VhiEhjVHoYui_6ykz9fOsg"
  }
}).then(function(response) {
  console.log(response);
});
````

````ruby
require 'rest-client'
require 'json'

result =
  RestClient.post 'https://api.qvo.cl/webpay_plus/charge', {
    amount: 2000,
    return_url: "http://www.example.com/return",
    customer_id: "cus_VhiEhjVHoYui_6ykz9fOsg"
  }, {
    Authorization: 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  }

p JSON.parse(result)
````

````python
import requests

r = requests.post('https://api.qvo.cl/webpay_plus/charge', params={
  'amount': 2000,
  'return_url': "http://www.example.com/return",
  'customer_id': "cus_VhiEhjVHoYui_6ykz9fOsg"
}, headers={
  'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
})

print r.json()
````

````php
<?php
require 'guzzle.phar';

$client = new GuzzleHttp\Client();

$body = $client->request('POST', 'https://api.qvo.cl/webpay_plus/charge', [
  'json' => [
    'amount' => 2000,
    'return_url' => "http://www.example.com/return",
    'customer_id' => "cus_VhiEhjVHoYui_6ykz9fOsg"
  ],
  'headers' => [
    'Authorization' => 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  ]
])->getBody();

$response = json_decode($body);

var_dump($response);
?>
````

> Ejemplo de respuesta

```json
{
  "transaction_id": "trx_fzmNpXvJJZBWwGbH5fW8cw",
  "redirect_url": "https://api.qvo.cl/webpay_plus/init_transaction/wpt_y7CUkd3EqiLB8TV1O7fhGQ",
  "expiration_date": "2017-05-21T23:43:41.332Z"
}
```

`POST /webpay_plus/charge`

Crea una cobro utilizando Webpay Plus.

Permite realizar un cobro mediante la interfaz de Webpay Plus. El proceso se divide en 3 pasos:

#### 1. Realizar la llamada y **redirigir** al cliente

Realiza la llamada de cobro `POST /webpay_plus/charge`. Una vez realizada la llamada, es necesario **redirigir** al cliente a el `redirect_url` retornado por la llamada, para iniciar el proceso de cobro.

#### 2. Capturar la respuesta

Una vez terminado paso 1, se retornará el cliente con una llamada `GET` a el `return_url` proporcionado como parámetro en el paso 1. Esta llamada, irá acompañada de un parámetro llamado `transaction_id` ubicado en la ruta, que representa el identificador único de la transacción.

Por ejemplo, para `return_url = "http://www.example.com/return` se retornará el cliente a:

`GET http://www.example.com/return?transaction_id=trx_fzmNpXvJJZBWwGbH5fW8cw`

donde `transaction_id` es igual a `trx_fzmNpXvJJZBWwGbH5fW8cw`

#### 3. Obtener el resultado

Para verificar si la transacción fue exitosa, se debe realizar una llamada a [obtener una transacción](#obtener-una-transaccion), utilizando el identificador único de la transacción `transaction_id`. retornado en el paso 2.


<aside class="warning">
El cobro posee una fecha de expiración de <b>10 minutos</b> luego de su fecha de creación. Si se intenta acceder a <code>redirect_url</code> luego de este tiempo, retornará <a href="#errores">un error</a>.
</aside>


### Parámetros
|||
|---------: | -----------|
| amount<p class="attr-desc warning">Requerido</p><p class="attr-desc">integer</p> | El monto de la transacción|
| return_url<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | URL de retorno de la transacción |
| customer_id<p class="attr-desc">string</p> | Identificador único de cliente. |
| description<p class="attr-desc">string</p> | Descripción de la transacción. |


### Respuesta

Retorna los parámetros para iniciar un cobro con Webpay Plus.