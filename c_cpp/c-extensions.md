### C Extensions

- ```__attribute__((cleanup(cleanup_f)))```

```c

#define auto_free_cstr __attribute__((cleanup(f_cleanup_cstr)))

void f_cleanup_cstr(char **s) { 
  if(s && *s) 
    free(*str); 
}

int main(void) {
  auto_free_cstr char *s = malloc(10);
  return 0;                     // Great! s is freed when it exit its scope   
}

```
