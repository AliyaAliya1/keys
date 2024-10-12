def decrypt_vigenere(ciphertext, key):
    alphabet = "abcdefghijklmnopqrstuvwxyz"
    decrypted_text = ""
    key_length = len(key)
    
    for i, letter in enumerate(ciphertext):
        if letter.isalpha():  # Only process alphabetic characters
            key_letter = key[i % key_length].lower()
            key_index = alphabet.index(key_letter)
            cipher_index = alphabet.index(letter.lower())
            
            # Decrypt by shifting backwards
            decrypted_letter = alphabet[(cipher_index - key_index) % 26]
            decrypted_text += decrypted_letter
        else:
            decrypted_text += letter  # Non-alphabetic characters remain unchanged
    
    return decrypted_text

# Ciphertext
ciphertext = "yrgzxeyiskmkxer"

# Read the key from key.txt
with open("key.txt", "r") as key_file:
    key = key_file.read().strip()

# Decrypt
decrypted_message = decrypt_vigenere(ciphertext, key)
print("Decrypted message:", decrypted_message)

# Check against the password list
password_file = "10-million-password-list-top-100000.txt"
try:
    with open(password_file, "r") as file:
        passwords = file.read().splitlines()  # Read all lines into a list
        if decrypted_message in passwords:
            print("The decrypted message is in the password list!")
        else:
            print("The decrypted message is NOT in the password list.")
except FileNotFoundError:
    print(f"The file {password_file} does not exist.")
