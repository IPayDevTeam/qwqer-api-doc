## Authorization

### POST: `/api/xr/mch/login`

Login to the system, this command return valid **restid** and additional info about the user.
<br>
The **restid** is need to call authorized endpoints.

**Request:**

```json
{
  "login": string, // Required field
  "passw": string // Required field
}
```

**Response:**

```json
{
  "data": {
    ...
    "restid": string,
    ...
  },
  "rmsg":"SUCCESS",
  "rstate": 0 // `0` if successfull request.
}
```


<br><br>


## Check delivery price

### POST: `/api/xr/mch/delivery_price`

Calculate price for delivery orded without creating it in the system.

**Headers:**

```json
{
  "Authorization": "Bearer {restid}"
}
```

**Request:**

```json
{
  // Sender info
  "sender": {
    "name": string,
    "phone": string,
    "contact": string, // This field must be the same as `phone` field.
    "email": string,
    "company" string,
    "country": string,
    "countrycode2": string, // Required field, country code ISO-2.
    "zipcode": string,
    "state": string,
    "statecode": string,
    "city": string,
    "citycode2": string,
    "region": string,
    "regioncode2": string,
    "address": string, // Required field, full address line.
    "address1": string,
    "address2": string,
    "addressinfo": string
  },
  // Receiver info
  "receiver": {
    "name": string,
    "phone": string,
    "contact": string, // This field must be the same as `phone` field.
    "email": string,
    "company" string,
    "country": string,
    "countrycode2": string, // Required field, country code ISO-2.
    "zipcode": string,
    "state": string,
    "statecode": string,
    "city": string,
    "citycode2": string,
    "region": string,
    "regioncode2": string,
    "address": string, // Required field, full address line.
    "address1": string,
    "address2": string,
    "addressinfo": string
  },
  // Order parcel info
  "ordersize": {
    "length": numeric,
    "width": numeric,
    "height": numeric,
    "weight": numeric, // Required field.
    "lenunit": string, // MILLIMETER, CENTIMETER, DECIMETER, METER, INCH, FEET, YARD.
    "weightunit": string // GRAM, KILOGRAM, POUND, TONE, OUNCE.
  }
}
```

**Response:**

```json
{
  "data": {
    "distance": numeric,
    "distanceprice": numeric,
    "price": numeric,
    "discount": numeric,
    ...
  },
  "rmsg":"SUCCESS",
  "rstate": 0 // `0` if successfull request.
}
```


<br><br>


## Create delivery order

### POST: `/api/xr/mch/delivery`

Create delivery order in the system.

Before calling this endpoint it's necessary to request [delivery price checking](api-endpoints?id=check-delivery-price), and place some values from response to this endpoints request

**Headers:**

```json
{
  "Authorization": "Bearer {restid}"
}
```

**Request:**

```json
{
  "distance": numeric, // `distance` value from `delivery_price` response.
  "dunit": string, // METER, KILOMETER, MILE.
  "dkind": "NONE",
  "country": string, // Sender country code ISO-2.
  "duration": numeric, // `duration` value from `delivery_price` response.
  "summa": numeric, // Calculate from the `delivery_price` response fields, `price - discount = summa`.
  "sender": object, // `sender` value from `delivery_price` response.
  "receiver": object, // `receiver` value from `delivery_price` response.
  "ordersize": object, // `ordersize` value from `delivery_price` response.
  "status": 1,
}
```

**Response:**

```json
{
  "data": {
    "id": numeric,
    "status": numeric, // Here will be `1` as `new`.
    ...
  },
  "rmsg":"SUCCESS",
  "rstate": 0 // `0` if successfull request.
}
```


<br><br>


## Delivery order payment

### POST: `/api/xr/mch/delivery_payment`

Make payment for created delivery order.

**Headers:**

```json
{
  "Authorization": "Bearer {restid}"
}
```

**Request:**

```json
{
  "id": numeric
}
```

**Response:**

```json
{
  ...
  "rmsg":"SUCCESS",
  "rstate": 0 // `0` if successfull request.
}
```


<br><br>


#### For all technical questions please contact our specialist at:
- **Email:** [andrejs.konakovs@gmail.com](mailto:andrejs.konakovs@gmail.com)
- **Phone:** [+371 29-779-888](tel:+37129779888)


<br><br>


## PDF with order info

### GET: `/api/xr/mch/delivery-pdf/{OrderID}`

Get *url* string of **PDF** file with order info

**Response:**

```json
{
  "rstate": 0,
  "rmsg": "ok",
  "data": {
    "pdf_url": "https://qwqer.eu/files/pdfreport/mr/order/xxxxx-xxxxxxxxxxxxx.pdf"
  }
}
```
