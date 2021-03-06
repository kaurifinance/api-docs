- [Обработка запросов](#обработка-запросов)
- [Публичные данные](#публичные-данные)
  - [Получение списка активных валют](#получение-списка-активных-валют)
  - [Получение списка активных пар](#получение-списка-активных-пар)
  - [Получение цен](#получение-цен)
  - [Подсчёт стоимости обмена](#подсчёт-стоимости-обмена)
- [Пользовательские данные](#пользовательские-данные)
  - [Создание аккаунта](#создание-аккаунта)
  - [Виды аккаунтов](#виды-аккаунтов)
  - [Виды авторизации](#виды-авторизации)
    - [JWT авторизация](#jwt-авторизация)
    - [Авторизация с помощью подписи запроса](#авторизация-с-помощью-подписи-запроса)
  - [Получение баланса](#получение-баланса)
  - [Получение настроек по аккаунту](#получение-настроек-по-аккаунту)
- [Заявки](#заявки)
  - [Получение деталей по заявке](#получение-деталей-по-заявке)
  - [Получение истории по заявкам](#получение-истории-по-заявкам)
  - [Callback нотификация](#callback_нотификация)
  - [Заявка на депозит](#заявка-на-депозит)
    - [Схема работы](#схема-работы-депозитной-заявки)
    - [Получение настроек](#получение-настроек-по-депозитной-заявке)
    - [Получение адреса для пополнения](#получение-адреса-для-пополнения)
    - [Специфические параметры](#специфические-параметры-депозитной-заявки)
    - [Детали заявки при callback нотификации](#детали-заявки-при-callback-нотификации)
    - [Получение деталей по депозитной заявке](#получение-деталей-по-депозитной-заявке)
  - [Заявка на вывод](#заявка-на-вывод)
    - [Схема работы](#схема-работы-заявки-на-вывод)
    - [Получение настроек](#получение-настроек-по-заявке-на-вывод)
    - [Создание заявки](#создание-заявки-на-вывод)
    - [Отмена заявки](#отмена-заявки-на-вывод)
    - [Повторение заявки](#повторение-заявки-на-вывод)
    - [Специфические параметры](#специфические-параметры-заявки-на-вывод)
    - [Получение деталей](#получение-деталей-по-заявке-на-вывод)
    - [Детали заявки при callback нотификации](#детали-заявки-на-вывод-при-callback-нотификации)
  - [Заявка на внутренний перевод](#заявка-на-внутренний-перевод)
    - [Схема работы](#схема-работы-заявки-на-внутренний-перевод)  
    - [Получение настроек](#получение-настроек-по-заявке-на-внутренний-перевод)
    - [Создание заявки](#создание-заявки-на-внутренний-перевод)
    - [Повторение заявки](#повторение-заявки-на-внутренний-перевод)
    - [Получение деталей по заявке](#получение-деталей-по-заявке-на-внутренний-перевод)
    - [Детали заявки при callback нотификации](#детали-заявки-на-внутренний-перевод-при-callback-нотификации)
  - [Заявка на создание счёта(invoice)](#заявка-на-создание-счёта) 
    - [Схема работы](#схема-работы-заявки-на-создание-счёта)
    - [Получение настроек](#получение-настроек-по-заявке-на-создание-счёта)
    - [Создание счёта](#создание-счёта)
    - [Получение деталей](#получение-деталей-по-счёту)
    - [Детали заявки при callback нотификации](#детали-заявки-на-создание-счёта-при-callback-нотификации)
  - [Заявка на обмен](#заявка-на-обмен)
    - [Разновидности обменов](#разновидности-обменов)
    - [Получение настроек](#получение-настроек-по-заявке-на-обмен)
    - [Создание обмена](#создание-обмена)
    - [Отмена лимитного обмена](#отмена-лимитного-обмена)
    - [Повтор лимитного обмена](#повтор-лимитного-обмена)
    - [Получение деталей](#получение-деталей-по-обменной-заявке)
    - [Детали заявки при callback нотификации](#детали-заявки-по-обмену-при-callback-нотификации)
  



## Обработка Запросов
* Базовый api url - https://api.kauri.finance/
* Content-Type - json

Каждый ответ содержит структуру, в которой есть поле "status" - которое отвечает за удачно обработанный запрос, или нет. Удачно обработанный ответ имеет статус-код - 2XX, не удачно - или 4XXX, или 5XX.

###### Пример удачно обработанного запроса:

```javascript
 {"status": "success"}
```

###### Пример не удачно обработанного запроса:

```javascript
 {"status": "error", "error": <имя ошибки>}
```

Кодов ошибок нету, есть только словестно описанная причина.
По-умолчанию, все ошибки возвращаються на английском языке.
Есть возможность локализировать ошибки на русский язык, добавив к самому запросу след.заголовок - "Accept-Language" со значением "ru"

# Публичные Данные
## Получение списка активных валют

```javascript
 GET "/api/v1/currency"
```
###### Пример ответа :

```javascript
{
  "status": "success",
  "currencies": ["BTC","EUR",...]
}

```
Система возвращает список валют, которые на данный момент активны и имя самой валюты, как она идентифицированна в системе

## Получение списка активных пар
```javascript
GET "/api/v1/pair"
```

###### Пример ответа :

```javascript
{
  "status": "success",
  "pairs": [
    [
      {
        "currency_to_spend": "UAH",
        "currency_to_get": "BTC",
        "name": "BTC_UAH",
        "base_currency": "BTC"
      }
    ],
```

API ендпоинт возвращает список активных пар, по которым можно совершать обмены.

**Расшифровка названия пары:**

Обычно в обмене принимают участие две валюты, одна - которую человек тратит, другая - которую получает.
В рамках текущего примера, пара "BTC_UAH" расшифроваеться как покупка BTC за UAH.
Для покупки, UAH за BTC - нужно использовать другую пару - "UAH_BTC". По-факту, у нас - одна пара, это одно направление обмена

## Получение цен


```javascript
 GET "api/v1/exchange_rate"
```

###### Пример ответа :

```javascript
{  
  "rates": [  
    {  
      "pair": "UAH_EUR",  
      "base_currency_price": 0.03800836,  
      "price": 26.31  
    }  
  ]  
}                              
																						
```

По текущему API ендпоинту, можно получить все цены по всем парам на обмен(ticker)


## Подсчёт стоимости обмена

```javascript
 GET "api/v1/exchange/calculate"
```

###### Параметры:

```javascript
currency_to_get - обязательный. Валюта, которую пользователь получает
currency_to_spend - обязательный. Валюта, которую пользователь тратит
currency_to_get_amount, currency_to_spend_amount - нужно указать один из параметров для подсчёта, либо "размер, валюты которую нужно получить", либо "размер валюты которую пользователь хочет потратить"
exchange_price - необязательный параметр. Можно указать цену для обмена, если не указываеться цена, берёться цена по рынку.
```

###### Пример ответа:

```javascript
{
  "currency_to_get_amount": 1,
  "currency_to_get": "BTC",
  "currency_to_spend_amount": 202170.7475,
  "currency_to_spend": "UAH",
  "status": "success",
  "exchange_price": 202170.7475
}
```
При каждом просчёте в ответе всегда возращаеться подсчитанный обмен(цена обмена, сколько будет потрачено и какой валюты и сколько будет получено)

# Пользовательские данные
## Создание аккаунта

```javascript
  POST "api/v1/user/create"
```

###### Параметры:

```javascript
{
    "email": "string",
    "username": "string",
    "password": "string",
}                                                  

```

Все указанные выше поля являються обязательные к заполнение. После успешного выполнения апи запроса - нужно подтвердить email(письмо будет отправлено на почту), только после подтверждения емейла - можно проходить авторизацию.
В теле письма, есть ссылка на которую нужно нажать чтобы подтвердить email. Время жизни ссылки - 1 день

## Виды аккаунтов
После того, как пользователь подтвердил своей емейл, его аккаунт становиться - "NOT_VERIFIED"
После прохождения верификации, аккаунт меняеться на "VERIFIED"
Есть третий вид аккаунта, как бизнес-пользователь(мерчант) - "BUSINESS"

## Виды авторизации
На данный момент времени, есть два вида авторизации по АПИ - c помощью JWT токена и с помощью подписи запроса через api_key и api_secret.
Сам пользователь уже выбирают какой авторизацией пользоваться. Мы рекомендуем пользоваться подписью запроса.

### JWT авторизация

```javascript
POST "api/v1/user/obtain_token"
```
###### Параметры:

```javascript
{
  "email": "string",
  "password": "string"
}                                              

```
###### Пример удачного ответа(полученного токена:
```javascript
{
  "username": "<username>",
  "token": "<token>"
}
```
После того, как был получен токен, можно выполнять запросы,которые требуют прохождения авторизации.
Токен нужно указывать в заголовке --header 'Authorization: Bearer <token> . Время жизни токена - 15 минут. 
В том же формате указывается токен для "Swagger"(через кнопку Authorize), чтобы он перегрузился и показал все доступные методы, которые разрешены пользователю.
	
После истечения срока жизни токена, нужно его "переполучить", через "obtain token" метод

### Авторизация с помощью подписи запроса
После прохождения верификации - будут предоставлены api_key и api_secret.
Для того, чтобы пользоваться авторизацией через подпись запроса, нужно передавать два заголовка:

```javascript
--header 'Sign: <generated_signature>' --header 'Key: <api_key>'                                          
```
###### Алгоритм создания подписи:
**Шаг 1:**  Нужно отсортировать параметры запроса в алфавитном порядке, если есть вложенность в параметрах, то её преобразовать.

**Пример без вложенности:**

```javascript
{
  "currency": "string",
  "amount": "string"
}							
```
В данном случае, должен получиться словарь, но уже с отсортированными ключами:

```javascript
{
  "amount": "string",
  "currency": "string"
}							
```

**Пример если есть вложенность:**
```javascript
{
  "currency": "string",
  "amount": "string",
  "additional_info": {"client_ip": "8.8.8.8"}
}
```

**Трансформируеться в словарь след.вида:**
{
  "currency": "string",
  "amount": "string",
  "additional_info_client_ip": "8.8.8.8"
}
Ключи полученного словаря, нужно отсортировать в альфавитном порядке.


**Шаг 2:**  Создается строка на подпись в таком формате:

```javascript
{request.method} - {request.path} - {sorted_params}
```

**Шаг 3:**  Подписывается строка api_secret, с помощью алгоритма - hmac_sha_256
Подобные манипуляции нужно проводить с каждым запросом

## Получение баланса

```javascript
  GET "api/v1/user/balance"
```
###### Пример ответа :

```javascript
{
"wallets": {
    "USDT": {
      "address": "0x85E12eA5270C8848D9258FB76de475144dBC1E3e",
      "qr_file_data": img in base64
    },
    ...
  },
  "balance": {
    "EUR": {
      "currency": "EUR",
      "EUR": {
        "reserved": 0,
        "total": 0
      },
      "ETH": {
        "reserved": 0,
        "total": 0
      },
      "UAH": {
        "reserved": 0,
        "total": 0
      },
      "USDT": {
        "reserved": 0,
        "total": 0
      },
      "USD": {
        "reserved": 0,
        "total": 0
      },
      "RUB": {
        "reserved": 0,
        "total": 0
      },
      "BTC": {
        "reserved": 0,
        "total": 0
      }
    },
    ...
  }
}                                                  

```
В балансе приходят крипто-адреса, которые можно пополнять, получается это адреса закреплены за пользователем. Также приходит сам баланс - есть два поля : "total", "reserved". "Total" - означает общее количество средств, "Reserved" - количество средств, которое уже занято, находиться в заявках. По балансу можно получить сколько есть средств на данный момент по конкретной валюте, плюс можно получить пересчёт средств одной валюты в другую.

**Например:**

1) Получение сколько есть "EUR" на аккаунте - balance[‘EUR’][‘EUR’]

2) Получение сколько есть "EUR" в "ETH" - balance[‘EUR’][‘ETH’]


## Получение настроек по аккаунту
```javascript
  GET "api/v1/user/account_info"
```

```javascript
  {
  "name": "Свят",
  "email": "svyatoslavkravchenko@gmail.com",
  "account_type": "VERIFIED",
  "is_email_verified": true,
  "referral_id": "89f67887-cae6-4a6f-a393-a89079878a57",
  "created": "2019-02-05T08:13:48.952334",
  "is_2fa_enabled": false,
  //limits, fee, processing_rules
  }
```

В ответе приходит имя пользователя, его емейл, тип аккаунта, верифицирована ли почта, включена ли двух-факторная авторизация, также по каждому виду заявок приходят лимиты, фии, и т.д. По каждой заявке будет отдельно рассматриваться

# Заявки
## Получение деталей по заявке

При создании заявки через АПИ, система отдает order_id заявки, по которой можно узнать детали

```javascript
GET "api/v1/orders/detail"
```
###### Параметры:

```javascript
{
  "order_id" : $order_id
}						
```
В ответе можно будет получить детали по заявке, если заявку создавал конкретный аккаунт или аккаунт участвовал в этой заявке. Есть заявки, где участвуют несколько аккаунтов

В главе, по каждому из виду заявок, будет приводиться пример что конкретно каждая из заявок возвращает.

## Получение истории по заявкам

```javascript
GET "api/v1/orders/history"
```
###### Пример ответа:

```javascript
{
  "orders": [<orders_details_list>]
  "status": "success",
  "pages_count": 78
}
```
Для истории заявок присуствует постраничный вывод, на одной странице выводиться по 10 заявок.

###### Фильтра:
 - order_type - означает тип заявки. Возможные значения - `'DEPOSIT’, ‘WITHDRAWAL’, ‘EXCHANGE’, ‘INTERNAL_MOVEMENT’, ‘INVOICE'` 
 
 - order_status - означает статус заявки. Возможные значения - `‘NEW’, ‘ERROR’, ‘CLOSED’, ‘EXPIRED’, ‘CANCELLED’, ‘CANCELLING’, ‘WAITING_FOR_OPERATOR_CONFIRMATION’, ‘CONFIRMED_BY_OPERATOR’, ‘CANCELLED_BY_OPERATOR’, ‘WAITING_FOR_CONFIRMATION’, ‘WAITING_FOR_PRICE’, ‘PAYMENT_IN_PROGRESS’`

- order_sub_type - означает под-тип заявки. У некоторых заявок есть свой под-тип, по которому можно сделать фильтр
- page - указание страницы для вывода
- from_timestamp, till_timestamp - фильтрация по времени создания заявок
- currency - фильтрация по валюте.Отображает все заявки в которых принимала участие та или иная валюта
- address - находит все заявки в которых фигурировал адрес. Это может быть заявки на пополнения или вывод

### Callback нотификация
При создании заявки, есть возможность указать url для нотификации, когда статус заявки поменяеться.
При callback информировании, отсылаеться POST запрос на адрес, который был указан. Успешной обработкой запроса - будет 200-ый ответ, если возникает ошибка система пытаеться 3 раза с интервалом в 5 минут отправить callback

## Заявка на депозит
### Схема работы депозитной заявки

Для того, чтобы пополнить аккаунт, нужно изначально получить аддрес для пополнения, после этого перевести деньги на этот счёт, это может быть как крипто-валютный адрес, так ссылка для оплаты картой. После успешного пополнения - будет создана депозитная заявка, получаеться заявка создаеться "пост-фактом".

#### Пример переходов статусов по крипто-валютам(UAH):
Успешное пополнение(зачисление денег) - "NEW->WAITING_FOR_CONFIRMATION->CLOSED"

Как только есть транзакция в сети, заявка переходит в статус "NEW", а потом в статус "WAITING_FOR_CONFIRMATION", и находиться в этом статусе до тех пор пока не будет достигнуто определённого количества подтверждений для зачисления денег на баланс. Заявка может перейти в статус "EXPIRED", если в течении суток не было достугниуто нужного количества подтверждений по транзакции

#### Пример переходов статусов по фиатным валютам(UAH):
Успешное пополнение(зачисление денег) - "NEW->CLOSED" 

Пополнение не удалось - "NEW->ERROR" 

Ссылка перестала быть активной "NEW>EXPIRED(CANCELLED)"

### Получение настроек по депозитной заявке

```git
GET "api/v1/user/account_info"
```

Есть три вида настроек - "fees", "limits", "processing_rules"

#### Лимиты

```javascript
"deposit_order_limits": {
    "UAH": {
      "GATEWAY": {
        "P2P": {
          "max_amount": 14000,
          "min_amount": 10
        }
      }
    }
  }
 ``` 
На данный момент есть лимиты на пополнения есть только для фиатных валют, указываеться лимит за операцию. В данном примере показываються лимит на пополнение "UAH", по типу пополнения - "P2P".


#### Fee

```javascript
"deposit_order_fees": {
	"BTC": {
          "GATEWAY": {
            "P2P": {
             "payment_provider_static_fee": null,
             "static_fee": 0,
             "percent_fee": null
        }
      }
    },
}													
```
Показывает какие есть фии по конкретной валюте на пополнение.

    static_fee - показывает статическое значение, которое берёться в рамках депозита
    percent_fee - показывает значение, которое берёться в рамках депозита в процентном соотношении
    payment_provider_static_fee - стоимость работы провайдера на пополнение, обычно указываеться с каким-то значением(static_fee, или percent_fee)
    
#### Processing rules

```javascript
"deposit_order_processing_rules": {
	"BTC": {
          "GATEWAY": {
            "P2P": {
              "is_deposit_enabled": true,
              "confirmations_count": 2
        }
      }
    },
}													
```
Показывает, включен ли депозит,"confirmations_count" - для фиатных валют не имеет значения, для крипто-валюты показывает по скольким подтверждениям идет зачисления депозита.

### Получение адреса для пополнения

```javascript
POST "api/v1/deposit/address"
```

###### Параметры:

```javascript
{
  "amount_to_spend": "string",
  "callback_url": "string",
  "payment_type": "string",
  "currency": "string",
  "amount_to_receive": "string",
  "additional_info": {},
  "comment": "string"
}
```
**Описание параметров:**

 1. `currency - валюта, должна быть указана(обязательный параметр)`
 2. `callback_url - url для нотификации при создании депозитной заявки(не обязательный параметр)`
 3. `amount_to_spend, amount_to_receive - нужно указать один из этих параметров. В первом случае, система создаст ссылку на пополнение с учетом того сколько клиент может потратить, а во втором случае баланс будет пополнен на это значение(amount_to_receive). Нужно указывать эти поля только для пополнения фиатных валют`
 4. `comment - комментарий, которы будет указываться при создании заявки по конкретному адресу, в колл-беке будет приходить - (не обязательный параметр)`
 6. `payment_type - способ пополнения, если не указываеться берёться по-умолчанию P2P`
 7. `additional_info - словарь, с доп.параметрами. customer_id - не обязательный параметр, client_ip - обязательный параметр, deposit_email или deposit_phone нужно указывать если у вас статус аккаунта - "BUSINESS"`


###### Пример получение депозитного адреса для крипто-валюты:

```javascript
{
  "currency": "BTC",
  "callback_url": "http://",
  "additional_info": {"client_ip": "1.1.1.1",
	              "customer_id": "<some_id>"}
}
```

###### Пример получения депозитного адреса для UAH:

```javascript
{
  "amount_to_spend": "10", 
  "callback_url": "http://",
  "currency": "UAH",
  "additional_info": {
	"client_ip": "62.80.170.214",
	"deposit_email": "<some_email>"
    }
}
```

###### Анализ ответа :

```javascript
{
   "qr": "base64 img",
   "addr": "адрес для пополнения или ссылка",
   "status": "success"
}
```

"qr" будет заполнен только для крипто-валюты

### Специфические параметры депозитной заявки

 1. `address - адрес пополнения`
 2. `status - статус заявки`
 3. `order_id - order_id в системе, по которому можно получить детали заявки`
 4. `customer_id - клиентский id`
 5. `amount - сумма пополнения`
 6. `received_amount - сумма которая была зачислена на аккаунт`
 
### Детали заявки при callback нотификации

```javascript
{"status": "CLOSED", 
 "customer_id": "37750", 
 "received_amount": 0.02206137, 
 "comment": null, 
 "address": "32ssDLdkZngu4gJ1gdmSFWp16AGmfaCnML", 
 "order_id": "0a6282ec-f63d-4a15-a16c-a128b46eb7eb", 
 "currency": "BTC", 
 "tr_hash": "ffb7c8fb3acc13b1cdd924c8ae1bc953c0c81c4eedc643ad104ecfd2f0e45481", 
 "amount": 0.02206137, 
 "confirmations_count": 1}
``` 
 
 ### Получение деталей по депозитной заявке
 
 ###### Пример

```javascript
{
  "external_id": "92ba1fb2-b0af-4281-89e9-21f47ae16874",
  "order_type": "DEPOSIT",
  "status": "CLOSED",
  "fee": 5.15,
  "details": {
		"fee": 5.15,
		"address": "https://mapi.xpay.com.ua/ru/frame/widget/e89ce23c-4d5b-4124-897a-84e75ea972c9",
		"tr_id": "e89ce23c-4d5b-4124-897a-84e75ea972c9",
		"comment": null
	     },
  "currency": "UAH",
  "confirmations_count": null,
  "order_sub_type": "GATEWAY",
  "amount": 10,
  "dt": "2020-02-04 20:11:13.860751",
  "comment": null,
  "tr_hash": "e89ce23c-4d5b-4124-897a-84e75ea972c9"
}
```

## Заявка на вывод
### Схема работы заявки на вывод

При успешном создании заявки на вывод, заявка автоматически переходит в статус - "NEW".

При успешном выводе, заявка меняет статус на "CLOSED". Это финальный статус, который означает успех.

При ошибке вывода, заявка переходит в статус - "ERROR"

Есть возможность отменить заявку, если транзакция/транзакции  на вывод не были выполнены в полном обьеме.

При успешном принятии запроса на отмену, статус заявки переходит в "CANCELLING", при отмене заявка переходит в "CANCELLED"

При выводе фиата, сумма вывода может разбиваться на несколько транзакций и могут быть ситуации, когда часть транзакций успешны, часть нет, в таком случае создаеться две заявки, одна со статусом "CLOSED", в которой фигурирует количество средств, которое было успешно выведено, вторая заявка со статусом - "ERROR", в которой фигурирует количество средств, которые не вывелись

### Получение настроек по заявке на вывод

```git
 GET "api/v1/user/account_info"
```

###### Позволяет получить, значения лимитов, фии, включен ли вывод:

```javascript
withdrawal_order_processing_rules": {
	"USDT": {
		  "GATEWAY": {
		    "is_cancel_enabled": true,
		    "is_repeat_enabled": true,
		    "is_withdrawal_enabled": true
		   }
	},
	...
}
```
Показывает включен ли вывод, включена ли отмена вывода, включено ли повторение вывода

```javascript
"withdrawal_order_fees": {
	"UAH": {
		"GATEWAY": {
		   "parent_currency_static_fee": null,
		   "static_fee": null,
		   "percent_fee": 0.5
		},
	},
	...
}
```
Показывает какие установленные комиссии. 

Возможны след. вариации:

 - `static_fee - снимаеться статическое значение при выводе` 
 - `percent_fee - снимаеться в процентном сотношении от размера вывода`
 - `parent_currency_static_fee - снимаеться статическое значении, если
    для вывода какой-то валюты может платиться комисия в другой валюте. Как пример, это может быть какой-то ERC-20 токен`

```javascript
"withdrawal_order_limits": {
	"USDT": {
		"GATEWAY": {
		    "min_amount": 10,
		    "max_amount": 10000
		}
	}, 
	...
}
```
В данном случае показаны лимиты за операцию


### Создание заявки на вывод

```git
 POST "api/v1/withdrawal"
```

###### Параметры:

```javascript
{
	"currency": "string",
	"withdrawal_type": "string",
	"comment": "string",
	"mode": "string",
	"callback_url": "string",
	"additional_info": {},
	"amount": 0,
	"wallet_to": "string"
}
```

**Анализ параметров:**

 - `currency - валюта, обязательный параметр`
 - `withdrawal_type - тип вывода, обязательный параметр. Для вывода на карты или на крипто-валютные адреса, нужно указывать - "GATEWAY"`
 - `comment - комментарий к выводу, не обязательный параметр`
 - `callback_url - url, для нотификации, не обязательный параметр. Если он указан, то будут приходить нотификации с обновлением статусов по конкретной заявке`  
 - `amount - сумма для вывода, обязательный параметр`  
 - `wallet_to - адрес кошелька, обязательный параметр`
 - `additional_info - словарь, с доп.параметрами. client_ip - не обязательный параметр, withdrawal_email нужно указывать если у вас статус аккаунта - "BUSINESS"`

**Примеры:**

###### Создания заявки для вывода(UAH):

```javascript
{
   "currency": "UAH",
   "withdrawal_type": "GATEWAY",
   "comment": "comment",
   "callback_url": "http://",
   "additional_info": {"withdrawal_email": $customer_email},
   "amount": 100,
   "wallet_to": $card_number
}
```

###### Создания заявки для вывода(крипто-валюта):

```javascript
{
   "currency": "BTC",
   "withdrawal_type": "GATEWAY",
   "comment": "comment",
   "callback_url": "http://",
   "amount": 100,
   "wallet_to": $btc_addr
}
```

В ответ на создания заявки, апи отдает order_id - ID заявки.

### Отмена заявки ни вывод

Заявку на вывод можно отменить, если сама отмена разрешена и заявка находиться в процессе выполнения
Если сам вывод уже совершен(транзакция) уже была отправлена, то саму транзакцию отменить нельзя. Можно успеть отменить до фактического вывода.

###### URI

```javascript
 POST "api/v1/withdrawal/cancel"
```

###### Параметры:

```javascript
{
  "order_id": "string"
}
```

Если получилось отменить заявку - системы выдаст 200-ый ответ, в другом случае - будет ошибка.

### Повторение заявки на вывод

Есть возможность повторить заявку на вывод, если повторение включено и сама заявка завершилась

```javascript
 POST " /api/v1/withdrawal/repeat            "
```

###### Параметры:

```javascript
{
  "amount": 0,
  "order_id": "string"
}
```

Обязательное для указания - order_id. Можно указать amount, он изменит сумму для вывода в рамках новой заявки.

### Специфические параметры заявки на вывод

1. `amount - количество средств, которое было снято с баланса пользователя`
2. `amount_to_withdrawal - фактическая сумма вывода`
3. `withdrawal_transactions - список успешных транзакций`
4. `address - адрес вывода. В рамках фиатной валюты пишуться последние 4 цифры`
5. `dt - дата закрытия заявки`

### Получение деталей по заявке на вывод
```javascript
{
      "details": {
        "comment": "",
        "address": "0997",
        "fee": 2.9
      },
      "amount": 582.9,
      "order_sub_type": "GATEWAY",
      "dt": "2020-04-09 13:43:47.531414",
      "comment": "",
      "status": "CLOSED",
      "external_id": "0bf77841-fe66-4a50-aa6a-129cde64c9aa",
      "amount_to_withdrawal": 580,
      "order_type": "WITHDRAWAL",
      "withdrawal_transactions": [
        580
      ],
      "currency": "UAH"
    },
```

### Детали заявки на вывод при callback нотификации
```javascript
{"withdrawal_transactions": [0.03562889], 
"comment": "some_comment", 
"order_type": "WITHDRAWAL", 
"currency": "BTC", 
"dt": "2020-04-09 16:14:12.076628", 
"status": "CLOSED", 
"order_sub_type": "GATEWAY", 
"amount_to_withdrawal": 0.03562889, 
"details": {"tr_id": "2a834817d524f8dde54fb9c4e1d5d3ba4839bc81495ed5d1e2bebb1ebeffc23d", 
            "comment": "some_comment", 
	    "tr_hash": "https://www.blockchain.com/btc/tx/2a834817d524f8dde54fb9c4e1d5d3ba4839bc81495ed5d1e2bebb1ebeffc23d",             "fee": 0.0002, 
	    "address": "14ckdLFzj3ba4FSQiW1fSGKURycqc5gNQE"
	    }, 
"amount": 0.03582889, 
"external_id": "02241379-109d-4c49-965d-6eea8de164c7"}
```
## Заявка на внутренний перевод
### Схема работы заявки на внутренний перевод
Данный тип заявки предполагает перевод средств между пользователями на платформе. К примеру у пользователя "A" есть 1000 USD, зная email получателя, можно мгновенно перевести 1000 USD.

У самой заявки возможны след. статусы:

"NEW" - заявка в процессе выполнения

"CLOSED" - успешно закрыта

"ERROR" - закончилась с ошибкой

### Получение настроек по заявке на внутренний перевод
```javascript
 GET "api/v1/user/account_info"
```

##### Позволяет получить, значения лимитов, фии, включено ли перемещение средств:

```javascript
"internal_movement_processing_rules": {
    "UAH": {
      "is_repeat_enabled": true,
      "is_enabled": true
    },
	...
}
```
Показывает включено ли перемещение средств внутри платформы, включено ли повторение операции

```javascript
"internal_movement_fees": {
   "UAH": {
      "static_fee": 0,
      "percent_fee": 0
    },
	...
}
```
Показывает какие установленные комиссии. 
Комиссия снимаеться с отправителя

Возможны след. вариации:

 - `static_fee - снимаеться статическое значение при переводе` 
 - `percent_fee - снимаеться в процентном сотношении от размера перевода`

```javascript
"internal_movement_limits": {
  "UAH": {
      "max_amount": 1000000,
      "min_amount": 0
    },
	...
}
```
В данном случае показаны лимиты за операцию. Размер перевода не должен выходить за границу указанных цифр.


### Создание заявки на внутренний перевод

```javascript
 POST "api/v1/internal_movement"
```

###### Параметры:

```javascript
{
  "comment": "string",
  "amount": "string",
  "callback_url": "string",
  "currency": "string",
  "destination_account_email": "string"
}
```

**Анализ параметров:**

 - `currency - валюта, обязательный параметр`
 - `comment - комментарий к выводу, не обязательный параметр`
 - `callback_url - url, для нотификации, не обязательный параметр. Если он указан, то будут приходить нотификации с обновлением статусов по конкретной заявке`  
 - `amount - сумма для вывода, обязательный параметр`
 - `destination_account_email - email получателя средств на платформе`
 
 При удачном создании ,в ответе будет order_id созданной заявки 
 
 ### Повторение заявки на внутренний перевод

Есть возможность повторить заявку на внутренний перевод, если повторение включено и сама заявка завершилась

```javascript
 POST "/api/v1/internal_movement/repeat"
```

###### Параметры:

```javascript
{
  "amount": 0,
  "order_id": "string"
}
```

Обязательное для указания - order_id. Можно указать amount, он изменит сумму для перевода в рамках новой заявки.

 ### Получение деталей по заявке на внутренний перевод
 
```javascript
      "details": {
        "comment": "",
        "destination_account": "destination_account",
        "source_account": "source_account"
      },
      "amount": 266,
      "fee": 0,
      "dt": "2020-03-20 22:23:52.977529",
      "status": "CLOSED",
      "external_id": "021b33c6-060a-4018-be71-57088ce81d2e",
      "order_type": "INTERNAL_MOVEMENT",
      "currency": "USDT"
    },
```

 ### Детали заявки на внутренний перевод при callback нотификации
 ```javascript
 {"details": 
    {"destination_account": "2@gmail.com", 
     "comment": "string", 
     "source_account": "1@gmail.com"
     }, 
  "fee": 0.01, 
  "dt": "2020-04-08 22:22:40.733016", 
  "currency": "UAH", 
  "order_type": "INTERNAL_MOVEMENT", 
  "external_id": "aaf4a18f-9148-4b09-a069-2f543a1f0c70", 
  "status": "CLOSED", 
  "amount": 1.01, 
  "order_sub_type": null
  }
 ```
 
 ## Заявка на создание счёта
### Схема работы заявки на создание счёта
Платформа позволяет создавать счёта для оплаты пользователям их услуг.
Например, магазин может выставить счёт на оплату товара или услуг, и отдать оплачивать этот счёт пользователю магазина.
На данный момент оплата такого счёта возможна только в случае, когда у пользователя, есть аккаунт на kauri.finance и там хватает средств.

#### Этапы работы со счётом:

1) создаеться счёт(генериться ссылка для оплаты)
2) пользователь переходит по ссылке(логиниться на сайте kauri.finance) и может оплатить в той валюте, в который был создан счёт, или любой другой валютой


#### Возможные статусы :

1) "NEW" - счёт создан
2) "PAYMENT_IN_PROGRESS" - оплата в процессе. Ожидание финального статуса
3) "CLOSED" - счёт учспешно оплачен
4) "ERROR" - счёт неудалось оплатить
5) "EXPIRED" - счёт прекратил существование. По истичении времени в 900 секунд счёт перестает быть активным


### Получение настроек по заявке на создание счёта

```javascript
GET api/v1/user/account_info
 ```
 
#### Получение настройки активно ли создание заявки
  ```javascript
 "invoice_order_processing_rules": {
    "UAH": {
      "is_enabled": true
           },
      }
  ```
  Показывает, включено ли создание счёта по той или иной валюте
  
  
#### Получение настройки по фии
```javascript
"invoice_order_fees": {
    "UAH": {
      "percent_fee": 0
    },
  ```
 Показывает, какой размер фии и как будет подсчитоваться фии для каждого счёта
 
 
#### Получение настройки по лимитам за операцию
```javascript
"invoice_order_limits": {
    "UAH": {
      "max_amount": 148500,
      "min_amount": 81
    },
  ```
 Показывает, в границах каких лимитов счёт на какую сумму может быть создан
 
 ### Создание счёта
 ```javascript
 POST api/v1/invoice
 ```
 
 #### Параметры
 ```javascript
 {
  "comment": "string" - не обязательный параметр
  "amount": "string" - сумма счёта(обязательный параметр)
  "currency": "string" - обязательный параметр
  "payment_option": "string" - не обязательныей параметр. Показывает, возможные варианты оплаты этого счёта.
  
  Есть 3 опции - "CRYPTO", "FIAT", "ALL". Если не указывать этот параметр, то по-умолчанию будет установлена возможность оплаты счёта всеми возможными средствами(через kauri.finance и не только).
  
  Если установлено - "FIAT" - оплата средствами kauri.finance + есть возможность оплатить картой
  Если установлено - "CRYPTO" - оплатама средствами kauri.finance + есть возможность оплатить крипто-валютой
  
  "pay_account_email":  - обязательный параметр. На этот емейл приходит email с информацией по счёту.
  "additional_info" - не обязательный параметр(словарь из доп.полей). "callback_url", "success_url", "fail_url". 
    "callback_url" - используеться для нотификаций
    "success_url" - используеться для редиректа на страницу клиента при успешной оплате
    "fail_url" - используеться для редиректа на страницу клиента при неуспешной оплате
}
```

#### Пример ответа при успешно созданном счёте
 ```javascript
 {
  "url": "https://kauri.finance/invoice/cf700d3b-20b4-4b33-b195-38709b7e51fa",
  "order_id": "cf700d3b-20b4-4b33-b195-38709b7e51fa",
  "status": "success"
}
```
Для того, чтобы оплатить пользователю нужно пройти по указанной ссылке, залогиниться в "kauri.finance", выбрать какой валютой оплатить, и пройти процесс оплаты


### Получение деталей по счёту
Детали по счёту, может видеть аккаунт, который создавал счёт и аккаунт, который оплачивал.
```javascript
{
      "internal_id": 164554,
      "details": {
        "comment": null,
        "destination_account": "Svyat_merchant",
        "source_account": null
      },
      "url": "https://kauri.finance/invoice/cf700d3b-20b4-4b33-b195-38709b7e51fa",
      "order_sub_type": null,
      "dt": "None",
      "amount": 100,
      "status": "NEW",
      "external_id": "cf700d3b-20b4-4b33-b195-38709b7e51fa",
      "order_type": "INVOICE",
      "fee": 0,
      "currency": "UAH"
    }
```

### Детали заявки на создание счёта при callback нотификации
```javascript
{"order_type": "INVOICE", 
 "dt": "2020-04-07 21:54:57.185155", 
 "url": "https://kauri.finance/invoice/3542e3c2-4bab-48b8-bfbb-2b95b88c8a7a", 
 "internal_id": 163787, 
 "order_sub_type": null, 
 "amount": 100.0, 
 "status": "EXPIRED", 
 "fee": 0.0, 
 "currency": "UAH", 
 "details": {
       "destination_account": "Merchant_test", 
       "comment": "Bot_operation_100_UAH", 
       "source_account": <some_account>}, 
 "external_id": "3542e3c2-4bab-48b8-bfbb-2b95b88c8a7a"}
```

## Заявка на обмен
### Разновидности обменов
Платформа позволяет совершать два разных вида обмена:

1) Обмен по рынку(под-тип заявки - "MARKET_EXCHANGE")
2) Обмен при достижении указанной цены - (под-тип заявки - "LIMIT_EXCHANGE")

При рыночном обмене возможны след.статусы:
1) "NEW" - заявка создана
2) "CLOSED" - обмен прошел успешно
3) "ERROR" - возникла ошибка, при обмене

При лимитном обмене возможны след.статусы:
1) "NEW", "WAITING_FOR_PRICE" - ожидание цены на платформе
2) "CLOSED" - обмен успешно произведен
3) "ERROR" - возникла ошибка при обмене
4) "CANCELLING" - обмен был отправлен на отмену
5) "CANCELLED" - обмен отменен


### Получение настроек по заявке на обмен

```javascript
GET api/v1/user/account_info
```

#### Получение настроек по доступности обменных операций
```javascript
"exchange_order_processing_rules": {
    "EUR_USD": {
      "is_market_exchange_enabled": true,
      "is_cancel_enabled_for_limit_exchange": false,
      "is_repeat_enabled_for_limit_exchange": false,
      "is_limit_exchange_enabled": true
    },
```
"is_market_exchange_enabled" - показывает, включен ли обмен по рынку

"is_limit_exchange_enabled" - показывает, включен ли обмен с заказом цены

"is_cancel_enabled_for_limit_exchange" - включена ли отмена для лимитного обмена

"is_repeat_enabled_for_limit_exchange" - вклчено ли повторение для лимитного обмена

#### Получение настроек по лимитам на обменную операцию
```javascript
"exchange_order_limits": {
    "EUR_USD": {
      "max_amount": 10000,
      "currency_to_spend": "USD",
      "min_amount": 5
    },
```
Лимиты на каждую пару сформированны таким образом, что проверяеться сколько тратиться той или иной валюты в рамках обмена.
В текущем примере, можно потратить от 5 до 10000 USD при покупке евро


### Создание обмена
```javascript
POST /api/v1/exchange
```

#### Параметры
```javascript
{
  "currency_to_spend": "string",
  "currency_to_get": "string",
  "currency_to_spend_amount": "string",
  "callback_url": "string",
  "currency_to_get_amount": "string",
  "exchange_price": "string"
}
```

#### Правила, по созданию обмена
1) Нужно указать валюту, которая тратиться и валюта которая покупаеться
2) Нужно указать одну из сумм, или сделать обмен потратитв "X" валюты, или купить, чтобы получить "Y" валюты
3) Если есть желание купить по заказанной цене нужно указать значение параметра - "exchange_price"
4) Можно указать callback_url, чтобы подписаться на нотификации по изменению статуса обмена

#### Примеры

1) Покупка 1 BTC за UAH по рынку
```javascript
{
  "currency_to_spend": "UAH",
  "currency_to_get": "BTC",
  "currency_to_get_amount": "1"
}
```

2) Покупка BTC за UAH по рынку потратив на обмен 1000 UAH
```javascript
{
  "currency_to_spend": "UAH",
  "currency_to_get": "BTC",
  "currency_to_spend_amount": "10000"
}
```

3) Покупка 1 BTC за UAH по цене 200000
```javascript
{
  "currency_to_spend": "UAH",
  "currency_to_get": "BTC",
  "currency_to_get_amount": "1",
  "exchange_price": "200000"
}
```
### Отмена лимитного обмена
```javascript
POST api/v1/exchange/cancel
```

#### Параметры
```javascript
{
  "order_id": "string"
}
```
Отмениться может только заявка на лимитный обмен, если отмена включена и заявка находиться в процессе выполнения

### Повтор лимитного обмена

```javascript
POST /api/v1/exchange/repeat
```
#### Параметры
```javascript
{
  "order_id": "string"
}
```
Повтор заявки возможен, если повторение включено, и заявка завершена

### Получение деталей по обменной заявке
```javascript
{
      "details": {
        "currency_to_spend_amount": 92.42144177,
        "currency_to_get_amount": 2499.99999988,
        "price": 27.05
      },
      "order_sub_type": "MARKET_EXCHANGE",
      "dt": "2020-04-10 11:19:40.596357",
      "status": "CLOSED",
      "external_id": "d0a9823a-90e4-40af-9739-a380bdc13932",
      "order_type": "EXCHANGE",
      "currency": "UAH_USD"
    },
```

### Детали заявки по обмену при callback нотификации

```javascript
{"external_id": "ddd08d0a-198f-441e-bf45-a61fc889261f", 
"status": "CLOSED", 
"order_type": "EXCHANGE", 
"order_sub_type": "MARKET_EXCHANGE", 
"dt": "2020-04-09 14:05:19.373028", 
"currency": 
"RUB_USDT", 
"details": {"currency_to_get_amount": 40337.397594, 
            "price": 75.28443, 
	    "currency_to_spend_amount": 535.8}
	    }
}
```
