---
title: Error definition
description: How to add interactive quizzes to your site.
---

# Errors
The Hotel API uses conventional HTTP response codes to represent the success or failure of an API request. In general, codes in the `2xx` range indicate success. Codes in the `4xx` range indicate an error that failed to complete the request. Codes in the `5xx` range indicate an error with Hotels' servers.

<br>

| HTTP Status Code | Description | Notes |
|:--------|:-------|:-------|
|  400  | Bad Request   | The request was unacceptable due to missing a required parameter.  |
|=====
| 401   | Unauthorized  | No valid API key. |
|=======
| 403 |  Forbidden | The API key is not allowed to perform request. |
|=====
| 500, 502, 503 | Server Errors | Something went wrong on server. |
|======
{: rules="groups"}
