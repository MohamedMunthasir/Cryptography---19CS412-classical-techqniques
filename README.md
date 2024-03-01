# Cryptography---19CS412-classical-techqniques


# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To develop a simple python program to implement Caeser Cipher.

## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```python
## Encryption:

def caesar_cipher(text, shift):
    encrypted_text = ""
    for char in text:
        if char.isalpha():  # Check if the character is alphabet
            shifted = ord(char) + shift
            if char.islower():
                if shifted > ord('z'):
                    shifted -= 26
                elif shifted < ord('a'):
                    shifted += 26
            elif char.isupper():
                if shifted > ord('Z'):
                    shifted -= 26
                elif shifted < ord('A'):
                    shifted += 26
            encrypted_text += chr(shifted)
        else:
            encrypted_text += char
    return encrypted_text
text = "munthasir"
shift = 3


encrypted_text = caesar_cipher(text, shift)
print("Original Text:", text)
print("Encrypted Text:", encrypted_text)

## Decryption:

def caesar_decrypt(encrypted_text, shift):
    decrypted_text = ""
    for char in encrypted_text:
        if char.isalpha():  # Check if the character is alphabet
            shifted = ord(char) - shift
            if char.islower():
                if shifted > ord('z'):
                    shifted -= 26
                elif shifted < ord('a'):
                    shifted += 26
            elif char.isupper():
                if shifted > ord('Z'):
                    shifted -= 26
                elif shifted < ord('A'):
                    shifted += 26
            decrypted_text += chr(shifted)
        else:
            decrypted_text += char
    return decrypted_text


text = "munthasir"
shift = 3

decrypted_text = caesar_decrypt(encrypted_text, shift)
print("Decrypted Text:", decrypted_text)

```

## OUTPUT:
![image](https://github.com/MohamedMunthasir/Cryptography---19CS412-classical-techqniques/assets/121957086/4548aab0-4890-4e3a-b1fe-b0a5f960f588)

## RESULT:
The program is executed successfully

---------------------------------
# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To develop a simple C  or python program to implement PlayFair Cipher.

## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```python


```

## OUTPUT:
![Screenshot 2024-03-01 132921](https://github.com/jaisurya143/Cryptography---19CS412-classical-techqniques/assets/121999338/3cfe72e5-94b7-4784-ad5f-be6b9d68c916)

## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C or python program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```python

import numpy as np

def generate_key_matrix(key):
    key = key.upper().replace(" ", "")
    n = int(len(key) ** 0.5)
    if n * n != len(key):
        raise ValueError("Key length must be a perfect square")
    key_matrix = np.array([ord(char) - ord('A') for char in key]).reshape(n, n)
    return key_matrix

def generate_inverse_key_matrix(key_matrix):
    determinant = np.linalg.det(key_matrix)
    inverse_matrix = np.linalg.inv(key_matrix)
    adjugate_matrix = np.round(inverse_matrix * determinant).astype(int)
    det_inv = pow(int(determinant), -1, 26)
    inverse_key_matrix = (adjugate_matrix * det_inv) % 26
    return inverse_key_matrix

## ENCRYPTION

def hill_encrypt(plain_text, key_matrix):
    plain_text = plain_text.upper().replace(" ", "").replace("J", "I")
    n = key_matrix.shape[0]
    while len(plain_text) % n != 0:
        plain_text += 'X'
    plain_text = [ord(char) - ord('A') for char in plain_text]
    plain_matrix = np.array(plain_text).reshape(-1, n)
    encrypted_matrix = np.dot(plain_matrix, key_matrix) % 26
    encrypted_text = ""
    for row in encrypted_matrix:
        for char in row:
            encrypted_text += chr(char + ord('A'))
    return encrypted_text

## DECRYPTION

def hill_decrypt(encrypted_text, key_matrix):
    n = key_matrix.shape[0]
    inverse_key_matrix = generate_inverse_key_matrix(key_matrix)
    encrypted_text = encrypted_text.upper().replace(" ", "").replace("J", "I")
    encrypted_text = [ord(char) - ord('A') for char in encrypted_text]
    encrypted_matrix = np.array(encrypted_text).reshape(-1, n)
    decrypted_matrix = np.dot(encrypted_matrix, inverse_key_matrix) % 26
    decrypted_text = ""
    for row in decrypted_matrix:
        for char in row:
            decrypted_text += chr(char + ord('A'))
    return decrypted_text

