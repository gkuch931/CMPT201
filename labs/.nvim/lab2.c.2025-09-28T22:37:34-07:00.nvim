#define _POSIX_C_SOURCE 200809L
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
  char *line = NULL;
  size_t len = 0;
  char *saveptr;
  while (1) {
    printf("Enter a command: ");
    getline(&line, &len, stdin);
    char *token = strtok_r(line, "\n", &saveptr);
    pid_t id = fork();
    if (id == 0) {
      // printf("command to be run: %s\n", token);
      if (execl(token, token, NULL) == -1) {
        perror("Exec failure");
      };
    } else {
      int wstatus = 0;
      if (waitpid(id, &wstatus, 0) == -1) {
        perror("waitpid");
        exit(EXIT_FAILURE);
      }
      printf("Finished waiting on %d\n", id);
    }
  }
}
