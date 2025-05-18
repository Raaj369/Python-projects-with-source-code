# Python Projects Collection

A curated list of Python projects with source code and tutorials. This repository contains categorized Python projects that cover various domains, including image processing, games, utilities, and more. Each project includes a tutorial to help you understand the implementation and improve your coding skills.

## 🏢 Management System Projects
- [Bank Management System Using Python Django](
Bank Management System Using Python Django
Introduction
The Bank Management System V2.0.2 is a feature-rich online banking solution built using the Python Django web framework. This system automates core banking processes, including account management, deposits, withdrawals, interest calculations, and transaction reporting. Designed for both scalability and efficiency, the system leverages tools like Redis and Celery for background task processing and scheduled operations.

The primary aim of this system is to simplify banking operations while providing users with a smooth and modern interface powered by Tailwind CSS. By supporting multiple account types (e.g., Savings and Current), imposing transaction restrictions, and offering accurate balance updates, the system enhances the reliability of online banking.

Key Features:
Account Management:

Users can create bank accounts (Savings or Current Accounts).

Deposits and Withdrawals:

Perform seamless deposit and withdrawal operations with transaction restrictions.

Interest Calculation:

Accurate monthly interest calculation based on the account type.

Scheduled tasks using Celery ensure timely interest computation.

Transaction Reports:

View transaction history with date range filtering.

Track balance updates after every transaction.

Modern UI:

Intuitive and responsive user interface using Tailwind CSS.

Scheduled Tasks:

Celery handles scheduled updates for monthly interest and balance adjustments efficiently.

This system is perfect for developers looking to explore Django’s capabilities in building reliable web-based financial applications.

How to Run the Code
To run the Bank Management System locally, follow these steps:

Prerequisites:
Ensure the following tools and software are installed on your system:

Python >= 3.7

Redis Server

Git

pip

Virtualenv

Steps to Setup:
Install Redis Server: Follow the Redis Quick Start Guide to install Redis. Start the Redis server:

redis-server
Create a Virtual Environment: Use virtualenv to set up an isolated Python environment:

virtualenv venv
source venv/bin/activate
Or using virtualenvwrapper:

mkvirtualenv -p python3 bank_system
workon bank_system
Clone the Project: Clone the GitHub repository and navigate to the project directory:

git clone git@github.com:saadmk11/banking-system.git
cd banking-system
Install Dependencies: Install required Python packages from requirements.txt:

pip install -r requirements.txt
Apply Database Migrations: Initialize the database using Django migrations:

python manage.py migrate
Create Superuser: Create an admin account for managing the system:

python manage.py createsuperuser
Run the Development Server: Start the local Django server:

python manage.py runserver
Access the application at http://127.0.0.1:8000/.

Run Celery Workers and Scheduler: Open separate terminal windows (activate the virtual environment in each terminal):

Start the Celery worker:

celery -A banking_system worker -l info
Start the Celery scheduler:

Code Explanation
The project uses the Django framework for backend development, along with Celery for background tasks and Redis for messaging.

1. Account Management:
The system supports Savings and Current accounts. The Account model stores account details:

class Account(models.Model):
    ACCOUNT_TYPES = (
        ('Savings', 'Savings Account'),
        ('Current', 'Current Account'),
    )
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    account_type = models.CharField(max_length=10, choices=ACCOUNT_TYPES)
    balance = models.FloatField(default=0.0)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"{self.user.username} - {self.account_type}"
2. Deposits and Withdrawals:
The Transaction model handles deposit and withdrawal operations with balance updates:

class Transaction(models.Model):
    TRANSACTION_TYPES = (
        ('Deposit', 'Deposit'),
        ('Withdrawal', 'Withdrawal'),
    )
    account = models.ForeignKey(Account, on_delete=models.CASCADE)
    transaction_type = models.CharField(max_length=10, choices=TRANSACTION_TYPES)
    amount = models.FloatField()
    date = models.DateTimeField(auto_now_add=True)

    def save(self, *args, **kwargs):
        if self.transaction_type == 'Deposit':
            self.account.balance += self.amount
        elif self.transaction_type == 'Withdrawal':
            if self.amount > self.account.balance:
                raise ValueError("Insufficient balance")
            self.account.balance -= self.amount
        self.account.save()
        super().save(*args, **kwargs)
This ensures transactions are validated and balances are updated correctly.

3. Interest Calculation with Celery:
Interest calculation is automated using Celery tasks, which run at scheduled intervals:

from celery import shared_task
from .models import Account

@shared_task
def calculate_monthly_interest():
    for account in Account.objects.filter(account_type='Savings'):
        interest = account.balance * 0.03  # 3% monthly interest
        account.balance += interest
        account.save()
This task ensures savings accounts accrue interest at 3% monthly.

Provided Code
The full project structure includes:

accounts/: Handles user accounts and authentication.

transactions/: Manages transactions like deposits and withdrawals.

core/: Includes Celery configurations and scheduled tasks.

templates/: Contains HTML templates for the user interface.

Notable files include:

manage.py: Django management script.

requirements.txt: Python dependencies.

banking_system/: Main project directory.)
- [Pharmacy Management System Using Python Django](https://codewithcurious.com/projects/pharmacy-management-system-using-python-django/)
- [Complain Management using Python With GUI](https://codewithcurious.com/projects/complain-management-using-python/)
- [COVID-19 Hospital Management Using Django](https://codewithcurious.com/projects/covid-19-hospital-management-django/)
- [Contact Management System In Python](https://codewithcurious.com/projects/contact-management-system-in-python/)
- [Hostel Management System Using Python](https://codewithcurious.com/projects/hostel-management-system-using-python/)
- [Library Management System Using Python](https://codewithcurious.com/projects/library-management-system-using-python/)
- [Hotel Management System Using Python](https://codewithcurious.com/projects/hotel-management-system-using-python/)
- [Student Management System Using Python](https://codewithcurious.com/projects/student-management-system-using-python/)
- [Billing Software Using Python](https://codewithcurious.com/projects/billing-software-using-python/)
- [Hospital Management Using Python](https://codewithcurious.com/projects/hospital-management-using-python/)
- [Restaurant Billing System Using Python](https://codewithcurious.com/projects/restaurant-billing-system-using-python/)



## 🎮 Python Games
- [KBC Game Using Python](https://codewithcurious.com/projects/kbc-game-using-python-source-code/)
- [21 Number Game Using Python](https://codewithcurious.com/projects/21-number-game-using-python/)
- [Typing Game Using Python](https://codewithcurious.com/projects/typing-game-using-python/)
- [A Sliding Puzzle Game in Python](https://codewithcurious.com/projects/a-sliding-puzzle-game-in-python/)
- [Spaceship Game Using Python](https://codewithcurious.com/projects/spaceship-game-using-python/)
- [Classic Memory Puzzle Game Using Python](https://codewithcurious.com/projects/classic-memory-puzzle-game-python/)
- [Memory Game Using Python](https://codewithcurious.com/projects/a-card-matching-game-using-python/)
- [Optical Illusion Game with Python](https://codewithcurious.com/projects/optical-illusing-game-using-python/)
- [Creating a Connect Four Game Using Python](https://codewithcurious.com/projects/connect-four-game-using-python-language/)
- [Cannon Game Using Python](https://codewithcurious.com/projects/cannon-game-using-python/)
- [Pacman Game with Python](https://codewithcurious.com/projects/pacman-game-using-python/)
- [Blackjack Game Using Python](https://codewithcurious.com/projects/blackjack-game-using-python/)
- [Tetris Game Using Python](https://codewithcurious.com/projects/tetris-game-using-python/)
- [Super Mario Game Using Python](https://codewithcurious.com/projects/super-mario-game-using-python-with-source-code/)
- [2048 Game Using Python](https://codewithcurious.com/projects/2048-game-using-python/)
- [Car Racing Game Using Python](https://codewithcurious.com/projects/car-racing-game-using-python/)
- [Contra Game Using Python Pygame](https://codewithcurious.com/projects/contra-game-using-python-pygame/)
- [Jungle Dash Game Using Python](https://codewithcurious.com/projects/jungle-dash-game-using-python/)
- [2D Vertical Plane Shooter Game Using Python](https://codewithcurious.com/projects/2d-vertical-plane-shooter-game-python/)
- [Flappy Bird Game Using Python](https://codewithcurious.com/projects/flappy-bird-game-using-python/)
- [Hangman Game using Python](https://codewithcurious.com/projects/hangman-game-using-python-2/)
- [Sudoku Game Using Python](https://codewithcurious.com/projects/sudoku-game-using-python/)
- [Ping Pong Game using Python](https://codewithcurious.com/projects/pingpong-game-using-python/)
- [Snake Game Using Python](https://codewithcurious.com/projects/snake-game-using-python/)
- [Rock Paper Scissor Game using Python](https://codewithcurious.com/projects/rock-paper-scissor-game-python/)

## 🐢 Turtle Graphics Projects
- [Drawing Chhatrapati Shivaji Maharaj Using Python](https://codewithcurious.com/projects/drawing-chhatrapati-shivaji-maharaj-using-python/)
- [Drawing Ganesha Using Python Turtle Graphics](https://codewithcurious.com/projects/drawing-ganesha-using-python/)
- [Valentine Day Project using Python Turtle](https://codewithcurious.com/projects/valentine-day-project-using-python-turtle/)
- [Drawing Rose Using Python Turtle](https://codewithcurious.com/projects/rose-using-turtle-pyth/)
- [Make an Indian Flag using Turtle Python](https://codewithcurious.com/projects/how-to-make-indian-flag-using-turtle-python/)
- [Drawing Pikachu Using Python](https://codewithcurious.com/projects/draw-pikachu-with-python/)
- [Draw Doraemon Using Python](https://codewithcurious.com/projects/draw-doraemon-using-python/)
- [Radha Krishna Drawing using Python](https://codewithcurious.com/projects/radha-krishan-painting-using-python/)
- [Turtle Patterns in Python](https://codewithcurious.com/projects/turtle-patterns/)
- [Drawing Patterns Using Python Turtle](https://codewithcurious.com/projects/drawing-pattern-using-python-turtle/)

## GUI Applications
- [GUI Alarm Clock Using Python](https://codewithcurious.com/projects/gui-alarmclock-using-python/)
- [GUI Based Internet Speed Test Using Python](https://codewithcurious.com/projects/gui-based-internet-speed-test-using-python/)
- [GUI Digital Clock Using Python](https://codewithcurious.com/projects/gui-digital-clock-using-python/)
- [GUI Stopwatch using Python](https://codewithcurious.com/projects/gui-stopwatch-using-python/)

## 🔍 OpenCV & AI Projects
- [QR Code & Bar Code Detection Using OpenCV Python](https://codewithcurious.com/projects/qr-code-bar-code-detection-python/)
- [Object Tracking Using OpenCV Python](https://codewithcurious.com/projects/object-tracking-using-open-cv-python/)
- [Resume Analyzer using Python](https://codewithcurious.com/projects/resume-analyzer-using-python/)
- [OMR MCQ Automated Grading Using OpenCV Python](https://codewithcurious.com/projects/omr-mco-automated-grading-python/)
- [Shape Detection Using OpenCV Python](https://codewithcurious.com/projects/shape-detection-using-open-cv-python/)
- [Text Detection Using OpenCV Python](https://codewithcurious.com/projects/text-detection-using-open-cv-python/)
- [Realtime Colour Detection Using OpenCV Python](https://codewithcurious.com/projects/realtime-colour-detection-python/)
- [Volume & Brightness Control Using OpenCV Python](https://codewithcurious.com/projects/volume-brightness-control-python/)
- [Vehicle Speed Estimation Using OpenCV Python](https://codewithcurious.com/projects/vehicle-speed-estimation-using-python/)
- [Building Our Own ChatGPT using Python](https://codewithcurious.com/projects/chatgpt-using-python/)
- [Detect Plagiarism in files using Python](https://codewithcurious.com/projects/detect-plagiarism-in-files-using-python/)
- [Language Detection of a Sentence using Python](https://codewithcurious.com/projects/language-detection-using-python/)
- [Black and White to Colour Images using Python](https://codewithcurious.com/projects/black-and-white-to-colour-image-using-python/)
- [Creating A Watermark on Image using OpenCV](https://codewithcurious.com/projects/creating-watermark-on-images-using-opencv/)
- [Convert Image Into Sketch Using Python](https://codewithcurious.com/python-projects/convert-image-into-sketch-python/)

## 🔧 Mini Projects
- [Screen Recorder Using Python](https://codewithcurious.com/projects/screen-recorder-using-python/)
- [File Sharing App Using Python](https://codewithcurious.com/projects/file-sharing-app-using-python/)
- [Automated Instagram Message Sending Using Python](https://codewithcurious.com/projects/automated-instagram-msg-sending-python/)
- [Building A WhatsApp Bot Using Python](https://codewithcurious.com/projects/build-a-whatsapp-bot-using-python/)
- [Create a Telegram Bot Using Python](https://codewithcurious.com/projects/create-a-telegram-bot-using-python/)
- [Get Info of Phone Number using Python](https://codewithcurious.com/projects/phone-number-info-using-python/)
- [Get Instagram Account Details using Python](https://codewithcurious.com/projects/get-instagram-account-details-using-python/)
- [Binary to Decimal & Decimal to Binary Converter Using Python](https://codewithcurious.com/projects/binary-to-decimal-decimal-to-binary-converter/)
- [Google Search Clone Using Python](https://codewithcurious.com/projects/google-search-clone-using-python/)
- [Convert Image to PDF Using Python GUI](https://codewithcurious.com/projects/convert-image-to-pdf-using-python-gui/)
- [Photo Collage Maker using Python](https://codewithcurious.com/projects/photo-collage-maker-using-python/)
- [Word Cloud Using Python Language](https://codewithcurious.com/projects/word-cloud-using-python/)
- [Birthday Wishes Using Python](https://codewithcurious.com/projects/birthday-wishes-using-python/)
- [OTP Verification using Python](https://codewithcurious.com/projects/otp-verification-using-python/)
- [Quiz Application Using Python](https://codewithcurious.com/projects/quiz-application-using-python/)
- [BMI Calculator using Python](https://codewithcurious.com/projects/bmi-calculator-using-python/)
- [Scientific Calculator using Python](https://codewithcurious.com/projects/scientific-calculator-using-python/)
- [Convert Text to Speech using Python](https://codewithcurious.com/projects/convert-text-to-speech-using-python/)
- [Send WhatsApp Messages Using Python](https://codewithcurious.com/projects/send-whatsapp-messages-using-python/)
- [Find Wi-Fi Passwords using Python](https://codewithcurious.com/projects/find-wifi-passwords-using-python/) 

---
Explore these projects, and happy coding! 🚀
