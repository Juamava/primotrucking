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

### Response: The API response

```json
{
    "data": {
        "quoteNumber": 8904305,
        "rates": [
            {
                "rateNumber": "1",
                "prenotice": "3-5 days",
                "freight": 935.907284870394320,
                "fuel": 0.00,
                "accessorials": [
                    {
                        "name": "Reefer",
                        "cost": 200,
                        "quantity": 1
                    },
                    {
                        "name": "Hazardous",
                        "cost": 200,
                        "quantity": 1
                    },
                    {
                        "name": "Chassis",
                        "cost": 50,
                        "quantity": 2
                    },
                    {
                        "name": "ChassisSplit",
                        "cost": 90,
                        "quantity": 1
                    }
                ],
                "expectedAccessorialsCosts": 590,
                "expectedTotal": 1525.907284870394320
            },
            {
                "rateNumber": "2",
                "prenotice": "2-3 days",
                "freight": 969.940277047499568,
                "fuel": 0.00,
                "accessorials": [
                    {
                        "name": "Reefer",
                        "cost": 200,
                        "quantity": 1
                    },
                    {
                        "name": "Hazardous",
                        "cost": 200,
                        "quantity": 1
                    },
                    {
                        "name": "Chassis",
                        "cost": 50,
                        "quantity": 2
                    },
                    {
                        "name": "ChassisSplit",
                        "cost": 90,
                        "quantity": 1
                    }
                ],
                "expectedAccessorialsCosts": 590,
                "expectedTotal": 1559.940277047499568
            }
        ],
        "disclaimers": [
            {
                "drayageMarketZipCode": "Rate per Container",
                "disclaimer": "15148"
            },
            {
                "drayageMarketZipCode": "Subject to Equipment Availability",
                "disclaimer": "15148"
            },
            {
                "drayageMarketZipCode": "NS is grounded Ramp",
                "disclaimer": "15148"
            }
        ],
        "remarks": [
            {
                "drayageMarketZipCode": "15148",
                "accessorialNumber": 595,
                "remark": "OW Permit for Excessive Weight: $75 per state"
            },
            {
                "drayageMarketZipCode": "15148",
                "accessorialNumber": 740,
                "remark": "LayOver Fee (May apply and varies due to Distance, HOS, Delays, etc): $300 - $500 (depends on the distance)"
            },
            {
                "drayageMarketZipCode": "15148",
                "accessorialNumber": 735,
                "remark": "Drop&Pick: Double the Rate"
            },
            {
                "drayageMarketZipCode": "15148",
                "accessorialNumber": 630,
                "remark": "Storage: $45 per day"
            },
            {
                "drayageMarketZipCode": "15148",
                "accessorialNumber": 720,
                "remark": "Chassis Split (maximum 2): $90/each"
            },
            {
                "drayageMarketZipCode": "15148",
                "accessorialNumber": 545,
                "remark": "Driver Detention: $100/Additional Hour. 1 Free Hour for Loading/Unloading/Terminal Transaction"
            },
            {
                "drayageMarketZipCode": "15148",
                "accessorialNumber": 710,
                "remark": "Chassis Flip (if required): $110"
            },
            {
                "drayageMarketZipCode": "15148",
                "accessorialNumber": 715,
                "remark": "Pre Pull (if needed): $150"
            }
        ],
        "notes": [
            {
                "drayageMarketZipCode": "15148",
                "note": "Pool Chassis Shortage"
            },
            {
                "drayageMarketZipCode": "15148",
                "note": "We have Private Chassis Available"
            }
        ]
    },
    "errors": null
}
```
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
GET /v1/drayage/equipments
```