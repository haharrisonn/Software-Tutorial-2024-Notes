# Skeleton Code

> Please don't include any extra libraries in your homework. We already included
> all necessary libraries in the skeleton code.

```c
#include <stdio.h>
#include <string.h>
#include <stdint.h>
#include <stdbool.h>

const char* const error_msg_decimal = "Error! That set of number is not a decimal number.\n";
const char* const error_msg_trinary = "Error! That set of number is not a trinary number.\n";
const char* const error_msg_duodecimal = "Error! That set of number is not a duodecimal number.\n";
const char* const error_msg_unsupported_system = "Error! The number system is not supported.\n";

const char* const msg_prompt_number = "Please enter a set of number:\n";
const char* const msg_prompt_current_number_system = "Please enter the current number system:\n";
const char* const msg_prompt_number_system_to_convert = "Please enter the number system you want the set of number be converted to:\n";
const char* const msg_output = "Output=";

int tri_to_dec(const char* input);
void dec_to_tri(int input, char trinary[]);
void dec_to_duo(int input, char duodecimal[]);
int duo_to_dec(const char* input);
void duo_to_tri(const char* input, char trinary[]);
int atoi(const char* input);

int main(){
    char input[20];
    int system, convert;

    printf("%s", msg_prompt_number);
    scanf("%s", input);

    /**
     * @brief 
     * Get user input for number to be convert
     */

    // TODO:

    printf("%s", msg_prompt_current_number_system);
    scanf("%d", &system);
    if(system != 3 && system != 10 && system != 12){
        printf("%s", error_msg_unsupported_system);
        return 1;
    }

    /**
     * @brief 
     * Get user input for current number system
     */

    // TODO:

    printf("%s", msg_prompt_number_system_to_convert);
    scanf("%d", &convert);
    if(convert != 3 && convert != 10 && convert != 12){
        printf("%s", error_msg_unsupported_system);
        return 1;
    }

    /**
     * @brief 
     * Get user input for the number system for conversion.
     * Print converted number in format of "Output=12", e.g Output=ABCDEF
     * No space should be inserted in the asnwer "Output=XXX".
     * In case of wrong number system for conversion, please use the above error msgs.
     */

    // TODO:

    if(system == 3){
        if(convert == 10){
            printf("%s%d\n", msg_output, tri_to_dec(input));
        }
        else if(convert == 12){
            char duodecimal[20];
            dec_to_duo(tri_to_dec(input), duodecimal);
            printf("%s%s\n", msg_output, duodecimal);
        }
    }
    else if(system == 10){
        if(convert == 3){
            char trinary[20];
            dec_to_tri(atoi(input), trinary);
            printf("%s%s\n", msg_output, trinary);
        }
        else if(convert == 12){
            char duodecimal[20];
            dec_to_duo(atoi(input), duodecimal);
            printf("%s%s\n", msg_output, duodecimal);
        }
    }
    else if(system == 12){
        if(convert == 3){
            char trinary[20];
            duo_to_tri(input, trinary);
            printf("%s%s\n", msg_output, trinary);
        }
        else if(convert == 10){
            printf("%s%d\n", msg_output, duo_to_dec(input));
        }
    }

    return 0;
}

int atoi(const char* input){
    int output = 0;
    int x = 0;
    while(input[x] == ' '){
        x++;
    }
    while(input[x] >= '0' && input[x] <= '9'){
        output = output*10 + (input[x] - '0');
        x++;
    }
    return output;
}

int tri_to_dec(const char* input) {
    int decimal = 0;
    for (int i = 0; input[i] != '\0'; i++) {
        int digit = input[i] - '0'; //char to int
        if(digit < 0 || digit > 2) {
            printf("%s", error_msg_trinary);
            return -1;
        }
        decimal = decimal * 3 + digit;
    }
    return decimal;
}

void dec_to_duo(int input, char duodecimal[]){
    int count = 0;
    while(input > 0) {
        int digit = input % 12;
        input /= 12;
        if(digit < 10) {
            duodecimal[count] = digit + '0'; //int to char
        }
        else {
            duodecimal[count] = (digit - 10) + 'A';
        }
        count += 1;
    }
    duodecimal[count] = '\0';

    for(int i = 0; i < count / 2; i++) {
        char temp = duodecimal[i];
        duodecimal[i] = duodecimal[count - i - 1]; //reverse lsit
        duodecimal[count - i - 1] = temp;
    }
}

void dec_to_tri(int input, char trinary[]){
    int count = 0;
    while(input > 0){
        trinary[count] = (input % 3) + '0'; //int to char
        input /= 3;
        count += 1;
    }
    trinary[count] = '\0';
    for(int i = 0; i < count / 2; i++){
        char temp = trinary[i];
        trinary[i] = trinary[count - i - 1]; //reverse list
        trinary[count - i - 1] = temp;
    }
}

int duo_to_dec(const char* input) {
    int decimal = 0;
    for (int i = 0; input[i] != '\0'; i++) {
        int digit;
        if(input[i] >= '0' && input[i] <= '9') {
            digit = input[i] - '0';
        }
        else if(input[i] >= 'A' && input[i] <= 'B') {
            digit = input[i] - 'A' + 10;
        }
        else {
            printf("%s", error_msg_duodecimal);
            return -1;
        }
        decimal = decimal * 12 + digit;
    }
    return decimal;
}

void duo_to_tri(const char* input, char trinary[]) {
    int decimal = duo_to_dec(input);
    if (decimal == -1) return;
    dec_to_tri(decimal, trinary);
}
// C programmers never die. They are just cast into void.
```
