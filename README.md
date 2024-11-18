# Vehicle Registration API Documentation

Welcome to the **Vehicle Registration API** documentation! This project demonstrates how to use the **Swagger Editor** to create, document, and mock an API. The API is hosted on [mockapi.io](https://mockapi.io) and is used for learning and experimentation purposes.

This guide will walk you through the structure of the API, its functionality, and how to interact with it. Even if you're a beginner, you'll find this tutorial helpful for understanding how APIs are built and documented.

---

## What is Swagger?

Swagger is an open-source toolset for designing, building, and documenting APIs. It uses the **OpenAPI Specification** (OAS) to define the structure and behavior of an API in a YAML or JSON format. Swagger provides tools like:
- **Swagger Editor**: Create and document APIs.
- **Swagger UI**: Visualize and test APIs interactively.
- **Mock Server**: Simulate API responses for testing without a backend.

---

## Using Swagger Editor in Browser

You can access the Swagger Editor directly in your browser by visiting this [link](https://editor.swagger.io/).

---

## Using Swagger Editor in Docker

### Running the Image from DockerHub

A pre-built Docker image for Swagger Editor is available on [DockerHub](https://hub.docker.com/r/swaggerapi/swagger-editor/).

To set it up, run the following commands:
```bash
docker pull swaggerapi/swagger-editor
docker run -d -p 80:8080 swaggerapi/swagger-editor
```

This will start the Swagger Editor in **detached mode** on port `80` of your machine. You can open the editor by navigating to [http://localhost](http://localhost) in your web browser.

---

## Getting Started

### Prerequisites
To follow this tutorial, you'll need:
- [Swagger Editor](https://editor.swagger.io/) (web-based or locally installed).
- Basic knowledge of YAML syntax.

### Opening the API in Swagger Editor
1. Open [Swagger Editor](https://editor.swagger.io/).
2. Copy the provided YAML code into the editor.
3. Explore the automatically generated documentation and interactive interface.

---

## API Overview

### Purpose
This API is designed to manage vehicle data, including:
- Registering vehicles.
- Viewing all vehicles.
- Searching for vehicles by ID.
- Updating vehicle information.
- Deleting vehicles.

### Base URL
The API is hosted on a mock server:
```
https://67391350a3a36b5a62ede4e1.mockapi.io/
```

---

## YAML Code Explanation

The **YAML file** defines the structure, endpoints, and behavior of the API. Below is an explanation of its key sections:

### 1. **API Metadata**
```yaml
info:
  title: Vehicle Registration API
  description: This API allows users to manage vehicle data.
  version: 1.0.0
  termsOfService: https://www.example.com/terms
  contact:
    name: API Support Team
    email: support@example.com
  license:
    name: GPL-3.0
    url: https://www.gnu.org/licenses/gpl-3.0.html
```
- **title**: The name of the API.
- **description**: Brief explanation of the API's functionality.
- **version**: API version number.
- **contact**: Support contact information.
- **license**: Licensing details for the API.

---

### 2. **Base URL**
```yaml
servers:
  - url: https://67391350a3a36b5a62ede4e1.mockapi.io/
    description: Mock Server for Testing
```
- Defines the mock server where the API is hosted.

---

### 3. **Tags**
```yaml
tags:
  - name: Vehicles
    description: Endpoints related to vehicle management.
```
- Groups related endpoints for better organization.

---

### 4. **Paths (Endpoints)**
Each path represents an endpoint in the API. Below is an example:

#### `/vehicles` Endpoint
```yaml
paths:
  /vehicles:
    get:
      summary: Retrieve all registered vehicles
      tags:
        - Vehicles
      responses:
        200:
          description: List of vehicles retrieved successfully.
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Vehicles"
```
- **GET**: Retrieves all vehicles.
- **tags**: Categorizes the endpoint under `Vehicles`.
- **responses**: Specifies the response format and schema.

#### `/vehicles/{id}` Endpoint
```yaml
  /vehicles/{id}:
    get:
      summary: Retrieve a vehicle by ID
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: integer
          description: ID of the vehicle to retrieve.
      responses:
        200:
          description: Vehicle retrieved successfully.
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Vehicle"
```
- **Path Parameter (`id`)**: Used to fetch a specific vehicle.
- **200 Response**: Returns the vehicle data.

---

### 5. **Components (Schemas)**
Schemas define the structure of data used in requests and responses.

#### Vehicle Schema
```yaml
components:
  schemas:
    Vehicle:
      type: object
      properties:
        id:
          type: integer
          example: 1
        manufacturers:
          type: string
          example: "Toyota"
        model:
          type: string
          example: "Corolla"
        engine:
          type: string
          example: "2.0L"
        power:
          type: string
          example: "150hp"
        category:
          type: string
          example: "Sedan"
        year:
          type: string
          example: "2023"
```
- **Properties**: Define the fields in the vehicle data.
- **Example**: Shows sample values for each field.

---

### 6. **Authentication**
```yaml
components:
  securitySchemes:
    auth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```
- Implements **Bearer Token Authentication** using JSON Web Tokens (JWT).

---

## Interacting with the API

1. **Retrieve All Vehicles**  
   Send a `GET` request to `/vehicles` to get a list of all vehicles.

2. **Register a New Vehicle**  
   Send a `POST` request to `/vehicles` with the following JSON body:
   ```json
   {
     "manufacturers": "Honda",
     "model": "Civic",
     "engine": "1.8L",
     "power": "140hp",
     "category": "Sedan",
     "year": "2022"
   }
   ```

3. **Retrieve a Vehicle by ID**  
   Send a `GET` request to `/vehicles/{id}`, replacing `{id}` with the vehicle ID.

4. **Update a Vehicle**  
   Send a `PUT` request to `/vehicles/{id}` with the updated vehicle details.

5. **Delete a Vehicle**  
   Send a `DELETE` request to `/vehicles/{id}`.

---

## Learn More

- [Swagger Documentation](https://swagger.io/docs/)
- [MockAPI.io](https://mockapi.io)
