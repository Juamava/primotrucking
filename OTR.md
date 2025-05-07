# OTR API Documentation 📦🚚

## Contexto a nivel de negocio: ¿Qué es OTR? 🌎

OTR (Over the Road) se refiere al transporte de carga por carretera, y se clasifica en dos categorías principales:
- **FTL (Full Truckload)**: Carga completa en un solo camión.
- **LTL (Less than Truckload)**: Carga parcial, donde el camión transporta mercancías de diferentes clientes.

Nuestro servicio de OTR permite obtener tarifas y realizar bookings para ambos modos de transporte.

---

## Obtención de tarifas 📊

Para obtener las tarifas para un trayecto OTR, puedes hacer uso del siguiente endpoint:

### Ruta: `{{lfs-connect-api}}/v1/otr/quote`

### ¿Cómo funciona la obtención de tarifas?

El endpoint recibe una solicitud que incluye información detallada sobre el origen, destino, y los artículos a transportar. A partir de esta información, se calcula el costo total del transporte para diferentes transportistas y modos de servicio.

### Endpoint para obtener tarifas

`POST {{lfs-connect-api}}/v1/otr/quote`

### Request: La solicitud a la API

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

### Response: La respuesta de la API

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

## Creación de un embarque 🚢

Para la creación de un embarque, debes enviar la solicitud con la información relevante sobre el cliente, el origen, el destino, los artículos, y las tarifas seleccionadas.

### Endpoint para crear un embarque

`POST {{lfs-connect-api}}/v1/otr/shipment`

### Request

```json
{
    "customerReference": 1237100106,
    "shipmentDetails": {
        "origin": {
            "name": "Warehouse A",
            "address1": "123 Main Street",
            "city": "Los Angeles",
            "state": "CA",
            "postalCode": "90001",
            "country": "US"
        },
        "destination": {
            "name": "Customer B",
            "address1": "456 Market Street",
            "city": "San Francisco",
            "state": "CA",
            "postalCode": "94103",
            "country": "US"
        },
        "items": [
            {
                "itemName": "Pallet of Electronics",
                "quantity": 2,
                "weight": 30
            }
        ],
        "service": "Standard"
    }
}
```

### Response

```json
{
    "data": {
        "shipmentNumber": "SH123456",
        "status": "Created",
        "trackingUrl": "https://tracking.url/SH123456"
    },
    "errors": null
}
```

---

## Metadata 🛠️

La metadata en la API de OTR incluye claves necesarias para trabajar con el sistema, tales como:

- **equipments**: Tipos de equipo disponibles para el transporte.
- **accessorials**: Servicios adicionales, como la manipulación o el seguro.
- **service**: El nivel de servicio de transporte, como "Standard", "Expedited", etc.

Estas claves permiten personalizar las solicitudes según las necesidades del cliente y los requerimientos de transporte.

---

Gracias por usar nuestra API! 🚚
