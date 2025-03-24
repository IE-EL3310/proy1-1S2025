# Proyecto 1: Generación de CRC32 para textos de entrada
### EL3310 - Diseño de Sistemas Digitales
### Escuela de Ingeniería Electrónica
### Tecnológico de Costa Rica


### Preámbulo

Para el desarrollo de este proyecto, usted deberá contar con una instalación de LiteX, ya sea de forma nativa o mediante una máquina virtual. En la [wiki](https://github.com/EL4314/Laboratorio1_1Sem23/wiki/Home) de este repositorio se tiene una serie de guías que lo ayudaran a tener ya sea una maquina virtual con LiteX o un contenedor de docker con LiteX. 

<br/><br/>

### Comprobación de Redundancia Cíclica de 32 bits

Comprobación de Redundancia Cíclica de 32 bits, CRC32, es un código de detección de errores ampliamente utilizado para detectar cambios accidentales o errores en los datos durante la transmisión o el almacenamiento. En este proyecto usted realizará una implementación para calcular el CRC32 empleando lenguaje ensamblador para RV32I. Dicha implementación se ejecutará en un sistema en chip (SoC), creado con LiteX, y en el cual se tendrá un _core_ de RISC-V. 

<br/><br>

### Implementación
Para la implementación de su programa, deberá guiarse con código de ejemplo que le es provisto en este repositorio. Deberá crear una archivo en C, `crc32.c` (y su respectivo `crc32.h`) que le permita capturar una palabra o frase de hasta 30 caracteres. Por ejemplo, se podría recibir una entrada como se muestra a continuación. El resultado obtenido se deberá mostrar como se ejemplifica. 

```bash
proy1 > CRC32
Prueba

41dd1b75
```

Como se muestra anteriormente, debe ingresar el texto que se usará como entrada para. Como salida debe indicar el CRC32, en formato hexadecimal. Usted deberá investigar cómo implementar el algoritmo de una forma sencilla ya que lo hará usando un lenguaje de muy bajo nivel (ensamblador de RV32I).

Las funcionalidades que implemente en `crc32.c` solamente serán para la captura y preparación de los datos que se procesarán con el algoritmo que será implementado en lenguaje ensamblador. Dicha función (contenida en `crc32_asm.S`) deberá recibir los parámetros que usted defina como necesarios. Se debe limitar al uso de las instrucciones del ISA RV32I y deberá implementar una forma eficiente. Considere solo utilizar texto de entrada en UTF-8. Deberá investigar la forma en que se implementa el algoritmo comúnmente, considerando que cada vez que su código se ejecute deberá generar todos los valores iniciales necesarios.

<br/><br>

### Resultados
Evalúe su implementación para al menos los siguientes casos. Considere validar los resultados que obtiene de su implementación con otras herramientas existentes en línea (por ejemplo, https://emn178.github.io/online-tools/crc/)

````
Prueba
Sistemas Digitales
Este es texto de prueba
abcdefghijklmnopqrstuvwxyz0123
XYZ123
````

<br/><br>




## Construcción del SoC y del código

Empleando LiteX, usted podrá construir un SoC para ejecutar el código desarrollar. Empleando:

```bash
litex_sim --integrated-main-ram-size=0x10000 --cpu-type=vexriscv --no-compile-gateware
```

podrá crearlo. Como producto de este comando, se producirá una carpeta `build`, la cuál deberemos referenciar al compilar el código.

En la carpeta `proy1` de este repositorio se encuentra el código de referencia a utilizar y modificar. En dicha carpera usted deberá agregar su código fuente, tanto `.c/.h` como `.S`. Además, deberá modificar el `Makefile` para asegurarse de que su código se compile y quede dentro del `.bin`.


```makefile
OBJECTS="helloc.o add_asm.o add.o fir_asm.o fir.o crt0.o main.o"
```

Una vez realizadas las modificaciones necesarias, desde la carpeta `proy1` podrá ejecutar un script de Python que se encargará de disparar la compilación 

```bash
./proy1.py --build-path=../build/sim
```

Para cargar el `.bin` generado y que se ejecute en el SoC, usted deberá ejecutar:

```bash
litex_sim --integrated-main-ram-size=0x10000 --cpu-type=vexriscv --ram-init=./proy1/proy1.bin
```

<br/><br>

### Evaluación
Este laboratorio se evaluará con la siguiente rúbrica


| Rubro | % | C | EP | D | NP |
|-------|---|---|----|---|----|
|`crc32_asm.S` produce el código correcto| 50|   |    |   |    |
|`crc32.c` manipula entrada de texto y despliega resultado |20|   |    |   |    |
|Integración en `main.c`|20|   |    |   |    |
|Uso de repositorio |10|   |    |   |    |

C: Completo,
EP: En progreso ($\times 0,8$),
D: Deficiente ($\times 0,5$),
NP: No presenta ($\times 0$)

_Nota_: El uso del repositorio implica que existan contribuciones de todos los miembros del equipo. El último _commit_ debe registrarse antes de las 23:59 del martes 08 de abril de 2025. Queda prohibida la utilización de código fuente que no haya sido escrito/desarrollado por el equipo de trabajo.
