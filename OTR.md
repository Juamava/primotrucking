# 🚚 Over the road

**Over the Road** refers to freight transportation by road, and it is classified into two main categories:
- **FTL (Full Truckload)**: Full load in a single truck.
- **LTL (Less than Truckload)**: Partial load, where the truck transports goods from different customers.

Our OTR service allows you to get rates and make bookings for both transportation modes.

---

## Getting Rates 📊

To obtain transportation rates, you must send a `POST` request to the `/v1/otr/quote` endpoint. This endpoint is available in both our sandbox and production environments:

- 🧪 **Sandbox**: `https://connect.primofabric.com/v1/otr/quote`
- 🚀 **Production**: `https://connect.heyprimo.com/v1/otr/quote`

The request should include detailed information about the origin, destination, and items to be transported. Based on this data, our system returns quotes from different carriers and service modes, including FTL and LTL.

### Request: The API request

```json
{
    "customerReference": 1237100106,
    "customerName": "Transborder SA",
    "requestingUser": "juan.vallejo@heyprimo.com",
    "origin": {
        "name": "Warehouse A",
        "address1": "123 Main Street",
        "address2": "Suite 100",
        "city": "Los Angeles",
        "state": "CA",
        "postalCode": "90001",
        "country": "US",
        "bsnNumber": null
    },
    "destination": {
        "name": "Customer B",
        "address1": "456 Market Street",
        "address2": "",
        "city": "San Francisco",
        "state": "CA",
        "postalCode": "94103",
        "country": "US",
        "bsnNumber": null
    },
    "items": [
        {
            "itemName": "Pallet of Electronics",
            "packageType": "Pallet",
            "quantity": 2,
            "length": 48.0,
            "width": 40.0,
            "height": 60.0,
            "weight": 30,
            "commodityClass": "65",
            "unOrTechnicalName": null,
            "numberOfPieces": 1,
            "levels": 1,
            "isHazardous": false,
            "isStackable": false
        }
    ],
    "selectedAccessorials": [],
    "modes": [
        10
    ],
    "equipment": null,
    "equipmentLength": null,
    "service": "Standard",
    "targetRate": 103
}
```

### Response: The API response

```json
{
    "data": {
        "quoteNumber": 8895707,
        "mileage": 390.09066190180236171535114978,
        "referenceQuoteNumber": "13938883",
        "carrierQuotes": [
            {
                "rateNumber": 1525,
                "carrierNumber": 58624,
                "carrierName": "AAA Cooper",
                "laneName": "AAA COOPER TRANSPORTATION ",
                "carrierLogoUrl": "https://lfsratestoragedev.blob.core.windows.net/carrierlogoscontainer/aaa-cooper.png?sv=2021-04-10&st=2022-09-07T01%3A38%3A45Z&se=2099-09-08T01%3A38%3A00Z&sr=c&sp=r&sig=A%2BvrUChlCBil9j2h0EmN5AAnpgPetwmwol%2BWwl8%2BD94%3D",
                "carrierScac": "AACT",
                "carrierRemarks": [
                    "<span style="font-size:11.0pt;font-family:&quot;Calibri&quot;,&quot;sans-serif&quot;;
mso-fareast-font-family:Calibri;mso-fareast-theme-font:minor-latin;mso-bidi-font-family:
&quot;Times New Roman&quot;;mso-ansi-language:ES-CO;mso-fareast-language:ES-CO;
mso-bidi-language:AR-SA">TSA CARRIER</span>"
                ],
                "transitDays": 1,
                "mode": "LTL",
                "service": "Standard",
                "accessorials": [],
                "serviceDescription": "Less than Truckload",
                "totalAmount": 398.17,
                "quoteExpirationDate": "2025-05-10T22:35:42.1005425+00:00",
                "equipment": null,
                "equipmentLength": null,
                "charges": [
                    {
                        "displayName": "Base",
                        "chargeCode": 1000,
                        "chargeNumber": null,
                        "chargePoint": null,
                        "amount": 398.17,
                        "isWaived": false
                    }
                ]
            }
        ]
    },
    "errors": null
}
```
---

## Metadata 🛠️

Metadata in the OTR API includes the keys necessary to work with the system, such as:

- **equipments**: Available types of equipment for transportation.
- **accessorials**: Additional services like handling or insurance.
- **service**: The service level for transportation, such as "Standard", "Expedited", etc.

These keys allow customization of requests according to customer needs and transportation requirements.
