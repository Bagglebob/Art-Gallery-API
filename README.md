# User API

A Node.js Express API for user management with JWT authentication, favorites, and history tracking.

## Features

- User registration and login with bcrypt password hashing
- JWT-based authentication using Passport.js
- User favorites management (up to 50 items)
- User history tracking (up to 50 items)
- CORS support

## Installation

1. Clone or download the project
2. Install dependencies:
`ash
npm install
`

## Configuration

Create a .env file in the project root with the following variables:

`
PORT=8080
MONGO_URL=mongodb://your_mongodb_connection_string
`

- PORT: Server port (default: 8080)
- MONGO_URL: MongoDB connection string (required)

## API Endpoints

### Authentication

#### Register User
- **POST** /api/user/register
- Body: { userName, password, password2 }

#### Login
- **POST** /api/user/login
- Body: { userName, password }
- Returns: JWT token

### Favorites (Requires JWT Token)

#### Get Favorites
- **GET** /api/user/favourites
- Header: Authorization: jwt <token>

#### Add Favorite
- **PUT** /api/user/favourites/:id
- Header: Authorization: jwt <token>
- Max: 50 items

#### Remove Favorite
- **DELETE** /api/user/favourites/:id
- Header: Authorization: jwt <token>

### History (Requires JWT Token)

#### Get History
- **GET** /api/user/history
- Header: Authorization: jwt <token>

#### Add History
- **PUT** /api/user/history/:id
- Header: Authorization: jwt <token>
- Max: 50 items

#### Remove History
- **DELETE** /api/user/history/:id
- Header: Authorization: jwt <token>

## User Schema

`javascript
{
  userName: String (unique),
  password: String (bcrypt hashed),
  favourites: [String],
  history: [String]
}
`

## Starting the Server

`ash
npm start
`

The API will listen on the configured PORT (default: 8080).

## Dependencies

- **express**: Web framework
- **mongoose**: MongoDB ODM
- **bcryptjs**: Password hashing
- **jsonwebtoken**: JWT token generation
- **passport**: Authentication middleware
- **passport-jwt**: JWT strategy for Passport
- **cors**: Cross-Origin Resource Sharing
- **dotenv**: Environment variable management

## Error Handling

- 422 Unprocessable Entity: Invalid input or operation failed
- Authentication errors return 401 with error message
- User not found returns 422 with error message
