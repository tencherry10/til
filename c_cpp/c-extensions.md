### C Extensions

1. auto cleanup on scope exit: ```__attribute__((cleanup(cleanup_f)))```

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

1. labels as values

  ```c
  int main(){
    int value  = 2;
    const void *labels[] = {&&val_0, &&val_1, &&val_2};
    goto *labels[value];
    val_0:
        printf("The value is 0\n");
        goto end;
    val_1:
        printf("The value is 1\n");
        goto end;
    val_2:
        printf("The value is 2\n");
        goto end;
    end:
    return 0;
  }
  ```
