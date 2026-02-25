# Flor_de_Vida

## Creacion de el proyecto FLor de Vida

### Importación de librerías

`
import bpy
import math
`

` bpy`

Es la biblioteca de Blender que permite:

- Crear objetos

- Modificar escenas

- Controlar materiales, luces, cámaras, etc.

` math`

Se usa para:

- Funciones trigonométricas (cos, sin)

- Convertir grados a radianes (radians())


### Limpiar la escena
`
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
`
¿Qué hace?

- Selecciona todos los objetos existentes.

- Los elimina.

 Esto asegura que el script empiece desde una escena vacía.

 ## Parámetros principales
 `
radio = 50
angulo_actual = 0
paso_angular = 10
`

`radio`

- Es el radio de cada círculo.

- También determina la distancia desde el centro para posicionarlos.

` angulo_actual`

- Guarda el ángulo actual en grados.

- Empieza en 0°.

`paso_angular`

- Indica cuántos grados avanza cada círculo.

- Aquí está en 10°, así que habrá:

`360 / 10 = 36 círculos alrededor`

## Círculo central
`
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)
`

**¿Qué hace?**

Crea un círculo:

Radio: 50

Ubicación: centro (0,0,0)

64 vértices → se ve suave

Este es el círculo base en el centro.

## Círculo 1 (Manual)
`
x1 = radio * math.cos(math.radians(angulo_actual))
y1 = radio * math.sin(math.radians(angulo_actual))
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x1, y1, 0), vertices=64)
`

**¿Qué está pasando aquí?**

Se usan las fórmulas del círculo:
`
x = r cos(θ)
y = r sin(θ)
`

Como `angulo_actual = 0`:
`
cos(0°) = 1
sin(0°) = 0
`

Entonces:
`
x = 50
y = 0
`

Se crea un círculo en (50, 0, 0).

## Círculo 2 (Manual)
`
angulo_actual += paso_angular
`

Ahora el ángulo pasa a:
`
0 + 10 = 10°
`

Luego:
`
x2 = radio * math.cos(math.radians(angulo_actual))
y2 = radio * math.sin(math.radians(angulo_actual))
`

Se calcula su nueva posición usando trigonometría.

Después se crea el círculo en esa nueva posición.

## Círculos restantes con WHILE
`
angulo_actual += paso_angular
while angulo_actual < 360:
`

Aquí comienza el ciclo automático.

El while repite:

- Calcula posición con cos y sin

- Crea el círculo

- Aumenta el ángulo 10 grados

- Se detiene cuando llega a 360°
