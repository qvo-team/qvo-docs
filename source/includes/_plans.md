# Planes

Un plan de suscripción contiene la información para el cobro recurrente de un servicio o producto. Por ejemplo, puedes tener una plan de CLP$20.000 al mes por caracterísitcas básicas y otro de CLP$40.000 por características premium.


## El objeto plan

> Ejemplo de respuesta

```json
{
  "id": "oro",
  "name": "Plan oro",
  "price": "3000.0",
  "currency": "CLP",
  "interval": "month",
  "interval_count": 1,
  "trial_period_days": 0,
  "default_cycle_count": 12,
  "status": "active",
  "subscriptions": [
    {
      "id": "sub_HnKU4UmU5GtymRulcVOEow",
      "status": "active",
      "current_period_start": "2017-05-17T19:12:57.185Z",
      "current_period_end": "2017-06-17T19:12:57.185Z",
      "created_at": "2017-05-17T19:12:57.189Z",
      "updated_at": "2017-05-17T19:12:57.189Z",
      "customer": {
        "id": "cus_qos_6r3-4I4zIiou2BVMHg",
        "name": "Jon Snow",
        "email": "dabastard@thewatch.org",
        "metadata": null,
        "address": null
      }
    }
  ],
  "created_at": "2017-05-17T19:12:55.450Z",
  "updated_at": "2017-05-17T19:12:55.450Z"
}
```

### Atributos
|||
|---------: | -----------|
| id<p class="attr-desc">string</p> | Identificador único del objeto. |
| name<p class="attr-desc">string</p> | El nombre de despliegue del plan. |
| price<p class="attr-desc">decimal</p> | El precio del plan. |
| currency<p class="attr-desc">string</p> | Código correpondiente a la moneda. Puede ser: `CLP` o `UF` |
| interval<p class="attr-desc">string</p> | Intervalo del plan. Puede ser: `day` día, `week` semana, `month` mes o `year` año. |
| interval_count<p class="attr-desc">integer</p> | Cantidad del intervalo del plan. Por ejemplo, si este valor es `3` e `interval` es igual a `week`, el plan tendrá un periodo de 3 semanas. |
| trial_period_days<p class="attr-desc">integer</p> | Número de días de prueba otorgados cuando se suscribe un cliente al plan. Es `0` si no tiene un periodo definido. |
| default_cycle_count<p class="attr-desc">integer</p> | Número de ciclos por defecto de las suscripciones. |
| status<p class="attr-desc">string</p> | Estado del plan. Puede ser: `active` o `inactive`. |
| subscriptions<p class="attr-desc">Array<[Subscription](#el-objeto-suscripcion)></p> | Suscripciones activas relacionadas al plan. |
| created_at<p class="attr-desc">datetime</p> | Fecha de creación del objeto. |
| updated_at<p class="attr-desc">datetime</p> | Fecha de la última actualización del objeto. |


## Crear un plan

> Ejemplo de llamada

````shell
curl --request POST "https://api.qvo.cl/plans" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA" \
  -d id="oro" \
  -d name="Plan oro"
  -d price=15000,
  -d currency="CLP",
  -d trial_period_days=10
````


````javascript
const fetch = require('node-fetch-json');

fetch('https://api.qvo.cl/plans', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  },
  body: {
    id: "oro",
    name: "Plan Oro",
    price: 15000,
    currency: "CLP",
    trial_period_days: 10
  }
}).then(function(response) {
  console.log(response);
});
````

````ruby
require 'rest-client'
require 'json'

result =
  RestClient.post 'https://api.qvo.cl/plans', {
    id: "oro",
    name: "Plan Oro",
    price: 15000,
    currency: "CLP",
    trial_period_days: 10
  }, {
    Authorization: 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  }

p JSON.parse(result)
````

````python
import requests

r = requests.post('https://api.qvo.cl/plans', params={
  'id': 'oro',
  'name': 'Plan Oro',
  'price': 15000,
  'currency': 'CLP',
  'trial_period_days': 10
}, headers={
  'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
})

print r.json()
````

````php
<?php
require 'guzzle.phar';

$client = new GuzzleHttp\Client();

