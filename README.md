As per thee project requirement, Ive used Node.js/Express.js and MySQL

1. **MySQL Connection**:
   - The code sets up a connection to a MySQL database using the `mysql` library.
   - The connection details, such as the host, username, password, and database name, are provided in the `connection.createConnection` function.
   - The connection is established, and a success message is logged when the connection is successful.

2. **Admin Registration**:
   - The `/api/admin/signup` endpoint is created using the `POST` method.
   - When a request is made to this endpoint, the server extracts the `username`, `password`, and `email` from the request body.
   - The server then inserts the admin user information into the `users` table in the database using an `INSERT INTO` SQL query.
   - If the insertion is successful, the server responds with a JSON object containing the status, status code, and the generated `user_id`.

3. **Admin Login**:
   - The `/api/admin/login` endpoint is created using the `POST` method.
   - When a request is made to this endpoint, the server extracts the `username` and `password` from the request body.
   - The server then queries the `users` table to check if the provided credentials match an existing admin user.
   - If the login is successful (i.e., the user is an admin), the server generates a JSON Web Token (JWT) using the `jwt` library and the `user_id` as the payload.
   - The server responds with a JSON object containing the status, status code, `user_id`, and the generated `access_token`.

4. **Create Match (admin only)**:
   - The `/api/matches` endpoint is created using the `POST` method and is protected by the `verifyToken` middleware.
   - When a request is made to this endpoint, the server extracts the `team_1`, `team_2`, `date`, and `venue` from the request body.
   - The server then inserts the match information into the `matches` table in the database using an `INSERT INTO` SQL query.
   - If the insertion is successful, the server responds with a JSON object containing a success message and the generated `match_id`.

5. **Get Match Schedules (guest)**:
   - The `/api/matches` endpoint is created using the `GET` method.
   - When a request is made to this endpoint, the server queries the `matches` table to fetch all the available matches.
   - The server responds with a JSON object containing an array of all the matches.

6. **Get Match Details (guest)**:
   - The `/api/matches/:matchId` endpoint is created using the `GET` method.
   - When a request is made to this endpoint, the server extracts the `matchId` from the URL parameter.
   - The server then queries the `matches` table to fetch the details of the specified match.
   - Additionally, the server queries the `players` table to fetch the squad information (players) for each team.
   - The server responds with a JSON object containing the match details and the squad information for both teams.

7. **Add a Team Member to a Squad (admin only)**:
   - The `/api/teams/:teamId/squad` endpoint is created using the `POST` method and is protected by the `verifyToken` middleware.
   - When a request is made to this endpoint, the server extracts the `teamId` from the URL parameter and the `name` and `role` from the request body.
   - The server then inserts the new player information into the `players` table in the database using an `INSERT INTO` SQL query.
   - If the insertion is successful, the server responds with a JSON object containing a success message and the generated `player_id`.

8. **Get Player Statistics (logged in user)**:
   - The `/api/players/:playerId/stats` endpoint is created using the `GET` method and is protected by the `verifyToken` middleware.
   - When a request is made to this endpoint, the server extracts the `playerId` from the URL parameter.
   - The server then queries the `player_stats` table to fetch the statistics for the specified player.
   - The server responds with a JSON object containing the player's statistics.

9. **Middleware: `verifyToken`**:
   - The `verifyToken` middleware is used to protect the admin-only endpoints (`POST /api/matches` and `POST /api/teams/:teamId/squad`).
   - When a request is made to these endpoints, the middleware extracts the `Authorization` header from the request, which should contain the JWT token.
   - The middleware then verifies the JWT token using the `jwt` library and the secret key.
   - If the token is valid, the middleware sets the `userId` in the request object and calls the next middleware or route handler.
   - If the token is invalid, the middleware responds with a 401 Unauthorized error.

At the end, this implementation provides a basic structure for a Cricbuzz-like platform.
