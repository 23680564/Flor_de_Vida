# Flor_de_Vida

## Creación de el proyecto FLor de Vida

### Descargar Python y Blender
- Abrir el programa Blender, ir a "archivo" darle en "Generico"

  
  <img width="487" height="154" alt="image" src="https://github.com/user-attachments/assets/232a2b59-4687-4ffe-b29a-02a0a3862962" />

- Una vez se haya creado el archivo, ir a el apartado de Scripts y dar click en el apartado de "Nuevo" y poder generar el proyecto

  <img width="728" height="78" alt="image" src="https://github.com/user-attachments/assets/60ab7000-4603-4919-a66b-dc02035356c7" />

  

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

  ## Codigo completo

 ```
import bpy
import math

# Limpiar escena
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# Parámetros de la figura
radio = 3
angulo_actual = 0
paso_angular = 60  # Cada 60 grados para obtener 6 círculos alrededor

# 1. Círculo Central
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)

# --- INICIO DEL PATRÓN REPETITIVO ---
# Círculo 1 (Manual)
x1 = radio * math.cos(math.radians(angulo_actual))
y1 = radio * math.sin(math.radians(angulo_actual))
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x1, y1, 0), vertices=64)

# Círculo 2 (Manual)
angulo_actual += paso_angular
x2 = radio * math.cos(math.radians(angulo_actual))
y2 = radio * math.sin(math.radians(angulo_actual))
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x2, y2, 0), vertices=64)

# Completar círculos restantes con ciclo WHILE
angulo_actual += paso_angular
while angulo_actual < 360:
    x = radio * math.cos(math.radians(angulo_actual))
    y = radio * math.sin(math.radians(angulo_actual))
    bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x, y, 0), vertices=64)
    angulo_actual += paso_angular
 ```

## Para poder ejecutarlo
- Ir a el icono de **RUN** y darle click

  <img width="29" height="26" alt="image" src="https://github.com/user-attachments/assets/ff007ffa-75ba-49e6-825b-fd827aa0684e" />

  - Despues se mostrara en pantalla la figura que se realizo mediante el codiggo, en este caso lo es la "Flor de Vida"

    <img width="394" height="457" alt="image" src="https://github.com/user-attachments/assets/73abb3bc-6259-4957-a374-45fb56752c1e" />

    - Y asi es como se finaliza el proyecto
   
      **NOTA: Si no llegase a correr o ejecutarse, revisa la identacion**









