* strlen(str)
* strcpy(dest_str, src_str)
* strncpy(dest_str, src_str, n)  copies at most n values from the src, if the src has less than n fills with null values
* strcat(str1, str2) concatenates the two strings and puts in str1
* strcat(str1, str2, n) copies only n characters from str2
* strcmp(str1, str2) compares based on the weightage of ascii , applen>apple, returns <0 if s1< s2
* strncmp(str1, str2, n) compares only the first n terms based on weight but strncmp("apple", "applen", 4) gives result 0(equal)
* strchr(str, char) gives pointer to first occurrence of a character in a string, returns NULL if not available , array indexing starts from 0
* strrchr(str, char), gives the last occurrence of the character in the string
* strstr(str, substr) first occurence of a substring in a string and returns NULL if not found
* sprintf(str, "reference text %d", n);  converts this all to a string and stores in str
* strtok(str, char), splits the given string into substrings based on the occurrence of the given char
