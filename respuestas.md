Floating point exception
Al tener la funcion definida dentro de if en el  .c
#ifdef TRAPFPE
#include "fpe_x87_sse.h"
#endif
hace que requiera agregar -DTRAPFPE en el compilador para que ejecute include "fpe_x87_sse.h" 

 gcc -Ifpe_x87_sse/ -DTRAPFPE test_fpe1.c -o test_fpe1.e

Con -Ifpe_x87_sse/ asigno el path al subdirectorio!!

Para hacer el linkeo, genero los objetos del programa y la funcion y linkeo:

gcc fpe_x87_sse.o test_fpe1.o -lm -o main1.e . 

Tuve que agregar -lm para que me linkee con la libreria matematica. Compilo a main1.e con exito!!!!


Si compilo sin -DTRAPFPE, "fpe_x87_sse.h" no se define ni se incluye en el ejecutable.

creo objeto con TRAP
gcc -c -DTRAPFPE test_fpe2.c -o test_fpe2.o

EJECUTO
wtpc-23@ws15:~/HOdebug-profile/debug/fpe$ ./test_fpe2trap.e 
Insert a, b 
5.
0.
Excepción de coma flotante (`core' generado)

Error del GDB
Program received signal SIGFPE, Arithmetic exception.
0x00000000004007f1 in main ()
(gdb)

Conclusion: al compilar con el flag -DTRASSdasdkj, el ejecutable incluye la funcion fpe_x87_sse.c que comunica al programa cuando se ejecutan operaciones aritmeticas indebidas (por ejemplo dividir por cero), interrumpiendo la ejecucion.

Con el archivo fpe3 idem que con el fpe2. Interrumpe en aritmetica indebida, en este caso, raices negativas y divisiones por 0.



