# Intership
For password verification
import re

common_passwords = {
    "password", "123456", "qwerty",
    "admin", "welcome", "letmein"
}

def analyze_password(password):
    score = 0
    feedback = []

     
  if len(password) >= 12:
      score += 30
  elif len(password) >= 8:
      score += 15
  else:
      feedback.append("Use at least 8 characters.")

  # Complexity
  if re.search(r"[A-Z]", password):
      score += 15
  else:
      feedback.append("Add uppercase letters.")

  if re.search(r"[a-z]", password):
      score += 15
  else:
      feedback.append("Add lowercase letters.")

  if re.search(r"\d", password):
      score += 15
  else:
      feedback.append("Add numbers.")

  if re.search(r"[!@#$%^&*(),.?\":{}|<>]", password):
      score += 15
  else:
      feedback.append("Add special characters.")

  # Uniqueness
  if password.lower() not in common_passwords:
      score += 10
  else:
      feedback.append("Avoid common passwords.")

  # Rating
  if score >= 90:
      rating = "Very Strong"
  elif score >= 70:
      rating = "Strong"
  elif score >= 40:
      rating = "Moderate"
  else:
      rating = "Weak"

  return score, rating, feedback

password = input("Enter password: ")
score, rating, feedback = analyze_password(password)

print(f"\nScore: {score}/100")
print(f"Strength: {rating}")

if feedback:
    print("\nSuggestions:")
    for item in feedback:
        print("-", item)
