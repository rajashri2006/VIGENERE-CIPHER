# VIGENERE-CIPHER
## EX. NO: 4
 

## IMPLEMETATION OF VIGENERE CIPHER
 

## AIM:

To implement the Vigenere Cipher substitution technique using C program.

## DESCRIPTION:

To encrypt, a table of alphabets can be used, termed a tabula recta, Vigenère square,or Vigenère table. It consists of the alphabet written out 26 times in differnt rows, each
 
alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses adifferent alphabet from one of the rows. The alphabet used at each point repeating keyword.depends on a Each row starts with a key letter. The remainder of the row holds the letters A to Z. Although there are 26 key rows shown, you will only use as many keys as there are unique letters in the key string, here just 5 keys, {L, E, M, O, N}. For successive letters of the message, we are going to take successive letters of the key string, and encipher each message letter using its corresponding key row. Choose the next letter of the key, go along that row to find the column heading that	atches the message character; the letter at the intersection of
[key-row, msg-col] is the enciphered letter.


## ALGORITHM:

STEP-1: Arrange the alphabets in row and column of a 26*26 matrix.
STEP-2: Circulate the alphabets in each row to position left such that the first letter is attached to last.
STEP-3: Repeat this process for all 26 rows and construct the final key matrix.
STEP-4: The keyword and the plain text is read from the user.
STEP-5: The characters in the keyword are repeated sequentially so as to match with that of the plain text.
STEP-6: Pick the first letter of the plain text and that of the keyword as the row indices and column indices respectively.
STEP-7: The junction character where these two meet forms the cipher character.
STEP-8: Repeat the above steps to generate the entire cipher text.


## PROGRAM

```
#include <stdio.h>
#include <string.h>
#include <ctype.h>


void buildVigenereTable(char table[26][26]) {
    for (int i = 0; i < 26; i++) {
        for (int j = 0; j < 26; j++) {
            table[i][j] = 'A' + (i + j) % 26;
        }
    }
}


void extendKey(char *plaintext, char *key, char *extendedKey) {
    int textLen = strlen(plaintext);
    int keyLen = strlen(key);
    int j = 0;

    for (int i = 0; i < textLen; i++) {
        if (isalpha(plaintext[i])) {
            extendedKey[i] = key[j % keyLen];
            j++;
        } else {
            extendedKey[i] = plaintext[i]; 
        }
    }
    extendedKey[textLen] = '\0';
}


void encrypt(char *plaintext, char *key, char table[26][26], char *ciphertext) {
    char extendedKey[1000];
    int len = strlen(plaintext);

    extendKey(plaintext, key, extendedKey);

    for (int i = 0; i < len; i++) {
        char p = toupper(plaintext[i]);
        char k = toupper(extendedKey[i]);

        if (isalpha(p)) {
            int row = p - 'A';
            int col = k - 'A';
            ciphertext[i] = table[row][col];
        } else {
            ciphertext[i] = plaintext[i]; 
        }
    }
    ciphertext[len] = '\0';
}

int main() {
    char plaintext[1000], keyword[100], ciphertext[1000];
    char table[26][26];

   
    printf("Enter the plaintext: ");
    fgets(plaintext, sizeof(plaintext), stdin);
    plaintext[strcspn(plaintext, "\n")] = '\0'; // remove newline

    printf("Enter the keyword: ");
    scanf("%s", keyword);

  
    buildVigenereTable(table);

  
    encrypt(plaintext, keyword, table, ciphertext);

    printf("Cipher Text: %s\n", ciphertext);

    return 0;
}


```

## OUTPUT

<img width="810" height="304" alt="image" src="https://github.com/user-attachments/assets/e0dc95aa-5c0d-40ca-b96d-3b2aab99d558" />


## RESULT

Thus the implementation of Vigenere Cipher substitution technique using C program is executed successfully.