$body = $client->request('POST', 'https://api.qvo.cl/plans', [
  'json' => [
    'id' => 'oro',
    'name' => 'Plan Oro',
    'price' => 15000,
    'currency' => 'CLP',
    'trial_period_days' => 10
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
  "id": "oro",
  "name": "Plan oro",
  "price": "15000.0",
  "currency": "CLP",
  "interval": "month",
  "interval_count": 1,
  "trial_period_days": 10,
  "default_cycle_count": 6,
  "status": "active",
  "subscriptions": [],
  "created_at": "2017-05-17T19:12:55.450Z",
  "updated_at": "2017-05-17T19:12:55.450Z"
}
```

`POST /plans`

Crea un nuevo objeto plan.

### Parámetros
|||
|---------: | -----------|
| id<p class="attr-desc danger">Único</p><p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único del plan. |
| name<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Nombre de despliegue del plan. |
| price<p class="attr-desc warning">Requerido</p><p class="attr-desc">integer or decimal</p> | Precio del plan. Ciertas monedas soportan `decimal` como `UF`, pero en general es un `integer` |
| currency<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Código correspondiente a la moneda. Puede ser: `CLP` o `UF`. |
| interval<p class="attr-desc">string</p> | Intervalo del plan. Puede ser: `day` día, `week` semana, `month` mes o `year` año. Si no se especifica, el valor por defecto es `month`. |
| interval_count<p class="attr-desc">integer</p> | Cantidad del intervalo del plan. Debe ser un entero positivo mayor o igual a `1`. Por ejemplo, si este valor es `3` e `interval` es igual a `week`, el plan tenrá un periodo de facturación de 3 semanas. El valor por defecto es `1`. |
| trial_period_days<p class="attr-desc">integer</p> | Especifica el número de días de prueba del plan. Si incluyes un periodo de prueba, al cliente no se le cobrará hasta que termine este periodo. |
| default_cycle_count<p class="attr-desc">integer</p> | Especifica el número de ciclos por defecto de las suscripciones. Por ejemplo si el intervalo del plan es de 1 mes y el número de ciclos es 6, la suscripciones terminarán por defecto a los 6 meses después de creadas. |


### Respuesta

Retorna un objeto de plan si la llamada es exitosa. Si existe otro plan con el mismo `id`, retornará [un error](#errores).



## Obtener un plan

> Ejemplo de llamada

````shell
curl --request GET "https://api.qvo.cl/plans/oro" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA"
````

````javascript
const fetch = require('node-fetch-json');

fetch('https://api.qvo.cl/plans/oro', {
  headers: {
    'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  }
}).then(function(response) {
  console.log(response);
});
````

````ruby
require 'rest-client'
require 'json'

result =
  RestClient.get 'https://api.qvo.cl/plans/oro', {
    Authorization: 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('https://api.qvo.cl/plans/oro', headers={
  'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
})

print r.json()
````

```php
<?php
require 'guzzle.phar';

$client = new GuzzleHttp\Client();

$body = $client->request('GET', 'https://api.qvo.cl/plans/oro', [
  'headers' => [
    'Authorization' => 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  ]
]);->getBody();

$response = json_decode($body);

var_dump($response);
?>
```

> Ejemplo de respuesta

```json
{
  "id": "oro",
  "name": "Plan oro",
  "price": "15000.0",
  "currency": "CLP",
  "interval": "month",
  "interval_count": 1,
  "trial_period_days": 10,
  "default_cycle_count": null,
  "status": "active",
  "subscriptions": [],
  "created_at": "2017-05-17T19:12:55.450Z",
  "updated_at": "2017-05-17T19:12:55.450Z"
}
```

`GET /plans/{plan_id}`

Obtiene los detalles de un plan existente. Se necesita proporcionar sólo el identificador único del plan el cual fue retornado al momento de su creación.

### Parámetros
|||
|---------: | -----------|
| plan_id<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único del plan. |


### Respuesta

Retorna un objeto de plan si se provee de un identificador válido.




## Actualizar un plan

> Ejemplo de llamada

````shell
curl --request PUT "https://api.qvo.cl/plans/oro" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA" \
  -d name="Di Oro"
````


````javascript
const fetch = require('node-fetch-json');

fetch('https://api.qvo.cl/plans/oro', {
  method: 'PUT',
  headers: {
    'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  },
  body: {
    name: "Di Oro"
  }
}).then(function(response) {
  console.log(response);
});
````

````ruby
require 'rest-client'
require 'json'

result =
  RestClient.put 'https://api.qvo.cl/plans/oro', {
    name: "Di Oro"
  }, {
    Authorization: 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('https://api.qvo.cl/plans/oro', params={
  'name': 'Di Oro'
}, headers={
  'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
})

print r.json()
````

````php
<?php
require 'guzzle.phar';

$client = new GuzzleHttp\Client();

$body = $client->request('PUT', 'https://api.qvo.cl/plans/oro', [
  'json' => [
    'name' => "Di Oro"
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
  "id": "oro",
  "name": "Di Oro",
  "price": "15000.0",
  "currency": "CLP",
  "interval": "month",
  "interval_count": 1,
  "trial_period_days": 10,
  "default_cycle_count": null,
  "status": "active",
  "subscriptions": [],
  "created_at": "2017-05-17T19:12:55.450Z",
  "updated_at": "2017-05-17T19:12:55.450Z"
}
```


`PUT /plans/{plan_id}`

Actualiza el plan especificado con los parametros provistos. Cualquier parámetro que no se provea quedará inalterado.


### Parámetros
|||
|---------: | -----------|
| plan_id<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único del plan. |
| name<p class="attr-desc">string</p> | Nombre de despliegue del plan. |


### Respuesta

Retorna el objeto de plan si la actualización es exitosa. Retorna [un error](#errores) si algun parámetro de actualización es inválido.

## Eliminar un plan

> Ejemplo de llamada

````shell
curl -x DELETE "https://api.qvo.cl/plans/oro" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA"
````


````javascript
const fetch = require('node-fetch-json');

fetch('https://api.qvo.cl/plans/oro', {
  method: 'DELETE',
  headers: {
    'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  }
}).then(function(response) {
  console.log(response);
});
````

````ruby
require 'rest-client'
require 'json'

result =
  RestClient.delete 'https://api.qvo.cl/plans/oro', {
    Authorization: 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  }

p JSON.parse(result)
````

````python
import requests

r = requests.delete('https://api.qvo.cl/plans/oro', headers={
  'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
})

print r.json()
````

````php
<?php
require 'guzzle.phar';

$client = new GuzzleHttp\Client();

$body = $client->request('DELETE', 'https://api.qvo.cl/plans/oro', [
  'headers' => [
    'Authorization' => 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  ]
])->getBody();

$response = json_decode($body);

var_dump($response);
?>
````

`DELETE /plans/{plan_id}`

Elimina permanentemente un plan. Esta acción es irreversible. Si existieran suscripciones activas asociadas al plan, este no se podrá eliminar

### Parámetros
|||
|---------: | -----------|
| plan_id<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único del plan. |



### Respuesta

Retorna una respuesta sin contenido si el plan fue eliminado con éxito. Si el identificador del plan no es válido, retornará [un error](#errores).



## Obtener una lista de planes

> Ejemplo de llamada

````shell
curl --request GET "https://api.qvo.cl/plans" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA"
````

````javascript
const fetch = require('node-fetch-json');

fetch('https://api.qvo.cl/plans', {
  headers: {
    'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  }
}).then(function(response) {
  console.log(response);
});
````

````ruby
require 'rest-client'
require 'json'

result =
  RestClient.get 'https://api.qvo.cl/plans', {
    Authorization: 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('https://api.qvo.cl/plans', headers={
  'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA'
})

print r.json()
````

````php
<?php
require 'guzzle.phar';

$client = new GuzzleHttp\Client();

$body = $client->request('GET', 'https://api.qvo.cl/plans', [
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
[
  {
    "id": "oro",
    "name": "Plan Oro",
    "price": "15000.0",
    "currency": "CLP",
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": 10,
    "default_cycle_count": null,
    "status": "active",
    "subscriptions": [
      {
        "id": "sub_HnKU4UmU5GtymRulcVOEow",
        "status": "active",
        "current_period_start": "2017-05-17T19:12:57.185Z",
        "current_period_end": "2017-06-17T19:12:57.185Z",
        "created_at": "2017-05-17T19:12:57.189Z",
        "updated_at": "2017-05-17T19:12:57.189Z",
        "customer": {
          "id": "cus_qos_6r3-4I4zIiou2BVMHg",
          "name": "Jon Snow",
          "email": "dabastard@winterfell.com",
          "metadata": null,
          "address": null
        }
      }
    ],
    "created_at": "2017-05-17T19:12:55.450Z",
    "updated_at": "2017-05-17T19:12:55.450Z"
  }
]
```

`GET /plans`

Retorna una lista de planes. Los planes se encuentran ordenados por defecto por la fecha de creación, donde los mas recientes aparecerán primero.

<aside class="notice">
Este endpoint admite <a href="#paginacion-filtros-y-orden">paginación, filtros y orden</a>
</aside>

### Respuesta

Un arreglo donde cada entrada representa a un plan con su respectiva información.


