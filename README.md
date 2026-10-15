# Lab 5 Postman and APIs

**Student:** Haidar Saghir  
**Course:** ECE 435L Software Tools Lab

This project provides the five Flask endpoints in the Lab 5 handout. They create, read, update, and delete users in a local SQLite database. The Postman collection includes all five requests, a saved successful response example for each one, and automated response checks.

## Run the API

From this project folder, use Python 3.9 or newer:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python app.py
```

The server starts at `http://localhost:5000`. Opening `http://localhost:5000/api/users` in a browser should show `[]` before any users are added. The `database.db` file is created automatically when the app starts. Python includes `sqlite3`, so it does not need a separate package installation.

## API routes

| Method | Route | Purpose |
| --- | --- | --- |
| GET | `/api/users` | List all users |
| GET | `/api/users/<user_id>` | Get one user |
| POST | `/api/users/add` | Add a user |
| PUT | `/api/users/update` | Update a user |
| DELETE | `/api/users/delete/<user_id>` | Delete a user |

POST requires `name`, `email`, `phone`, `address`, and `country` as nonempty JSON strings. PUT requires those fields plus a positive integer `user_id`. Both return JSON. Invalid input returns HTTP 400; an unknown user ID returns HTTP 404.

## Run the Postman collection

1. Import `postman/Flask-user-app.postman_collection.json` and `postman/Flask-user-app-local.postman_environment.json` into Postman.
2. Select the **Flask user app local** environment. Its `base_url` variable is `http://localhost:5000`.
3. Start the Flask server and run the collection in order: Add user, Get all users, Get user by ID, Update user, Delete user. Add user saves the new ID to the `user_id` environment variable.
4. Open a request's **Examples** section to inspect its saved response. The examples were captured from the running Flask app with a temporary database.

Each collection run adds and then deletes one sample user. Existing users in `database.db` are left in place.

## Run automated tests

```powershell
python -m unittest discover -s tests -v
```

The tests use a temporary SQLite database and exercise the full CRUD flow plus invalid requests and missing users.

## Moodle submission evidence

The repository includes `database.db` with the `users` table. The `screenshots/` folder is for one Postman screenshot per request, showing the request method, URL, and result together. Run the collection requests in order and save screenshots as `01-post-add-user.png`, `02-get-all-users.png`, `03-get-user-by-id.png`, `04-put-update-user.png`, and `05-delete-user.png`.
