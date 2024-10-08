﻿# Weather API Application

## Project Overview

This Node.js application, built using TypeScript, interacts with a weather API to fetch temperature data based on user-provided date and location parameters. It includes a caching mechanism using SQLite, robust error handling, and comprehensive testing.

## Table of Contents

1. [Features](#features)
2. [Getting Started](#getting-started)
   - [Prerequisites](#prerequisites)
   - [Setup](#setup)
   - [Running the Application](#running-the-application)
   - [Running Tests](#running-tests)
   - [Docker Setup](#docker-setup)
3. [API Documentation](#api-documentation)
4. [Error Handling](#error-handling)
5. [Assumptions](#assumptions)
6. [License](#license)

## Features

- **Weather Data Fetching**: Retrieve temperature data based on city and date.
- **Temperature Conversion**: Ensure temperature data is returned in both Celsius and Fahrenheit.
- **Caching**: Use SQLite to cache API responses and reduce the number of API requests.
- **Rate Limiting**: Handle API rate limits with appropriate error responses.
- **Comprehensive Testing**: Includes unit and end-to-end tests.
- **Docker Support**: Containerize the application for consistent environments.

## Getting Started

### Prerequisites

Ensure you have the following installed:
- Node.js (v18+)
- Docker (optional but recommended for containerization)
- SQLite (for caching)

### Setup

1. **Clone the Repository**

   ```bash
   git clone https://github.com/renatosilveira99/weather-flow.git
   cd weather-api-app
   ```

2. **Install Dependencies**

   ```bash
   npm install
   ```

3. **Run Migrations**

   Create the SQLite database and apply migrations:

   ```bash
   npm run migrate:dev
   ```

### Running the Application

#### Development Mode

To run the application in development mode:

1. **Start the Application**

   ```bash
   npm run dev
   ```

   Ensure that you have installed dependencies and run migrations before starting the application.

#### Docker

If you prefer to use Docker for running the application:

1. **Build the Docker Image**

   ```bash
   docker build -t weather-api-app .
   ```

2. **Run the Docker Container**

   ```bash
   docker run -p 3333:3333 weather-api-app
   ```

   The application will be accessible at `http://localhost:3333` inside the Docker container.

## API Documentation

### Endpoint

- **GET** `/weather`

  **Query Parameters:**
  - `city` (string): The city name.
  - `date` (string, ISO 8601 format): The date for which the weather is requested.

  **Response:**
  - Status Code: 200 OK
  - Body: 
    ```json
    {
      "id": "30ad8f4e-5acc-449a-a9cf-9ad8b62e74a5",
      "city": "São Paulo",
      "date": "2024-09-12",
      "temperatureInCelsius": 20.68,
      "temperatureInFahrenheit": 69.22
    }
    ```

  **Error Response:**
  - Status Code: 400 Bad Request
  - Body: 
    ```json
    {
      "error": "Server is a teapot, cannot process the request. :)"
    }
    ```

## Error Handling

The application includes robust error handling for:
- API rate limits
- Random API errors
- Data format inconsistencies

Errors are logged and appropriate responses are sent to the client.

## Assumptions

- The SQLite database is used solely for caching and does not include long-term data storage.
- The API endpoint may vary and return temperatures in different formats; the application handles conversion to ensure consistent output.
- Docker is used for containerization to simplify deployment and ensure consistency across environments.
