```markdown
# Théorie des Codes - TP 2: Chiffrement de Vigenère

## Description

Ce projet implémente le chiffrement et déchiffrement de Vigenère en C++. Le chiffrement de Vigenère est une méthode de substitution polyalphabétique qui utilise une clé pour chiffrer un texte clair. Le projet inclut également une méthode de cryptanalyse qui permet de casser ce chiffrement en utilisant l'Indice de Coïncidence (IC) et un test du χ².

## Fonctionnalités

- **Chiffrement de Vigenère**
- **Déchiffrement de Vigenère**
- **Cryptanalyse pour casser le chiffrement**
- Gestion des caractères alphabétiques et non-alphabétiques

## Installation

Pour compiler et exécuter ce programme, vous avez besoin de g++ ou d'un autre compilateur C++.

### Compilation

```bash
g++ -o vigenere main.cpp
```

### Exécution

```bash
./vigenere
```

## Utilisation

### Exemple de chiffrement

```cpp
#include "vigenere.h"

Vigenere cipher("algorythme");
string encrypted = cipher.encrypt("pythagore");
cout << encrypted << endl; // Affiche le texte chiffré
```

### Exemple de déchiffrement

```cpp
#include "vigenere.h"

Vigenere cipher("algorythme");
string decrypted = cipher.decrypt("pjzvrehyq");
cout << decrypted << endl; // Affiche le texte déchiffré
```

### Cryptanalyse

Le programme propose aussi une fonction de cryptanalyse pour casser le chiffrement en utilisant l'Indice de Coïncidence.

```cpp
string cryptanalyse(string ciphertext);
```

## Structure du projet

- `main.cpp` : Le fichier principal contenant le point d'entrée du programme.
- `vigenere.h` et `vigenere.cpp` : Contiennent l'implémentation des fonctions de chiffrement, de déchiffrement et de cryptanalyse.
- `README.md` : Ce fichier qui documente le projet.

## Implémentation

### Chiffrement de Vigenère

Le chiffrement se fait caractère par caractère en utilisant la clé pour déterminer le décalage.

```cpp
string Vigenere::encrypt(string text) {
    string result;
    int keyIndex = 0;
    for (char c : text) {
        if (isalpha(c)) {
            char shift = toupper(key[keyIndex % key.length()]) - 'A';
            char encryptedChar = (toupper(c) - 'A' + shift) % 26 + 'A';
            result += encryptedChar;
            keyIndex++;
        } else {
            result += c;
        }
    }
    return result;
}
```

### Déchiffrement de Vigenère

Le déchiffrement est similaire au chiffrement, mais on applique l'inverse du décalage.

```cpp
string Vigenere::decrypt(string text) {
    string result;
    int keyIndex = 0;
    for (char c : text) {
        if (isalpha(c)) {
            char shift = toupper(key[keyIndex % key.length()]) - 'A';
            char decryptedChar = (toupper(c) - 'A' - shift + 26) % 26 + 'A';
            result += decryptedChar;
            keyIndex++;
        } else {
            result += c;
        }
    }
    return result;
}
```

### Cryptanalyse

L'algorithme de cryptanalyse utilise l'Indice de Coïncidence (IC) pour estimer la longueur de la clé, puis un test du χ² pour retrouver la clé.

```cpp
int findKeyLength(const string &text);
string findKey(const string &text, int keyLength);
string cryptanalyse(string ciphertext);
```

## Auteurs

- **ZZ3 F5** - Réseaux et Sécurité
```

Ce fichier `README.md` contient les instructions et la documentation nécessaires pour comprendre et utiliser ton projet de chiffrement de Vigenère en C++.
