# 🚛 Drayage

Our **Drayage** quoting API allows you to obtain pricing for container transport between ports or ramps and customer warehouses. This service supports both **import** and **export** operations.

---

## 🔗 Endpoint

To obtain a drayage quote, use the following endpoint:

- **UAT**  
  ```
  https://connect.primofabric.com/v1/drayage/quote
  ```

- **Production**  
  ```
  https://connect.heyprimo.com/v1/drayage/quote
  ```

---

## 🔐 Authentication

All requests must be authenticated and authorized using a **Bearer token** obtained from the following endpoint:

```
/v1/auth/login
```

Additionally, your client must be assigned the necessary **scopes**, which will be provided by our support team.

---

## 📥 Required Fields

When sending a request to the drayage quote endpoint, include the following JSON payload:

```json
{
  "customerReference": 900359,
  "operationType": "Import",
  "market": {
    "country": "US",
    "state": "CA",
    "city": "Long Beach",
    "postalCode": "90802",
    "name": "Long Beach, CA"
  },
  "warehouse": {
    "country": "US",
    "state": "CA",
    "city": "ANAHEIM",
    "postalCode": "92806"
  },
  "container": {
    "container": "Container",
    "containerLenght": 20,
    "commodityName": "TLT",
    "weight": 37000,
    "isHazmat": false,
    "isReefer": false,
    "inGauge": true
  }
}
```

### 📌 Field Descriptions

- **`customerReference`**: Identifies the specific branch or office of a client.
- **`operationType`**: Indicates the type of operation. Supported values are:
  - `10`: Import
  - `20`: Export
- **`market`**: Port or ramp location for drayage service.
- **`warehouse`**: Destination or origin warehouse location.
- **`container.containerLenght`**: Length of the container in feet.
- **`commodityName`**: Name of the commodity being transported.
- **`weight`**: Total weight of the container in pounds.
- **`isReefer`** ❄️: Indicates whether the container is refrigerated.
- **`isHazmat`** ☣️: Specifies if the container includes hazardous materials.
- **`inGauge`** 📏: Refers to whether the container dimensions fall within standard gauge limits.

---

## ⚓ Ports and Ramps

To specify the **Port/Ramp** for the drayage service, you must provide a `market`. To obtain a list of available markets, use the following endpoint:

```
GET /v1/drayage/markets
```

---

## 📦 Container Types

You must also specify the container type. Valid container types can be retrieved using the following endpoint:

```
GET /v1/drayage/container-types
```
