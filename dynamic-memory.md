## Memoria de un programa

* Estática: Tamaño fijo durante toda la ejecución del programa
  * text: Código (lógica) del programa
  * data: Varibles globales inicializadas
  * bss: Varibles globales no inicializadas
* Automática (stack): Llamadas a funciones
* Dinámica (heap): Memoria explicitamente alojada y desalojada

![memory](https://i.stack.imgur.com/wn0oN.jpg)

## Alojar memoria: `malloc`

Aloja memoria del tamaño indicado y devuleve un puntero.

```c
int *p = malloc(n * sizeof(int));
```

Si no conces el tipo del puntero, puedes poner:

```c
int *p;
p = malloc(n * sizeof(*p));
```

Si no se pudo alojar dicha memoria, devuelve un puntero NULL, así que se debe controlarlo.

```c
if (p == NULL) {
  fprintf(stderr, "malloc failed\n");
  return(-1);
}
```

## Desalojar memoria: `free`

Cuando hallas acabado de usar esa memoria, la puedes liberar.

```c
free(p)
```
