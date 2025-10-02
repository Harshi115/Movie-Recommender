# Movie Recommender System

A Django-based movie recommendation web application that helps users discover movies based on their preferences.

## Features

- Movie recommendation engine
- User-friendly web interface
- Media file management with AWS S3 integration
- Static file serving with WhiteNoise
- Responsive design

## Tech Stack

- **Backend**: Django 3.0.6
- **Database**: SQLite3 (Development)
- **Storage**: AWS S3 (for media files)
- **Static Files**: WhiteNoise
- **Deployment**: Heroku-ready

## Prerequisites

- Python 3.7+
- pip
- virtualenv (recommended)
- AWS Account (for S3 storage, optional for local development)

## Installation

### 1. Clone the repository

```bash
git clone <repository-url>
cd movie_recommender-master
```

### 2. Create and activate virtual environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set up environment variables

Create a `.env` file in the root directory with the following variables:

```env
# AWS Configuration (optional for local development)
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
AWS_STORAGE_BUCKET_NAME=your_bucket_name

# Django Secret Key (change in production)
SECRET_KEY=your_secret_key_here
```

### 5. Run migrations

```bash
python manage.py migrate
```

### 6. Create a superuser

```bash
python manage.py createsuperuser
```

### 7. Collect static files

```bash
python manage.py collectstatic
```

### 8. Run the development server

```bash
python manage.py runserver
```

Visit `http://127.0.0.1:8000/` in your browser.

## Project Structure

```
movie_recommender-master/
├── movie_recommender/          # Main project directory
│   ├── __init__.py
│   ├── settings.py            # Django settings
│   ├── urls.py                # URL routing
│   ├── wsgi.py                # WSGI configuration
│   ├── asgi.py                # ASGI configuration
│   └── aws/                   # AWS S3 configuration
│       ├── __init__.py
│       ├── conf.py            # AWS settings
│       └── utils.py           # S3 storage utilities
├── recommend/                  # Main application
├── static/                    # Static files (CSS, JS, images)
├── staticfiles/               # Collected static files
├── media/                     # User-uploaded media
└── manage.py                  # Django management script
```

## Configuration

### AWS S3 Setup (Optional)

To enable AWS S3 for media storage:

1. Uncomment the import in `settings.py`:
   ```python
   from movie_recommender.aws.conf import *
   ```

2. Set the required environment variables (see Installation step 4)

3. Configure your S3 bucket with appropriate permissions

### Production Settings

**Important**: Before deploying to production:

1. Set `DEBUG = False` in `settings.py`
2. Update `SECRET_KEY` with a secure random key
3. Update `ALLOWED_HOSTS` with your domain
4. Use a production database (PostgreSQL recommended)
5. Enable HTTPS

## Deployment

### Heroku Deployment

This project is configured for Heroku deployment:

1. Install Heroku CLI
2. Create a new Heroku app:
   ```bash
   heroku create your-app-name
   ```

3. Set environment variables:
   ```bash
   heroku config:set SECRET_KEY=your_secret_key
   heroku config:set AWS_ACCESS_KEY_ID=your_key
   heroku config:set AWS_SECRET_ACCESS_KEY=your_secret
   heroku config:set AWS_STORAGE_BUCKET_NAME=your_bucket
   ```

4. Deploy:
   ```bash
   git push heroku main
   ```

5. Run migrations:
   ```bash
   heroku run python manage.py migrate
   ```

## Usage

1. Access the admin panel at `/admin/` to manage content
2. Navigate to the home page to start getting movie recommendations
3. Follow the on-screen instructions to input your preferences

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Security Notes

- Never commit sensitive information (API keys, passwords) to version control
- Use environment variables for configuration
- Keep dependencies updated
- Change the default `SECRET_KEY` in production

## License

This project is open source and available under the [MIT License](LICENSE).

## Support

For issues and questions, please open an issue in the GitHub repository.

## Acknowledgments

- Django framework
- AWS S3 for storage
- WhiteNoise for static file serving
