# Tensores (Arrays multidimensionales)

# Array (puntero)

```c
double* array = malloc(M*N*sizeof(*array));
```



# Punteros a arrays
```c
int (*array4)[NCOLUMNS] = malloc(nrows * sizeof(*array4));
```

```c
int (*array5)[NROWS][NCOLUMNS] = malloc(sizeof(*array));
```



## Referencia

* https://en.wikibooks.org/wiki/C_Programming/Common_practices#Dynamic_multidimensional_arrays
* http://c-faq.com/aryptr/dynmuldimary.html