key = "hill"
plaintext = "SURYA"
key_matrix = generate_key_matrix(key)

encrypted_text = hill_encrypt(plaintext, key_matrix)
print("Plaintext:", plaintext)
print("Encrypted text:", encrypted_text)


decrypted_text = hill_decrypt(encrypted_text, key_matrix)
print("Decrypted text:", decrypted_text)
```
## OUTPUT:
![Screenshot 2024-02-29 164352](https://github.com/jaisurya143/Cryptography---19CS412-classical-techqniques/assets/121999338/d6942745-3ef3-49ea-ad63-3f87606d3922)

## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C or python program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```python

## ENCRYPTION

def vigenere_encrypt(plain_text, key):
    key = key.upper()
    encrypted_text = ""
    key_index = 0
    for char in plain_text:
        if char.isalpha():
            shift = ord(key[key_index % len(key)]) - ord('A')
            if char.islower():
                encrypted_char = chr((ord(char) - ord('a') + shift) % 26 + ord('a'))
            else:
                encrypted_char = chr((ord(char) - ord('A') + shift) % 26 + ord('A'))
            encrypted_text += encrypted_char
            key_index += 1
        else:
            encrypted_text += char
    return encrypted_text

## DECRYPTION

def vigenere_decrypt(encrypted_text, key):
    key = key.upper()
    decrypted_text = ""
    key_index = 0
    for char in encrypted_text:
        if char.isalpha():
            shift = ord(key[key_index % len(key)]) - ord('A')
            if char.islower():
                decrypted_char = chr((ord(char) - ord('a') - shift + 26) % 26 + ord('a'))
            else:
                decrypted_char = chr((ord(char) - ord('A') - shift + 26) % 26 + ord('A'))
            decrypted_text += decrypted_char
            key_index += 1
        else:
            decrypted_text += char
    return decrypted_text

plain_text = "surya"
key = "cipher"
encrypted_text = vigenere_encrypt(plain_text, key)
print("Original Text:", plain_text)
print("Encrypted Text:", encrypted_text)

decrypted_text = vigenere_decrypt(encrypted_text, key)
print("Decrypted Text:", decrypted_text)
```

## OUTPUT:
![Screenshot 2024-02-29 164729](https://github.com/jaisurya143/Cryptography---19CS412-classical-techqniques/assets/121999338/d427db5d-eb56-483a-8cf0-3d0558b4fd4e)

## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C or python program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```python

## ENCRYPTION

def rail_fence_encrypt(plain_text, key):
    encrypted_text = ""
    rail = [''] * key
    direction = False
    row = 0

    for char in plain_text:
        rail[row] += char
        if row == 0 or row == key - 1:
            direction = not direction
        row += 1 if direction else -1

    for i in range(key):
        encrypted_text += rail[i]

    return encrypted_text

## DECRYPTION

def rail_fence_decrypt(encrypted_text, key):
    decrypted_text = ""
    rail = [''] * key
    direction = False
    row = 0
    index = 0

    for char in encrypted_text:
        rail[row] += '*'
        if row == 0 or row == key - 1:
            direction = not direction
        row += 1 if direction else -1

    for i in range(key):
        for j in range(len(rail[i])):
            if rail[i][j] == '*' and index < len(encrypted_text):
                rail[i] = rail[i][:j] + encrypted_text[index] + rail[i][j + 1:]
                index += 1

    row = 0
    direction = False
    for i in range(len(encrypted_text)):
        decrypted_text += rail[row][0]
        rail[row] = rail[row][1:]
        if row == 0 or row == key - 1:
            direction = not direction
        row += 1 if direction else -1

    return decrypted_text

plain_text = "surya"
key = 3
encrypted_text = rail_fence_encrypt(plain_text, key)
print("Original Text:", plain_text)
print("Encrypted Text:", encrypted_text)

decrypted_text = rail_fence_decrypt(encrypted_text, key)
print("Decrypted Text:", decrypted_text)
```

## OUTPUT:
![Screenshot 2024-02-29 165220](https://github.com/jaisurya143/Cryptography---19CS412-classical-techqniques/assets/121999338/3be17f03-5a5f-47ac-bc3b-02353c870c51)

## RESULT:
The program is executed successfully
