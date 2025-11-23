# Tarea 2 - Ejercicios Unidad 1

En esta entrada presento mis soluciones en Python a los ejercicios de la sección **“Para practicar”** de la Unidad 1 del curso de Pensamiento Algorítmico.  
Cada reto incluye el enunciado, el código en Python y una breve explicación.

---

## Reto 1: simula el comportamiento de la tortuga usando solo `print()` e `input()`.

**Enunciado:**  
Reto 1: simula el comportamiento de la tortuga usando solo `print()` e `input()`.  
Intenta recrear el movimiento de la tortuga únicamente con texto, usando funciones, `print()` e `input()` para pedir valores al usuario.

**Código en Python:**

```python
def avanzar():
    print("Simulación sencilla de la tortuga avanzando.")
    pasos = int(input("¿Cuántos pasos avanza la tortuga? "))

    if pasos <= 0:
        print("La tortuga no se mueve.")
        return
    
    print("Tortuga avanzando hacia la derecha...")
    camino = "-" * (pasos - 1) + "→"
    print(camino)

    print(f"La tortuga avanzó {pasos} pasos hacia la derecha.")

if __name__ == "__main__":
    avanzar()
```

**Explicación:**  
El programa le pide al usuario cuántos pasos avanzará la tortuga. Luego imprime una fila de símbolos `→` que representan el desplazamiento hacia la derecha. Al final muestra un mensaje indicando cuántos pasos avanzó.

---

## Reto 2: Tortuga bajando

**Enunciado:**  
Reto 2: Tortuga bajando.  
Crea el rastro de una tortuga moviéndose hacia abajo usando únicamente `print()` e `input()`.

**Código en Python:**

```python
def bajar():
    print("Simulación de la tortuga bajando.")
    pasos = int(input("¿Cuántos pasos baja la tortuga? "))

    if pasos <= 0:
        print("La tortuga no se mueve.")
        return

    print("Tortuga bajando...")

    for _ in range(pasos - 1):
        print("|")

    print("↓")

    print(f"La tortuga bajó {pasos} pasos hacia abajo.")

if __name__ == "__main__":
    bajar()
```

**Explicación:**  
El programa pide el número de pasos hacia abajo y luego imprime una flecha `↓` por cada paso, formando una columna vertical que representa el movimiento descendente de la tortuga.

---

## Reto 3: Girar y dibujar usando solo `print()` e `input()`

**Enunciado:**  
Reto 3: Girar y dibujar usando solo `print()` e `input()`.  
Ahora la tortuga no solo avanza: también gira. Primero avanza, luego gira 90 grados a la derecha y vuelve a avanzar, de forma que se dibuje una “L”.

**Código en Python:**

```python
print("Simulación de la tortuga formando una 'L' con texto.")

# Distancias antes y después de girar
print("Simulación de la tortuga formando una 'L' con texto.")

pasos_derecha = int(input("¿Cuántos pasos avanza la tortuga hacia la derecha? "))
pasos_abajo = int(input("¿Cuántos pasos avanza la tortuga hacia abajo después de girar? "))

if pasos_derecha <= 0 or pasos_abajo <= 0:
    print("La tortuga no se mueve lo suficiente para dibujar una 'L'.")
else:
    # Tramo horizontal
    print("Tortuga avanzando hacia la derecha...")
    camino_horizontal = "-" * (pasos_derecha - 1) + "→"
    print(camino_horizontal)

    # Tramo vertical, alineado con la punta de la flecha
    print("Tortuga gira 90° a la derecha y baja...")
    columna = pasos_derecha - 1  # posición de la flecha →
    for _ in range(pasos_abajo - 1):
        print(" " * columna + "|")
    print(" " * columna + "↓")

    print("La tortuga ha dibujado una figura en forma de 'L'.")
```

**Explicación:**  
Primero la tortuga avanza hacia la derecha, y esto se muestra con una fila de `→`. Después “gira” y se mueve hacia abajo. Para que la forma parezca una “L”, se imprimen flechas `↓` alineadas debajo del último símbolo `→` usando espacios en blanco.

---

## Reto 4: Encapsula los comportamientos anteriores usando funciones

