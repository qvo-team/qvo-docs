# Suscripciones

Las suscripciones permiten cobrar a un cliente de manera recurrente. Una suscripcion vincula un cliente con un plan previamente creado.

## El objeto suscripción

> Ejemplo de respuesta

```json
{
  "id": "sub_HnKU4UmU5GtymRulcVOEow",
  "status": "active",
  "current_period_start": "2017-05-17T19:12:57.185Z",
  "current_period_end": "2017-06-17T19:12:57.185Z",
  "customer": {
    "id": "cus_qos_6r3-4I4zIiou2BVMHg",
    "name": "Jon Snow",
    "email": "dabastad@thewatch.org"
  },
  "plan": {
    "id": "oro",
    "name": "Plan Oro",
    "price": "15000.0",
    "currency": "CLP"
  },
  "created_at": "2017-05-17T19:12:57.189Z",
  "updated_at": "2017-05-17T19:12:57.189Z"
}
```

### Atributos
|||
|--------- | -----------|
| id<p class="attr-desc">string</p> | Identificador único del objeto |
| status<p class="attr-desc">string</p> | El estado de la suscripcion. Puede ser: `active`, `canceled`, `trialing`, `unpaid`. Una suscripción que está en periodo de prueba, se encuentra en `trialing` y se mueve a `active` cuando el periodo de prueba termina. Cuando se falla un cobro para renovar la suscripción, pasa al estado `unpaid`. Cuando se cancela una suscripción, tiene el estado `canceled`. |
| current_period_start<p class="attr-desc">datetime</p> | Fecha de inicio del periodo de facturación. |
| current_period_end<p class="attr-desc">datetime</p> | Fecha de término del periodo de facturación. Al final de este periodo se realizará un cobro. |
| customer<p class="attr-desc">[Customer](#el-objeto-cliente)</p> | El cliente asociado a la suscripción. |
| plan<p class="attr-desc">[Plan](#el-objeto-plan)</p> | El plan asociado a la suscripción. |
| created_at<p class="attr-desc">datetime</p> | Fecha de creación del objeto |
| updated_at<p class="attr-desc">datetime</p> | Fecha de la última actualización del objeto |


## Crear una suscripción

> Ejemplo de llamada

````shell
curl --request POST "https://api.qvo.cl/subscriptions" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA" \
  -d customer_id="cus_qos_6r3-4I4zIiou2BVMHg" \
  -d plan_id="oro"
````


````javascript
const request = require('node-fetch');
fetch('http://api.qvo.cl/subscriptions', { method: 'POST'}, {
  customer_id: "cus_qos_6r3-4I4zIiou2BVMHg",
  plan_id: "oro"
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.post 'http://api.qvo.cl/subscriptions', params:
  {
    customer_id: "cus_qos_6r3-4I4zIiou2BVMHg",
    plan_id: "oro"
  }

p JSON.parse(result)
````

````python
import requests

r = requests.post('http://api.qvo.cl/subscriptions', params={
  customer_id: "cus_qos_6r3-4I4zIiou2BVMHg",
  plan_id: "oro"
})

print r.json()
````

> Ejemplo de respuesta

```json
{
  "id": "sub_HnKU4UmU5GtymRulcVOEow",
  "status": "active",
  "current_period_start": "2017-05-17T19:12:57.185Z",
  "current_period_end": "2017-06-17T19:12:57.185Z",
  "customer": {
    "id": "cus_qos_6r3-4I4zIiou2BVMHg",
    "name": "Jon Snow",
    "email": "dabastad@thewatch.org"
  },
  "plan": {
    "id": "oro",
    "name": "Plan Oro",
    "price": "15000.0",
    "currency": "CLP"
  },
  "created_at": "2017-05-17T19:12:57.189Z",
  "updated_at": "2017-05-17T19:12:57.189Z"
}
```

`POST /subscriptions`

Crea una nueva suscripción para un cliente existente.

### Parámetros
|||
|--------- | -----------|
| customer_id<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único de un cliente. |
| plan_id<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único de un plan. |


### Respuesta

Retorna un objeto de suscripción si la llamada es exitosa. Si el cliente no posee un medio de pago asociado por defecto o el cobro falla, retornará [un error](#errores), a menos que el plan sea gratis o posea un periodo de prueba.



## Obtener una suscripción

> Ejemplo de llamada

````shell
curl --request GET "https://api.qvo.cl/subscriptions/sub_HnKU4UmU5GtymRulcVOEow" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA"
````

````javascript
const request = require('node-fetch');
fetch('http://api.qvo.cl/subscriptions/sub_HnKU4UmU5GtymRulcVOEow', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get 'http://api.qvo.cl/subscriptions/sub_HnKU4UmU5GtymRulcVOEow'
p JSON.parse(result)
````

````python
import requests

r = requests.get('http://api.qvo.cl/subscriptions/sub_HnKU4UmU5GtymRulcVOEow')

print r.json()
````

> Ejemplo de respuesta

```json
{
  "id": "sub_HnKU4UmU5GtymRulcVOEow",
  "status": "active",
  "current_period_start": "2017-05-17T19:12:57.185Z",
  "current_period_end": "2017-06-17T19:12:57.185Z",
  "customer": {
    "id": "cus_qos_6r3-4I4zIiou2BVMHg",
    "name": "Jon Snow",
    "email": "dabastad@thewatch.org"
  },
  "plan": {
    "id": "oro",
    "name": "Plan Oro",
    "price": "15000.0",
    "currency": "CLP"
  },
  "created_at": "2017-05-17T19:12:57.189Z",
  "updated_at": "2017-05-17T19:12:57.189Z"
}
```

`GET /subscriptions/{subscription_id}`

Obtiene los detalles de una suscripción existente. Se necesita proporcionar sólo el identificador único de la suscripción el cual fue retornado al momento de su creación.

### Parámetros
|||
|--------- | -----------|
| subscription_id<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único de la suscripción. |


### Respuesta

Retorna un objeto de suscripción si se provee de un identificador válido.




## Actualizar una suscripción

> Ejemplo de llamada

````shell
curl --request PUT "https://api.qvo.cl/subscriptions/sub_HnKU4UmU5GtymRulcVOEow" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA" \
  -d plan_id="plata"
````


````javascript
const request = require('node-fetch');
fetch('http://api.qvo.cl/subscriptions/sub_HnKU4UmU5GtymRulcVOEow', { method: 'PUT'}, {
  plan_id: "plata"
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put 'http://api.qvo.cl/subscriptions/sub_HnKU4UmU5GtymRulcVOEow', params:
  {
    plan_id: "plata"
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('http://api.qvo.cl/subscriptions/oro', params={
  plan_id: "plata"
})

print r.json()
````

> Ejemplo de respuesta

```json
{
  "id": "sub_HnKU4UmU5GtymRulcVOEow",
  "status": "active",
  "current_period_start": "2017-05-17T19:12:57.185Z",
  "current_period_end": "2017-06-17T19:12:57.185Z",
  "customer": {
    "id": "cus_qos_6r3-4I4zIiou2BVMHg",
    "name": "Jon Snow",
    "email": "dabastad@thewatch.org"
  },
  "plan": {
    "id": "plata",
    "name": "Plan Plata",
    "price": "5000.0",
    "currency": "CLP"
  },
  "created_at": "2017-05-17T19:12:57.189Z",
  "updated_at": "2017-05-18T11:20:57.201Z"
}
```


`PUT /subscriptions/{subscription_id}`

Actualiza la suscripción especificada con los parametros provistos. Cualquier parámetro que no se provea quedará inalterado.

_TODO: Explicar debt_

### Parámetros
|||
|--------- | -----------|
| subscription_id<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único de la suscripción. |
| plan_id<p class="attr-desc">string</p> | Identificador único de un plan existente. |


### Respuesta

Retorna el objeto de suscripción si la actualización es exitosa. Retorna [un error](#errores) si algun parámetro de actualización es inválido.



## Cancelar una suscripción

> Ejemplo de llamada

````shell
curl -x DELETE "https://api.qvo.cl/subscriptions/sub_HnKU4UmU5GtymRulcVOEow" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA"
````


````javascript
const request = require('node-fetch');
fetch('http://api.qvo.cl/subscriptions/sub_HnKU4UmU5GtymRulcVOEow', { method: 'DELETE'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.delete 'http://api.qvo.cl/subscriptions/sub_HnKU4UmU5GtymRulcVOEow'
p JSON.parse(result)
````

````python
import requests

r = requests.delete('http://api.qvo.cl/subscriptions/sub_HnKU4UmU5GtymRulcVOEow')

print r.json()
````

> Ejemplo de respuesta

```json
{
  "id": "sub_HnKU4UmU5GtymRulcVOEow",
  "status": "active",
  "current_period_start": "2017-05-17T19:12:57.185Z",
  "current_period_end": "2017-06-17T19:12:57.185Z",
  "cancel_at_period_end": true,
  "customer": {
    "id": "cus_qos_6r3-4I4zIiou2BVMHg",
    "name": "Jon Snow",
    "email": "dabastad@thewatch.org"
  },
  "plan": {
    "id": "oro",
    "name": "Plan Oro",
    "price": "15000.0",
    "currency": "CLP"
  },
  "created_at": "2017-05-17T19:12:57.189Z",
  "updated_at": "2017-05-17T19:12:57.189Z"
}
```


`DELETE /subscriptions/{subscription_id}`

Cancela una suscripción. Por defecto, esta se cancelará (pasará al estado `canceled`) en la fecha especificada por el final del periodo de facturación o `current_period_end`.

### Parámetros
|||
|--------- | -----------|
| subscription_id<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único de la suscripción. |

### Respuesta

Retorna la suscripción si la operación fue exitosa con el parámetro `cancel_at_period_end = true`. Si el identificador de la suscripción no es válido, retornará [un error](#errores).



## Obtener una lista de suscripciones

> Ejemplo de llamada

````shell
curl --request GET "https://api.qvo.cl/subscriptions" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA"
````

````javascript
const request = require('node-fetch');
fetch('https://api.qvo.cl/subscriptions', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get 'https://api.qvo.cl/subscriptions'
p JSON.parse(result)
````

````python
import requests

r = requests.get('https://api.qvo.cl/subscriptions')

print r.json()
````

> Ejemplo de respuesta

```json
[
  {
    "id": "sub_HnKU4UmU5GtymRulcVOEow",
    "status": "active",
    "current_period_start": "2017-05-17T19:12:57.185Z",
    "current_period_end": "2017-06-17T19:12:57.185Z",
    "customer": {
      "id": "cus_qos_6r3-4I4zIiou2BVMHg",
      "name": "Jon Snow",
      "email": "dabastad@thewatch.org"
    },
    "plan": {
      "id": "oro",
      "name": "Plan Oro",
      "price": "15000.0",
      "currency": "CLP"
    },
    "created_at": "2017-05-17T19:12:57.189Z",
    "updated_at": "2017-05-17T19:12:57.189Z"
  }
]
```

`GET /subscriptions`

Retorna una lista de suscripciones activas. Las suscripciones se encuentran ordenadas por defecto por la fecha de creación, donde las mas recientes aparecerán primero.

<aside class="notice">
Este endpoint puede ser utilizado con <a href="#paginaci-n-filtros-y-orden">paginación, filtros y orden</a>
</aside>

### Respuesta

Un arreglo donde cada entrada representa a una suscripción con su respectiva información.

