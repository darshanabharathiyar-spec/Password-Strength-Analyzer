# Password-Strength-Analyzer
import re
import random
import string

def check_password_strength(password):
    score = 0
    suggestions = []

    # Length Check
    if len(password) >= 12:
        score += 2
    elif len(password) >= 8:
        score += 1
    else:
        suggestions.append("Use at least 8-12 characters.")

    # Uppercase Check
    if re.search(r"[A-Z]", password):
        score += 1
    else:
        suggestions.append("Add uppercase letters.")

    # Lowercase Check
    if re.search(r"[a-z]", password):
        score += 1
    else:
        suggestions.append("Add lowercase letters.")

    # Digit Check
    if re.search(r"\d", password):
        score += 1
    else:
        suggestions.append("Add numbers.")

    # Special Character Check
    if re.search(r"[!@#$%^&*(),.?\":{}|<>]", password):
        score += 1
    else:
        suggestions.append("Add special characters.")

    # Common Password Check
    common_passwords = [
        "password", "123456", "qwerty", "admin",
        "welcome", "password123"
    ]

    if password.lower() in common_passwords:
        score = max(0, score - 2)
        suggestions.append("Avoid common passwords.")

    # Strength Rating
    if score <= 2:
        strength = "Weak"
    elif score <= 4:
        strength = "Medium"
    else:
        strength = "Strong"

    return strength, suggestions


def generate_strong_password(length=12):
    characters = string.ascii_letters + string.digits + "!@#$%^&*"
    return ''.join(random.choice(characters) for _ in range(length))


# Main Program
password = input("Enter a password: ")

strength, suggestions = check_password_strength(password)

print("\nPassword Strength:", strength)

if suggestions:
    print("\nSuggestions:")
    for s in suggestions:
        print("-", s)

if strength != "Strong":
    print("\nSuggested Strong Password:")
    print(generate_strong_password()

OUTPUT 

Enter a password: hello123

Password Strength: Medium

Suggestions:
- Add uppercase letters.
- Add special characters.

Suggested Strong Password:
T@9kL#2mP$8q