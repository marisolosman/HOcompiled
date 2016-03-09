#Ejercicios:

#En un archivo de texto respuestas.md:

#    Escriban qué esperan de cada uno de los pasos
1 Pre-proceso: ejecute la sentencia

´´´gcc -E calculator.c -o calculator.pp.c´´´

cuando preproceso, gcc se encargo del calculator.h que a su vez
tiene el include studio.h
Me genero el archivo calculator.pp.c

2 Pimera parte del compilado: Paso de C a assembler:
ejecute al sentencia

´´´gcc -S calculator.pp.c -o calculator.asm´´´

traduce mi codigo de C a assembler generando el archivo calculator.asm
assembler es un lenguaje muy cercano al de la maquina, pero es un quilombo
programar en assembler. por eso programo en C y luego traduzco

3. Compilado 2: Paso de assemble al lenguaje de maquina (binario)
ejecute la sentencia
´´´gcc -c calculator.asm -o calculator.o´´´
Hacerlo asi y no usar el archivo calculator.o me devuelve un warning, pero
se compila

4.linkeo: genero el ejecutable
ejecute la sentencia
´´´gcc -v calculator.o -o calculator.e´´´

obtengo un ejecutable
´´´./calculator.e 
I know how to add! 31 + 11 is 42´´´

#    ¿Qué agregó el preprocesador?
en el preprocesado, que prepara mi codigo para el compilado, genero el archivo

calculator.pp.c
Con los include que mencione antes resueltos
#    Identificar en la rutina de assembler las funciones

En el codigo calculator.asm las funciones son

add_numbers y printf

#    Explicar qué quieren decir los símbolos que se crean en el objeto
                 T add_numbers
0000000000000000 T main
                 U printf

printf es undefined porque no es propia de mi codigo
main y add_numbers si son propias por eso la T, son segmentos ejecutables


#    ¿En qué se diferencian los símbolos del objeto y del ejecutable?

hay un monton de simbolos. respecto al objeto, printf aparece ahora de esta manera
 U printf@@GLIBC_2.2.5
está linkeado dinamicamente a GLIBC_2.2.5

Símbolos

#El archivo visibility.c tiene muchos tipos de símbolos. En este trabajo 
#sólo tienen que compilar el objeto visibility.o e identificar los símbolos,
 ejecutando:

make object
ejecuto
´´´gcc -c visibility.c -o visibility.o´´´

0000000000000000 t add_abs
000000000000002a T main
                 U printf
0000000000000000 r val1
0000000000000004 R val2
0000000000000000 d val3
0000000000000004 D val4

Otra vez tengo printf undefined, T para el main y t add_abs, como algo interno
porque asi esta en el .c (static int add_abs). tambien son internas val1, que es constante entonces es solo lectura y val3, que es dato y puede cambiar su valorEn cambio Val4 y Val2 no son internas, una es constante y otra no

