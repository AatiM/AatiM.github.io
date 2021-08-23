---
title: API Reference
tags:
 - jekyll
 - github
description: Sample REST API documentation for a booking platform
---

# Hotel API Reference

## GET hotels

Retrieves the names and IDs of hotels in the specified postal code.
#### URL
`GET` http://api.example.com/hotel
### Query Parameters

| Parameter | Description | Type | Required | Notes |
|:--------|:-------|--------|---------|:--------|
| postalCode  | Postal code for hotels   | string   | Required |
|=======
| type   | the type of hotel   | string   | Optional | Default is all types.
|=====
| offset  | The index to start with   | integer | Optional |
|=====
| limit | The number of results to return | integer | Optional |
|=======
{: rules="groups"}
<br>
### Header

| HeaderName | Description | Required | Values |
|:--------|:-------|--------|:-------|
| Bearer   | The access token  | Required   | See Authorization section. |
|----
| Accept  | The format of the data to be returned   | Optional   | application/json, application/xml. Default is application/json |
|=====
{: rules="groups"}
<br>

### Sample Request
GET http://api.example.cpm/hotel?postalCode=98115&type=2stars

```
Bearer: 235a234e43
Accept: application/json
```

### Response

| Element | Description | Type | Notes |
|:--------|:-------|:--------|:-------|
| postalCode   | The postal code to define a region   | string   |
|----
| type   | The type of hotel   | string  | if type isn't specified, then type is not included in the response. |
|=====
| hotels   | Array of hotel data   |
|=====
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name   | The name of the hotel   | string |
|=====
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; id | The ID of the hotel | integer |
|=====
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url | The URL for the hotel resource | string |
|=======
{: rules="groups"}
<br>
### Sample Response

```json
{
      "postalcode": "98115",
      "type": "2stars",
      "hotels": [
        {
          "name": "HP Hotel",
          "id": 57389,
          "url": "http://api.example.com/hotel/57389"
        },
        {
          "name": "The Shelbourn Hotel",
          "id": 61134,
          "url": "http://api.example.com/hotel/61134"
        }
      ]
  }
  ```
### Status Codes and Errors

The following table lists the returned HTTP status codes.

| Code | Description | Notes |
|:--------|:-------|:--------|
| 200   | OK   | Success  |
|----
| 401   | Unauthorized   | Access token is invalid   |
|=====
| 404   | Not found   | Invalid hotel type |
|=====
{: rules="groups"}
-----------------------------------------------------
## POST guidebook
Uploads a guidebook for a client's account for a hotel website.

#### URL
`POST`  https://api.guidebook.com/account/guide
### Headers

| Header Name | Description | Required | Values |
|:--------|:-------:|--------:|
| Bearer  | Access token   | Required   | See Authorization section |
|----
| Content-Type   | The format of the guidebook to upload   | Optional  | Default is pdf. |
|=====
| Accept   | The format of the returned data  | Optional | application/xml or application/json. Default is application/json. |
|=======
{: rules="groups"}
<br>
### POST Body

| Element | Description | Type | Required |
|:--------|:-------|:--------|:--------|
| accountName   | The name of the account   | string   | Required |
|=======
| guide   | The guide notes in the guidebook   | string   | Required |  
|=====
{: rules="groups"}



### Sample Request
`POST` https://api.guidebook.com/account/5432/post/5434/guide

```
Bearer: {access token}
Content-Type: pdf
Accept: application/json
```

```json
{
  "accounname": "John32",
  "guide": " First go to big tower!"
}
```

### Response


| Element | Description | Type | Notes
|:--------|:-------|:--------|:-------|
| id   | The ID of the new guide book   | integer  |
|----
| length   | The length of the guide book  | float   | Length is in page.
|=====
{: rules="groups"}
<br>

### Sample Response
```json
{
    "id": 3543,
    "length": 19
}
```
### Status Codes and Errors

| Code | Description | Notes |
|:--------|:-------|:--------|
| 200   | OK   | Success  |
|=====
| 401   | Unauthorized   | Access token is invalid   |
|=====
| 404   | Not found   | Post ID is invalid |
|=====
{: rules="groups"}
-----------------------------------------------------
## GET report
Contains information about swimming conditions, including water temperature, wind, and tide. Also provides an overall recommendation about whether to go swimming.

#### Endpoints
`GET` swimmingreport/{beachId}

Retrieves the swimming condition for a specific beach ID for hotels.

## Parameters
### Path Parameters

| Path Parameters | Description |
|:--------|:-------|
| {beachId}   | The value for the beach you want to look up. |
|----
{: rules="groups}
<br>

### Query Parameters

| Parameter | Description | Type | Required |
|:--------|:-------|:--------|
| days   | The number of days to include in the response. Default is 6.   | Integer  | Optional |
|======
| time   | If you include the time, then only the current hour will be returned in the response.   | integer  | Optional |
|=====
{: rules="groups"}
<br>

### Sample Request

```
curl -I -X GET "https://api.weathermap.org/data/2.5/swimmingreport?zip=95050&appid=APIKEY&units=imperial&days=2"
```
(In the above code, replace 'APIKEY' with your actual API key.)
### Sample Response
```json
{
  "swimmingreport": [
      {
          "beach": "Barceloneta",
          "monday": {
              "1pm": {
                  "tide": 5,
                  "wind": 15,
                  "watertemp": 80,
                  "recommendation": "Go swimming!"
              },
              "2pm": {
                  "tide": -1,
                  "wind": 1,
                  "watertemp": 50,
                  "recommendation": "Swimming conditions are okay, not great."
              },
              "3pm": {
                  "tide": -1,
                  "wind": 10,
                  "watertemp": 65,
                  "recommendation": "Not a good day for swimming."
              }
              ...
          }
      }
  ]
}
```
### Response definition

The following table describes each item in the response.

| Response item | Description | Data type |
|:--------|:-------|:--------|
| beach   | The beach you selected based on the beach ID in the request.  | String   |
|----
| {day}   | The day of the week selected. A maximum of 6 days gets returned in the response.   | Object   |
|=====
| {time}   | The time for the conditions. | String |
|=====
| {day}/{time}/tide | The level of tide at the beach for a specific day and time. | integer |
|=====
| {day}/{time}/watertemp | The temperature of the water, returned in Fahrenheit or Celsius depending upon the units you specify. | integer |
|=====
{: rules="groups"}
