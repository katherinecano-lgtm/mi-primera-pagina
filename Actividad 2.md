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
    
    # Dibujo del movimiento hacia la derecha
    print("Tortuga avanzando hacia la derecha...")
    print("→" * pasos)
    
    # Mensaje descriptivo
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
    
    print("Tortuga bajando...")
    for _ in range(pasos):
        print("↓")   # Cada flecha representa un paso hacia abajo

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
pasos_derecha = int(input("¿Cuántos pasos avanza la tortuga hacia la derecha? "))
pasos_abajo = int(input("¿Cuántos pasos avanza la tortuga hacia abajo después de girar? "))

# Tramo horizontal
print("Tortuga avanzando hacia la derecha...")
print("→" * pasos_derecha)

# Tramo vertical (debajo del último símbolo)
print("Tortuga gira 90° a la derecha y baja...")
for _ in range(pasos_abajo):
    # (pasos_derecha - 1) espacios para que la flecha ↓ quede debajo del último →
    print(" " * (pasos_derecha - 1) + "↓")

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
# Posición horizontal acumulada de la tortuga (en número de pasos)
posicion_horizontal = 0

def adelante(n):
    """
    Dibuja el movimiento hacia la derecha (→) por n pasos.
    Usa la posición horizontal acumulada para saber cuántos espacios dejar antes.
    """
    global posicion_horizontal
    # Dibujamos n flechas hacia la derecha, desplazadas según la posición actual
    print(" " * posicion_horizontal + "→" * n)
    posicion_horizontal += n   # Actualizamos la posición horizontal

def abajo(n):
    """
    Dibuja el movimiento hacia abajo (↓) por n pasos,
    manteniendo la columna donde terminó el último adelante().
    """
    global posicion_horizontal
    for _ in range(n):
        # posicion_horizontal - 1 espacios para poner la flecha debajo del último →
        print(" " * (posicion_horizontal - 1) + "↓")

# Ejemplo de uso: debe formar una figura en forma de L
if __name__ == "__main__":
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
posicion_horizontal = 0  # Volvemos a iniciar la posición en 0

def adelante(n):
    global posicion_horizontal
    # Tramo horizontal, desplazado por la posición acumulada
    print(" " * posicion_horizontal + "→" * n)
    posicion_horizontal += n

def abajo(n):
    global posicion_horizontal
    for _ in range(n):
        print(" " * (posicion_horizontal - 1) + "↓")

if __name__ == "__main__":
    print("Tortuga bajando escalones con texto.
")

    # Escalón 1
    adelante(5)
    abajo(2)

    # Escalón 2
    adelante(5)
    abajo(2)

    # Escalón 3
    adelante(5)
    abajo(2)

    print("
La tortuga ha bajado tres escalones.")
```

**Explicación:**  
Se reutilizan las funciones del reto anterior.  
Cada llamada a `adelante(5)` dibuja un tramo horizontal más a la derecha que el anterior gracias a la posición acumulada.  
Luego `abajo(2)` dibuja dos pasos hacia abajo desde el extremo del tramo horizontal.  
Al repetir este patrón se forma una escalera de texto que representa a la tortuga bajando escalones.

---

### Referencias de IA

