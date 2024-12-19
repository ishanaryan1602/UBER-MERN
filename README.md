# User Registration Endpoint

## POST /users/register

This endpoint is used to register a new user.

### Request Body

The request body must be a JSON object containing the following fields:

- `fullname`: An object containing:
  - `firstname` (string, required): The first name of the user. Must be at least 3 characters long.
  - `lastname` (string, optional): The last name of the user. Must be at least 3 characters long.
- `email` (string, required): The email address of the user. Must be a valid email format and at least 5 characters long.
- `password` (string, required): The password for the user account. Must be at least 6 characters long.

### Example Request

```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "password123"
}
```

### Responses

- **201 Created**
  - **Description**: User successfully registered.
  - **Body**: A JSON object containing the authentication token and user details.
  - **Example**:
    ```json
    {
      "token": "your_jwt_token",
      "user": {
        "_id": "user_id",
        "fullname": {
          "firstname": "John",
          "lastname": "Doe"
        },
        "email": "john.doe@example.com"
      }
    }
    ```

- **400 Bad Request**
  - **Description**: Validation error or missing required fields.
  - **Body**: A JSON object containing the validation errors.
  - **Example**:
    ```json
    {
      "errors": [
        {
          "msg": "Invalid Email",
          "param": "email",
          "location": "body"
        },
        {
          "msg": "First name must be at least 3 characters long",
          "param": "fullname.firstname",
          "location": "body"
        },
        {
          "msg": "Password must be at least 6 characters long",
          "param": "password",
          "location": "body"
        }
      ]
    }
    ```

### Notes

- Ensure that the `Content-Type` header is set to `application/json` when making requests to this endpoint.

# User Login Endpoint

## POST /users/login

This endpoint is used to log in an existing user.

### Request Body

The request body must be a JSON object containing the following fields:

- `email` (string, required): The email address of the user. Must be a valid email format.
- `password` (string, required): The password for the user account. Must be at least 6 characters long.

### Example Request

```json
{
  "email": "john.doe@example.com",
  "password": "password123"
}
```

### Responses

- **200 OK**
  - **Description**: User successfully logged in.
  - **Body**: A JSON object containing the authentication token and user details.
  - **Example**:
    ```json
    {
      "token": "your_jwt_token",
      "user": {
        "_id": "user_id",
        "fullname": {
          "firstname": "John",
          "lastname": "Doe"
        },
        "email": "john.doe@example.com"
      }
    }
    ```

- **400 Bad Request**
  - **Description**: Validation error or missing required fields.
  - **Body**: A JSON object containing the validation errors.
  - **Example**:
    ```json
    {
      "errors": [
        {
          "msg": "Invalid Email",
          "param": "email",
          "location": "body"
        },
        {
          "msg": "Password must be at least 6 characters long",
          "param": "password",
          "location": "body"
        }
      ]
    }
    ```

- **401 Unauthorized**
  - **Description**: Invalid email or password.
  - **Body**: A JSON object containing an error message.
  - **Example**:
    ```json
    {
      "message": "Invalid email or password"
    }
    ```

### Notes

- Ensure that the `Content-Type` header is set to `application/json` when making requests to this endpoint.

# User Profile Endpoint

## GET /users/profile

This endpoint is used to get the profile of the authenticated user.

### Request Headers

- `Authorization` (string, required): The JWT token of the authenticated user.

### Example Request

```http
GET /users/profile HTTP/1.1
Host: example.com
Authorization: Bearer your_jwt_token
```

### Responses

- **200 OK**
  - **Description**: User profile retrieved successfully.
  - **Body**: A JSON object containing the user details.
  - **Example**:
    ```json
    {
      "_id": "user_id",
      "fullname": {
        "firstname": "John",
        "lastname": "Doe"
      },
      "email": "john.doe@example.com"
    }
    ```

- **401 Unauthorized**
  - **Description**: Invalid or missing token.
  - **Body**: A JSON object containing an error message.
  - **Example**:
    ```json
    {
      "message": "Unauthorized"
    }
    ```

### Notes

- Ensure that the `Authorization` header is set to `Bearer your_jwt_token` when making requests to this endpoint.

# User Logout Endpoint

## GET /users/logout

This endpoint is used to log out the authenticated user.

### Request Headers

- `Authorization` (string, required): The JWT token of the authenticated user.

### Example Request

```http
GET /users/logout HTTP/1.1
Host: example.com
Authorization: Bearer your_jwt_token
```

### Responses

- **200 OK**
  - **Description**: User successfully logged out.
  - **Body**: A JSON object containing a success message.
  - **Example**:
    ```json
    {
      "message": "Logged out successfully"
    }
    ```

- **401 Unauthorized**
  - **Description**: Invalid or missing token.
  - **Body**: A JSON object containing an error message.
  - **Example**:
    ```json
    {
      "message": "Unauthorized"
    }
    ```

### Notes

- Ensure that the `Authorization` header is set to `Bearer your_jwt_token` when making requests to this endpoint.