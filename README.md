# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:
```
#include <stdio.h>
#include <string.h>

#define KEY "secretkey"

// Function to generate MAC
void generateMAC(char *message, char *key, char *mac) {
    int i;
    int msg_len = strlen(message);
    int key_len = strlen(key);

    for(i = 0; i < msg_len; i++) {
        mac[i] = message[i] ^ key[i % key_len];  // XOR operation
    }
    mac[msg_len] = '\0';
}

int main() {
    char message[100];
    char mac[100];
    char verify_mac[100];

    printf("Enter the message: ");
    fgets(message, sizeof(message), stdin);

    message[strcspn(message, "\n")] = '\0';

    // Generate MAC
    generateMAC(message, KEY, mac);

    printf("Generated MAC: ");
    for(int i = 0; i < strlen(mac); i++) {
        printf("%02X", mac[i]);  // print in hex
    }

    printf("\n");

    // Receiver verification
    generateMAC(message, KEY, verify_mac);

    if(strcmp(mac, verify_mac) == 0) {
        printf("MAC Verified: Message is authentic.\n");
    } else {
        printf("MAC Verification Failed.\n");
    }

    return 0;
}

```
## Output:

<img width="817" height="205" alt="image" src="https://github.com/user-attachments/assets/3c1cf050-2b3f-418b-9720-57e60b25f79f" />


## Result:
The program is executed successfully.
