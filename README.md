<div align="center">
  
# 🎣 Security Awareness Training Platform (Work in progress)

Enterprise-style security awareness and phishing simulation platform for small IT teams, MSPs, and security-conscious organizations.

![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-Web%20Framework-black?logo=flask)
![License](https://img.shields.io/badge/License-MIT-green)

</div>

## Why This Exists

Phishing accounts for 90%+ of initial breach vectors. Most awareness training platforms are expensive enterprise tools or basic slide decks. This platform bridges the gap — real phishing simulations, interactive training modules, and progress tracking without the enterprise price tag.

## SOC & Security Team Value

This platform directly supports security operations by:

- **Reducing phishing success rates** through hands-on training
- **Improving user reporting** — trained users spot and report threats faster
- **Providing measurable metrics** — track pass rates, detection rates, and identify high-risk users
- **Supporting compliance requirements** — document security awareness training completion
- **Reducing triage workload** — fewer successful phishes means fewer incidents to investigate

## Features

### Core Functionality
- **User Authentication** - Secure registration and login system
- **Training Modules** - Interactive lessons on:
  - Phishing Basics
  - Password Security
  - Social Engineering
- **Quiz System** - Test knowledge after each module (70% to pass)
- **Phishing Simulator** - Real-world phishing email scenarios with:
  - Multiple difficulty levels
  - Timed challenges
  - Instant feedback with red flag analysis
- **Progress Tracking** - Visual dashboards showing completion rates
- **Admin Panel** - Monitor team progress and phishing detection rates

### Design
- Modern, responsive UI
- Clean gradient theme
- Mobile-friendly layout
- Real-time statistics
  

## Screenshots

### Landing Page
![Landing Page](docs/screenshots/Landing.png)

### Dashboard
![Dashboard](docs/screenshots/Dashboard.png)

### Training Module
![Training Module](docs/screenshots/Training%20Module.png)

### Quiz
![Quiz](docs/screenshots/Quiz.png)

### Phishing Simulator
![Phishing Simulator](docs/screenshots/Phishing%20Sim.png)

### Phishing Scenario
![Phishing Scenario](docs/screenshots/Phishing%20Scenario.png)

### Admin Panel
![Admin Panel](docs/screenshots/Admin%20Panel.png)



## Quick Start

### Prerequisites
- Python 3.8+
- pip

### Installation

1. **Install dependencies:**
```bash
pip install -r requirements.txt
```

2. **Run the application:**
```bash
python app.py
```

3. **Access the platform:**
```
Open your browser to: http://localhost:5000
```

## First Run
On first run, `init_db()` creates a seeded `admin` account and prints the generated password to stdout. Copy it before the output scrolls away — it is not stored in plaintext anywhere. Register additional accounts normally after that.

## Usage

### For Users
1. Register a new account
2. Complete training modules in any order
3. Take quizzes to test your knowledge (70% required to pass)
4. Practice with phishing simulator scenarios
5. Track your progress on the dashboard

### For Admins
1. Login with admin credentials
2. Access Admin Panel from navigation
3. Monitor all user progress
4. Review phishing simulation statistics
5. Identify users who need additional training

## Project Structure

```
security-training-platform/
├── app.py                 # Main Flask application
├── requirements.txt       # Python dependencies
├── templates/            # HTML templates
│   ├── base.html         # Base template
│   ├── index.html        # Landing page
│   ├── login.html        # Login page
│   ├── register.html     # Registration page
│   ├── dashboard.html    # User dashboard
│   ├── module.html       # Training module view
│   ├── quiz.html         # Quiz interface
│   ├── phishing.html     # Phishing simulator list
│   ├── phishing_scenario.html  # Individual scenario
│   ├── phishing_result.html    # Scenario results
│   └── admin.html        # Admin panel
├── static/
│   └── css/
│       └── style.css     # Custom styles
└── security_training.db  # SQLite database (created on first run)
```

## Database Schema

### Users
- ID, username, email, password (hashed), is_admin, created_at

### Modules
- ID, title, description, content (HTML), quiz_questions (JSON)

### UserProgress
- ID, user_id, module_id, completed, score, completed_at

### PhishingScenarios
- ID, title, from_email, subject, body, red_flags (JSON), difficulty

### PhishingResults
- ID, user_id, scenario_id, identified_correctly, time_taken, timestamp

## Customization

### Adding New Training Modules
Edit the `init_db()` function in `app.py` to add modules:
```python
{
    'title': 'Your Module Title',
    'description': 'Module description',
    'content': '''<h3>Your HTML content here</h3>''',
    'quiz_questions': [
        {
            'question': 'Your question?',
            'options': ['Option 1', 'Option 2', 'Option 3', 'Option 4'],
            'correct': 1  # Index of correct answer (0-based)
        }
    ]
}
```

### Adding Phishing Scenarios
Add to the `scenarios` list in `init_db()`:
```python
{
    'title': 'Scenario Name',
    'from_email': 'attacker@suspicious-domain.com',
    'subject': 'Email subject line',
    'body': '''Email body content...''',
    'red_flags': [
        'Red flag 1',
        'Red flag 2',
        'Red flag 3'
    ],
    'difficulty': 'Easy'  # Easy, Medium, or Hard
}
```

## Security Notes

- Passwords are hashed using Werkzeug's security functions
- Session management with secure secret keys
- SQLite database for easy deployment
- Input validation on all forms

## Deployment Recommendations

For production deployment:
1. The secret key is randomized at startup — no manual change needed, but set `SECRET_KEY` as an environment variable for a stable value across restarts
2. Set `debug=False` in `app.run()`
3. Use a production WSGI server (Gunicorn, uWSGI)
4. Consider PostgreSQL instead of SQLite
5. Add HTTPS/SSL certificates
6. Implement rate limiting
7. Add email notification features
8. Set up automated database backups

## Future Enhancements

- [ ] Email notifications for completed training
- [ ] Certificate generation upon completion
- [ ] More training modules (ransomware, data protection, GDPR)
- [ ] Scheduled phishing campaigns
- [ ] Detailed analytics and reporting
- [ ] Multi-language support
- [ ] Integration with LDAP/Active Directory
- [ ] Custom branding options
- [ ] Export reports to PDF/CSV

## License

MIT License — see [LICENSE](LICENSE) for details.

---

<div align="center">

Built by [Rootless-Ghost](https://github.com/Rootless-Ghost) 

</div>
