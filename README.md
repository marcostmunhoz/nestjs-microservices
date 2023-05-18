# NestJS Microservices POC

## Installation
After cloning the repository, run `cp .env.example .env` and `docker compose up`.

## Usage

The application exposes the following endpoints:
- `POST /accounts` with body `{"name": "SOME ACCOUNT NAME", "email": "SOME_ACCOUNT_EMAIL"}`: creates a new account
- `POST /auth/login` with body `{"email": "CREATED_ACCOUNT_EMAIL", "password": "GENERATED_PASSWORD"}`: returns an account auth token. The password is generated randomly after registering an account and printed in the auth service logs (`docker compose logs auth`).
- `GET /accounts` with header `Authorization: Bearer ACCOUNT_AUTH_TOKEN`: show the authenticated account data
- `PUT /accounts` with header `Authorization: Bearer ACCOUNT_AUTH_TOKEN` and body `{"name": "SOME ACCOUNT NAME", "email": SOME_ACCOUNT_EMAIL"}`: updates the authenticated account data. In case the email is changed, it's propagated to the auth service, meaning that the following auth requests should be made with the new email.
- `GET /simulate-account-creation`, at port 8080, simulates an account being created via the PHP application