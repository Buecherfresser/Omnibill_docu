# **GET** Webpage Request
To request a user's data in the end user portal please use:
```
https://europe-west3-omnibill-twl.cloudfunctions.net/webpageRequest
```
## Header parameters

### Year *(required)* 
#### Definition
*The year for which the user data is requested. Currently only one year at a time possible.*
#### Valid arguments
YYYY (int)

### Start-Month: *(required)*
#### Definition
*Data from this month on will be returned. (Inclusive)*
#### Valid arguments
MM (int)

### End-Month: *(required)*
#### Definition
*Data up to this month will be returned. (Inclusive)*
#### Valid arguments
MM (int)

### Interval: *(required)*
#### Definition
*The year for which the user data is requested. Currently only one year at a time possible.*
#### Valid arguments
"hourly" / "monthly" (String)
*For more information see Return.*

## Authentication
### Authorization: Bearer *token*
The token can be requested in generateToken.

## Return
Depending on the argument for Interval the return format is different.
### Monthly
Returns every month in the specified time range.
#### Example
```Code
{
    "result": {
        "2023-04": {
            "totalConsumption": 721.9999999999997,
            "totalCost": 68.033112378113
        },
        "2023-05": {
            "totalConsumption": 734.0000000000003,
            "totalCost": 69.23637012248663
        }
    }
}
```
### Hourly
Returns an array with each object being the data of an hour in the specified time range.
#### Example
```Code
{
    "result": {
        "CustomerData": [
            {
                "PowerConsumptionID": "295302",
                "CustomerConsumptionID": "929557",
                "HeatConsumptionID": "706099"
            }
        ],
        "CustomerConsumptionData": [
            {
                "customerTotal_Eur": 0.06021592442645073,
                "LossFactor": 0.91,
                "cop": 2.9381443298969074,
                "customerHeatCost": 0.08602274918064391,
                "customerTotal_ct": 6.0215924426450735,
                "PriceFactor": 0.23,
                "heatPumpHeatCost": 0.07828070175438596,
                "consumption": "0.70",
                "timeKey": "2023-04-01",
                "endTimestamp": 1680310800000,
                "startTimestamp": 1680307200000
            },
            {
                "customerTotal_Eur": 0.13081298093007696,
                "LossFactor": 0.91,
                "cop": 2.511764705882353,
                "customerHeatCost": 0.10062536994621304,
                "customerTotal_ct": 13.081298093007696,
                "PriceFactor": 0.23,
                "heatPumpHeatCost": 0.09156908665105387,
                "consumption": "1.30",
                "timeKey": "2023-04-01",
                "endTimestamp": 1680314400000,
                "startTimestamp": 1680310800000
            },
			...
			{
                "customerTotal_Eur": 0.059194823867721055,
                "LossFactor": 0.91,
                "cop": 2.9888268156424584,
                "customerHeatCost": 0.08456403409674437,
                "customerTotal_ct": 5.919482386772105,
                "PriceFactor": 0.23,
                "heatPumpHeatCost": 0.07695327102803738,
                "consumption": "0.70",
                "timeKey": "2023-05-01",
                "endTimestamp": 1682899200000,
                "startTimestamp": 1682895600000
            }
        ]
    }
}
```

*This function might change later on.*