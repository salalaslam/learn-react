# Communication with Backend Protocol

## Naming Conventions

- Always use camelCase for database columns and avoid snake_case at all costs.

  - Example:

  ```sql
  -- Good
  SELECT firstName, lastName FROM users;

  -- Bad
  SELECT first_name, last_name FROM users;
  ```

## API Design

- Use RESTful principles for designing APIs.
- Use meaningful and consistent naming for endpoints.
  - Example:
  ```plaintext
  GET /users
  POST /users
  GET /users/{id}
  PUT /users/{id}
  DELETE /users/{id}
  ```

## Data Formats

- Always use JSON for data exchange between frontend and backend.
- Ensure consistent data formats for dates, numbers, and other data types.

## Error Handling

- Use standard HTTP status codes to indicate the result of an API request.
  - Example:
  ```plaintext
  200 OK
  201 Created
  400 Bad Request
  401 Unauthorized
  404 Not Found
  500 Internal Server Error
  ```
- Provide meaningful error messages in the response body.

## Authentication and Authorization

- Use JWT (JSON Web Tokens) for authentication.
- Ensure all sensitive endpoints are protected and require proper authorization.

## Versioning

- Use versioning for APIs to ensure backward compatibility.
  - Example:
  ```plaintext
  /api/v1/users
  ```

## Documentation

- Maintain up-to-date API documentation using tools like Swagger or Postman.
- Include examples for each endpoint, detailing request and response formats.

## Performance

- Optimize database queries to reduce response times.
- Use caching mechanisms where appropriate to improve performance.

## Security

- Validate and sanitize all inputs to prevent SQL injection and other attacks.
- Use HTTPS to encrypt data in transit.
- Implement rate limiting to prevent abuse of APIs.

## Testing

- Write unit and integration tests for all API endpoints.
- Use automated testing tools to ensure the reliability of the backend.

---

_Disclaimer: This document is prepared for the backend team of Invotyx. These conventions might not be relevant for all._