**Enunciado:**  
Reto 4: Encapsula los comportamientos anteriores usando funciones.  

Reescribe los retos anteriores creando funciones que representen los movimientos de la tortuga solo con texto.  
Usa las siguientes funciones como interfaz:

- `adelante(n)` — Dibuja el movimiento hacia la derecha (→) por *n* pasos.  
- `abajo(n)` — Dibuja el movimiento hacia abajo (↓) por *n* pasos.

Por ejemplo, al ejecutar:

```python
adelante(5)
abajo(3)
```

Debería producir un patrón en forma de L.

**Código en Python:**

```python
# Posición horizontal acumulada de la tortuga
posicion_horizontal = 0


def adelante(n):
    """
    Dibuja el movimiento hacia la derecha por n pasos:
    """
    global posicion_horizontal

    if n <= 0:
        return

    camino = "-" * (n - 1) + "→"
    # Desplazar el camino según la posición actual
    print(" " * posicion_horizontal + camino)
    posicion_horizontal += n


def abajo(n):
    """
    Dibuja el movimiento hacia abajo por n pasos:
    alineadas con la punta actual de la tortuga.
    """
    global posicion_horizontal

    if n <= 0:
        return

    columna = posicion_horizontal - 1  # posición de la punta
    for _ in range(n - 1):
        print(" " * columna + "|")
    print(" " * columna + "↓")


if __name__ == "__main__":
    # Ejemplo: figura en forma de L
    adelante(5)
    abajo(3)
```

**Explicación:**  
Uso una variable global `posicion_horizontal` para recordar cuánto se ha movido la tortuga hacia la derecha.  
- `adelante(n)` imprime una fila de flechas `→` desplazada según la posición acumulada y luego actualiza esa posición.  
- `abajo(n)` imprime flechas `↓` en la misma columna donde terminó el último movimiento horizontal, de forma que el dibujo parezca una figura en forma de “L”.

---

## Reto 5: La tortuga baja las escalas

**Enunciado:**  
Reto 5: La tortuga baja las escalas.  

Ajusta tus funciones para que la tortuga pueda bajar escalones.  
Cada escalón debe conservar la posición horizontal acumulada y dibujar correctamente tanto el tramo horizontal como el vertical.  

Por ejemplo:

```python
# Escalón 1
adelante(5)
abajo(2)

# Escalón 2
adelante(5)
abajo(2)

# Escalón 3
adelante(5)
abajo(2)
```

**Código en Python:**

```python
posicion_horizontal = 0

def adelante(n):
    """
    Tramo horizontal del escalón:
    """
    global posicion_horizontal

    if n <= 0:
        return

    camino = "-" * (n - 1) + "→"
    print(" " * posicion_horizontal + camino)
    posicion_horizontal += n

def abajo(n):
    """
    Tramo vertical del escalón:
    alineadas con la punta actual.
    """
    global posicion_horizontal

    if n <= 0:
        return

    columna = posicion_horizontal - 1
    for _ in range(n - 1):
        print(" " * columna + "|")
    print(" " * columna + "↓")

if __name__ == "__main__":
    print("Tortuga bajando escalones con texto.\n")

    # Escalón 1
    adelante(5)
    abajo(2)

    # Escalón 2
    adelante(5)
    abajo(2)

    # Escalón 3
    adelante(5)
    abajo(2)

    print("\nLa tortuga ha bajado tres escalones.")
```

**Explicación:**  
Se reutilizan las funciones del reto anterior.  
Cada llamada a `adelante(5)` dibuja un tramo horizontal más a la derecha que el anterior gracias a la posición acumulada.  
Luego `abajo(2)` dibuja dos pasos hacia abajo desde el extremo del tramo horizontal.  
Al repetir este patrón se forma una escalera de texto que representa a la tortuga bajando escalones.

---

### Referencias de IA

**ChatGPT:** Asistencia en redacción y formato Markdown para la página personal.  
  [https://chatgpt.com/share/691043dd-54ec-8011-93bc-6e99bc14527c](https://chatgpt.com/share/691043dd-54ec-8011-93bc-6e99bc14527c)

