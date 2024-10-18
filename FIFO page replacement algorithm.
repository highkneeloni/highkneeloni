#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/wait.h>
#include <fcntl.h>

#define MAX 100


void typeline(char *option, char *filename) {

    FILE *file = fopen(filename, "r");

    if (file == NULL) {

        perror("Error opening file");

        return;

    }


    char line[MAX];

    if (strcmp(option, "-a") == 0) {

        while (fgets(line, MAX, file) != NULL) {

            printf("%s", line);

        }

    } else if (option[0] == '+' && strlen(option) > 1) {

        int n = atoi(option + 1);

        for (int i = 0; i < n && fgets(line, MAX, file) != NULL; i++) {

            printf("%s", line);

        }

    }


    fclose(file);

}


int main() {

    char input[MAX];

    char *args[MAX];

   

    while (1) {

        printf("myshell$ ");

        fgets(input, MAX, stdin);

        input[strlen(input) - 1] = '\0'; // remove newline character

       

        int i = 0;

        args[i] = strtok(input, " ");

        while (args[i] != NULL) {

            i++;

            args[i] = strtok(NULL, " ");

        }


        if (strcmp(args[0], "exit") == 0) {

            break;

        } else if (strcmp(args[0], "typeline") == 0 && args[1] && args[2]) {

            typeline(args[1], args[2]);

        } else {

            pid_t pid = fork();

            if (pid == 0) {

                execvp(args[0], args);

                perror("Error executing command");

                exit(1);

            } else {

                wait(NULL);

            }

        }

    }


    return 0;

}
