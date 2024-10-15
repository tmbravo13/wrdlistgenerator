import random
import string

# Expanded list of common words and phrases typically used in passwords
common_words = [
    'admin', 'password', '123456', 'qwerty', 'abc123', 'password1', 'letmein', 'welcome',
    '12345678', 'iloveyou', 'football', 'baseball', 'dragon', 'superman', 'batman', 'trustno1',
    '123123', '654321', '111111', '987654', 'guest', 'test', 'root', 'server', 'admin123', '2024',
    '1990', '1987', '000000', '12345', 'passw0rd', 'sunshine', 'master', 'login', 'starwars', 'shadow',
    'monkey', 'cheese', 'princess', 'pass123', 'love123', 'godzilla', 'trustme', 'secret', 'access', 
    'ninja', 'hunter', 'shadow123', 'summer2023', 'winter2023', 'spring2023', 'autumn2023', 'coolguy', 
    'coolgirl', 'sex123', 'hello123', 'yankees', 'lakers', 'champion', 'hacker', 'root123', 'admin2023', 
    'football123', 'baseball123', 'soccer123', 'superuser', 'manager', 'apple', 'orange', 'banana', 
    'charlie', 'michael', 'jessica', 'jordan', 'freedom', 'mercury', 'jupiter', 'password2023', '987654321', 
    'mypassword', 'changeme', 'testing', 'godmode', 'newpassword', 'mypassword123', 'start123', 'house123', 
    'red123', 'blue123', 'skywalker', 'joker', 'guest123', 'insecure', 'black123', 'white123', 'gandalf', 
    'dumbledore', 'chocolate', 'sunshine123', 'batman123', 'superman123', 'wonderwoman', 'pikachu', 'naruto', 
    'pokemon123', 'mypass123', 'test1234', 'securepassword', 'opensesame', 'silver', 'golden', 'football2023'
]

# Function to generate password wordlist
def generate_passwords(include_upper, include_lower, include_numbers, include_symbols, length, wordlist_size):
    characters = ''
    if include_upper:
        characters += string.ascii_uppercase
    if include_lower:
        characters += string.ascii_lowercase
    if include_numbers:
        characters += string.digits
    if include_symbols:
        characters += string.punctuation
    
    passwords = []

    # Start with some common words
    for word in common_words:
        if len(word) <= length:
            passwords.append(word)

    # Generate random passwords
    while len(passwords) < wordlist_size:
        password = ''.join(random.choice(characters) for _ in range(length))
        passwords.append(password)
    
    return passwords

# Function to save passwords to a file
def save_to_file(passwords, filename="password_wordlist.txt"):
    with open(filename, 'w') as f:
        for password in passwords:
            f.write(password + '\n')
    print(f"Passwords saved to {filename}")

# Introduction
def introduction():
    print("Welcome to the Automated Password Generator!")
    print("This script will generate a wordlist of passwords similar to the famous rockyou.txt file.")
    print("You'll be able to select the types of characters to include, the length of the passwords, and more.")
    print("Let's get started!\n")

# Main menu for character selection and password length
def main_menu():
    print("Please select the character types you want to include in the password:")
    
    include_upper = input("Include UPPERCASE letters? (y/n): ").lower() == 'y'
    include_lower = input("Include lowercase letters? (y/n): ").lower() == 'y'
    include_numbers = input("Include numbers? (y/n): ").lower() == 'y'
    include_symbols = input("Include symbols (e.g., @, #, $, %)? (y/n): ").lower() == 'y'

    length = int(input("Enter the desired password length (e.g., 8): "))
    wordlist_size = int(input("How many passwords do you want to generate?: "))

    return include_upper, include_lower, include_numbers, include_symbols, length, wordlist_size

# Main function to run the script
def run_password_generator():
    introduction()
    include_upper, include_lower, include_numbers, include_symbols, length, wordlist_size = main_menu()

    print("\nGenerating passwords...")
    passwords = generate_passwords(include_upper, include_lower, include_numbers, include_symbols, length, wordlist_size)
    
    save_to_file(passwords)
    print("\nPassword generation complete!")

# Run the password generator script
if __name__ == "__main__":
    run_password_generator()
