Pratham's Blog
A Flask-based blogging web application where users can register, log in, read blog posts, and leave comments. The application also includes an administrator role for creating, editing, and deleting blog posts.
Features
- User registration and login
- Secure password hashing using Werkzeug
- Session management with Flask-Login
- View individual blog posts
- Add comments to blog posts (logged-in users only)
- Rich-text editing for posts and comments with Flask-CKEditor
- Admin-only post creation, editing, and deletion
- SQLAlchemy database support
- SQLite by default, with PostgreSQL support through DB_URI
- Responsive pages styled with Bootstrap 5
Tech Stack
- Backend: Python, Flask
- Database: Flask-SQLAlchemy, SQLAlchemy
- Authentication: Flask-Login, Werkzeug
- Forms and validation: Flask-WTF, WTForms
- Editor: Flask-CKEditor
- Frontend: HTML, CSS, JavaScript, Bootstrap 5
- Deployment server: Gunicorn
Project Structure
My_Blogs/
├── main.py                 # Flask application, routes, and database models
├── forms.py                # WTForms form definitions
├── requirements.txt        # Python dependencies
├── Procfile                # Gunicorn start command for deployment
├── templates/              # Jinja2 HTML templates
│   ├── about.html
│   ├── contact.html
│   ├── footer.html
│   ├── header.html
│   ├── index.html
│   ├── login.html
│   ├── make-post.html
│   ├── post.html
│   └── register.html
└── static/
    ├── assets/
    │   └── img/            # Website images and backgrounds
    ├── css/
    │   └── styles.css
    └── js/
        └── scripts.js
Getting Started
1. Clone the repository
git clone https://github.com/<your-username>/<your-repository>.git
cd <your-repository>
Replace the URL and folder name with your GitHub repository details.
2. Create and activate a virtual environment
Windows (Command Prompt):
python -m venv venv
venv\Scripts\activate
macOS / Linux:
python3 -m venv venv
source venv/bin/activate
3. Install dependencies
python -m pip install --upgrade pip
pip install -r requirements.txt
4. Configure environment variables
The application reads its Flask secret key from FLASK_KEY. Set a strong, private value before starting the app.

Windows (Command Prompt):
set FLASK_KEY=replace-with-a-long-random-secret
PowerShell:
$env:FLASK_KEY = "replace-with-a-long-random-secret"
macOS / Linux:
export FLASK_KEY="replace-with-a-long-random-secret"
The database connection is read from DB_URI. If it is not set, the application uses a local SQLite database (posts.db).

For example, to use PostgreSQL, set DB_URI to your PostgreSQL SQLAlchemy connection URI. Keep database credentials private and never commit them to GitHub.
5. Run the application
python main.py
Open http://127.0.0.1:5001 in your browser.

The database tables are created automatically when the application starts.
User Roles
- Registered users: Can log in, read posts, and comment on posts.
- Administrator: The current code grants administrator access to the user whose database ID is 1. The first account created in a fresh database will normally receive this ID and can access post management features.
Security note: The current administrator check is based on current_user.id == 1. For a production application, replace this with an explicit role or administrator field, protect destructive actions with POST requests and CSRF validation, and add appropriate authorization checks.

Deployment
The repository includes a Procfile configured to start the application with Gunicorn:
web: gunicorn main:app
For deployment, configure the hosting provider with:
- FLASK_KEY — a strong secret key
- DB_URI — your production database connection URI (optional if using the default SQLite setup, though a persistent production database is recommended)
Install the dependencies from requirements.txt and deploy using the platform's Python/Gunicorn workflow.
Notes
- The contact page currently renders the contact template; email sending is not enabled in the current code.
- The application uses the default SQLite database when DB_URI is not configured.
- Do not commit secret keys, database passwords, virtual environments, or local database files to the repository.
Author
Pratham
If you find this project useful, feel free to ⭐ the repository.
