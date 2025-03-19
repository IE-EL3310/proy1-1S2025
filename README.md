# Proyecto 1: ???
### EL3310 - Diseño de Sistemas Digitales
### Escuela de Ingeniería Electrónica
### Tecnológico de Costa Rica


### Construcción del SoC y del código

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
|`zeller_asm.S` produce el resultado correcto| 40|   |    |   |    |
|Integración en `main.c`|25|   |    |   |    |
|Funcionamiento en FPGA (video)|25|   |    |   |    |
|Uso de repositorio |10|   |    |   |    |

C: Completo,
EP: En progreso ($\times 0,8$),
D: Deficiente ($\times 0,5$),
NP: No presenta ($\times 0$)

_Nota_: El uso del repositorio implica que existan contribuciones de todos los miembros del equipo. El último _commit_ debe registrarse antes de las 23:59 del sábado 24 de agosto de 2024.
