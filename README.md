# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```
#include <stdio.h>
#include <string.h>

void encryptRailFence(char text[], int rails, char cipher[]) {
    int len = strlen(text);
    char rail[rails][len];
    int i, j;

    for (i = 0; i < rails; i++)
        for (j = 0; j < len; j++)
            rail[i][j] = '\n';

    int row = 0, down = 0;
    for (j = 0; j < len; j++) {
        rail[row][j] = text[j];

        if (row == 0)
            down = 1;
        else if (row == rails - 1)
            down = 0;

        row += down ? 1 : -1;
    }

    int index = 0;
    for (i = 0; i < rails; i++)
        for (j = 0; j < len; j++)
            if (rail[i][j] != '\n')
                cipher[index++] = rail[i][j];
    cipher[index] = '\0';
}

void decryptRailFence(char cipher[], int rails, char result[]) {
    int len = strlen(cipher);
    char rail[rails][len];
    int i, j;

    for (i = 0; i < rails; i++)
        for (j = 0; j < len; j++)
            rail[i][j] = '\n';

    int row = 0, down = 0;
    for (j = 0; j < len; j++) {
        rail[row][j] = '*';

        if (row == 0)
            down = 1;
        else if (row == rails - 1)
            down = 0;

        row += down ? 1 : -1;
    }
    int index = 0;
    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            if (rail[i][j] == '*' && index < len) {
                rail[i][j] = cipher[index++];
            }
        }
    }

    row = 0; down = 0; index = 0;
    for (j = 0; j < len; j++) {
        result[index++] = rail[row][j];

        if (row == 0)
            down = 1;
        else if (row == rails - 1)
            down = 0;

        row += down ? 1 : -1;
    }
    result[index] = '\0';
}

int main() {
    char str[1000], cipher[1000], result[1000];
    int rails;

    printf("Enter a Secret Message: \n");
    scanf(" %[^\n]", str);  

    printf("Enter number of rails: \n");
    scanf("%d", &rails);

    encryptRailFence(str, rails, cipher);
    printf("Encrypted Message: %s\n", cipher);

    decryptRailFence(cipher, rails, result);
    printf("Decrypted Message: %s\n", result);

    return 0;
}
```

# OUTPUT

<img width="940" height="449" alt="image" src="https://github.com/user-attachments/assets/91938693-bbe6-4617-bd7e-b1e528cfdd74" />


# RESULT
Thus the implementation the rail fence transposition technique using C program is successful.
