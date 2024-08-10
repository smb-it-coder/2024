OAuth 2.0 is a framework for authorization that allows applications to obtain limited access to user resources on a server. The protocol defines several **grant types** for obtaining access tokens. Here's a detailed look at the most common OAuth 2.0 grant types, with a step-by-step example for each.

### 1. **Authorization Code Grant**

This is the most common grant type, used by web applications to obtain an access token. It involves an authorization code that the client exchanges for an access token.

#### Example Steps:

1. **User Requests Access**: The user initiates a request to access a protected resource.
   - **URL**: `https://authorization-server.com/auth`
   - **Parameters**:
     - `response_type=code`
     - `client_id=YOUR_CLIENT_ID`
     - `redirect_uri=YOUR_REDIRECT_URI`
     - `scope=YOUR_SCOPES`
     - `state=RANDOM_STATE_STRING`

2. **User Authenticates**: The user is redirected to the authorization server, where they authenticate and authorize the client application.

3. **Authorization Code Issued**: After successful authorization, the authorization server redirects the user back to the client's `redirect_uri` with an authorization code.
   - **Redirect URL**: `https://yourapp.com/callback?code=AUTH_CODE&state=RANDOM_STATE_STRING`

4. **Client Requests Access Token**: The client sends a POST request to the token endpoint to exchange the authorization code for an access token.
   - **URL**: `https://authorization-server.com/token`
   - **Parameters** (in the body of the POST request):
     - `grant_type=authorization_code`
     - `code=AUTH_CODE`
     - `redirect_uri=YOUR_REDIRECT_URI`
     - `client_id=YOUR_CLIENT_ID`
     - `client_secret=YOUR_CLIENT_SECRET`

5. **Access Token Issued**: The authorization server responds with an access token.
   - **Response**:
     ```json
     {
       "access_token": "ACCESS_TOKEN",
       "token_type": "Bearer",
       "expires_in": 3600,
       "refresh_token": "REFRESH_TOKEN"
     }
     ```

6. **Client Accesses Resources**: The client uses the access token to access protected resources.
   - **Request**: `https://resource-server.com/api/resource`
   - **Headers**:
     - `Authorization: Bearer ACCESS_TOKEN`

### 2. **Implicit Grant**

Used for client-side applications where the access token is returned directly in the URL fragment. This is generally used for Single Page Applications (SPAs).

#### Example Steps:

1. **User Requests Access**: The user initiates a request to access a protected resource.
   - **URL**: `https://authorization-server.com/auth`
   - **Parameters**:
     - `response_type=token`
     - `client_id=YOUR_CLIENT_ID`
     - `redirect_uri=YOUR_REDIRECT_URI`
     - `scope=YOUR_SCOPES`
     - `state=RANDOM_STATE_STRING`

2. **User Authenticates**: The user is redirected to the authorization server, where they authenticate and authorize the client application.

3. **Access Token Issued**: The authorization server redirects the user back to the client's `redirect_uri` with an access token in the URL fragment.
   - **Redirect URL**: `https://yourapp.com/callback#access_token=ACCESS_TOKEN&token_type=Bearer&expires_in=3600&state=RANDOM_STATE_STRING`

4. **Client Accesses Resources**: The client extracts the access token from the URL fragment and uses it to access protected resources.
   - **Request**: `https://resource-server.com/api/resource`
   - **Headers**:
     - `Authorization: Bearer ACCESS_TOKEN`

### 3. **Client Credentials Grant**

Used for machine-to-machine communication where the client itself is authorized, not a user.

#### Example Steps:

1. **Client Requests Access Token**: The client sends a POST request to the token endpoint with its credentials.
   - **URL**: `https://authorization-server.com/token`
   - **Parameters** (in the body of the POST request):
     - `grant_type=client_credentials`
     - `client_id=YOUR_CLIENT_ID`
     - `client_secret=YOUR_CLIENT_SECRET`
     - `scope=YOUR_SCOPES`

2. **Access Token Issued**: The authorization server responds with an access token.
   - **Response**:
     ```json
     {
       "access_token": "ACCESS_TOKEN",
       "token_type": "Bearer",
       "expires_in": 3600
     }
     ```

3. **Client Accesses Resources**: The client uses the access token to access protected resources.
   - **Request**: `https://resource-server.com/api/resource`
   - **Headers**:
     - `Authorization: Bearer ACCESS_TOKEN`

### 4. **Resource Owner Password Credentials Grant**

Used when the client is absolutely trusted, such as a first-party application. The user provides their credentials directly to the client.

#### Example Steps:

1. **Client Requests Access Token**: The client sends a POST request to the token endpoint with the user’s credentials.
   - **URL**: `https://authorization-server.com/token`
   - **Parameters** (in the body of the POST request):
     - `grant_type=password`
     - `username=USER_NAME`
     - `password=USER_PASSWORD`
     - `client_id=YOUR_CLIENT_ID`
     - `client_secret=YOUR_CLIENT_SECRET`
     - `scope=YOUR_SCOPES`

2. **Access Token Issued**: The authorization server responds with an access token.
   - **Response**:
     ```json
     {
       "access_token": "ACCESS_TOKEN",
       "token_type": "Bearer",
       "expires_in": 3600,
       "refresh_token": "REFRESH_TOKEN"
     }
     ```

3. **Client Accesses Resources**: The client uses the access token to access protected resources.
   - **Request**: `https://resource-server.com/api/resource`
   - **Headers**:
     - `Authorization: Bearer ACCESS_TOKEN`

### Summary

OAuth 2.0 provides multiple grant types to accommodate different scenarios for authorization. Each grant type has its own flow and use case:
- **Authorization Code Grant**: Suitable for web applications with a backend server.
- **Implicit Grant**: Suitable for single-page applications where the client-side is directly interacting with the authorization server.
- **Client Credentials Grant**: Suitable for server-to-server communication.
- **Resource Owner Password Credentials Grant**: Suitable for trusted applications where the user’s credentials are provided directly.

Each grant type follows a sequence of authorization and token exchange steps to obtain and use access tokens for accessing protected resources.