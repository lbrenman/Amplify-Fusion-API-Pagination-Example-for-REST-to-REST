# Amplify Fusion - Pagination Example

An Amplify Fusion API Pagination example that demonstrates how to map front end `page/size` query parameter request pagination to a back end API `offset/limit` query parameter request pagination with `totalItems` and `totalPages` response mapping from the back end `total` response.

The front end Open API specification file, [employee-facade-openapi.yaml](employee-facade-openapi.yaml) is in this repo and includes info on the pagination and data mapping implemented in the project.

The back end Open API specification file, [DataAPI.json](DataAPI.json), comes from the API described [here](https://github.com/lbrenman/api-test-tool) which you can deploy and run in GitHub Codespace or a hosting service of your choice.

This example also illustrates data mapping using an iMap and Multi-step functions and some API best practices for error handling using Try-catch, If-else and GetErrorObject components.

For reference, an example Amplify Fusion API Pagination where the backend is a Database can be found [here](https://gist.github.com/lbrenman/038864936adb8eacd9e7f4239792910b).

## Getting Started

TO get started, import the Amplify Fusion project export file, [APIPaginationExample.zip](APIPaginationExample.zip) into your Fusion tenant from the Fusion Manager module.

## Details

The front end request looks like this:

```bash
curl --location '{{FRONT_END_BASE_URL}}/employees?page=2&size=10'
```

The front end response looks like this:

```json
{
  "employees": [
    {
      "employeeId": 4,
      .
      .
      .
      "lastModified": "2026-09-30T14:05:12.000Z"
    },
    .
    .
    .
  ],
  "pagination": {
    "page": 2,
    "size": 10,
    "totalItems": 250,
    "totalPages": 25
  }
}
```

The back end request looks like this:

```bash
curl --location '{{BACK_END_BASE_URL}}/employees?offset=20&limit=20'
```

The back end response looks like this:

```json
{
    "data": [
        {
            "id": 21,
            "uuid": "62cb60d0-bf73-4bd8-af08-bd2c862d244d",
            "employeeNumber": "EMP-000021",
            .
            .
            .
        },
        .
        .
        .
    ],
    "meta": {
        "offset": 20,
        "limit": 20,
        "total": 250
    }
}
```