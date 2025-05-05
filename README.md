import time # Importamos el módulo time para pausas (opcional, para simular tiempo)
import random # Importamos random para posible variación en el futuro (no usado en este ejemplo básico, pero útil)

# --- Definición de las variables del juego ---
salud_enemigo = 100  # La salud inicial del objetivo o enemigo
municion_actual = 10 # La munición que tiene el jugador en el cargador actualmente
cargador_max = 10    # La capacidad máxima del cargador
municion_reserva = 30 # La munición que el jugador tiene fuera del cargador
dano_por_disparo = 15 # Cuánto daño hace cada disparo

print("--- ¡Simulación de Disparo Simple! ---")
print(f"Tienes un cargador con {cargador_max} balas y {municion_reserva} en reserva.")
print(f"El objetivo tiene {salud_enemigo} puntos de salud.")

# --- Bucle principal del juego ---
while salud_enemigo > 0:
    print("\n--- Estado Actual ---")
    print(f"Munición en cargador: {municion_actual}/{cargador_max}")
    print(f"Munición en reserva: {municion_reserva}")
    print(f"Salud del objetivo: {salud_enemigo}")

    accion = input("¿Qué quieres hacer? (D = Disparar, R = Recargar, S = Salir): ").upper()

    if accion == 'D':
        # Lógica para disparar
        if municion_actual > 0:
            municion_actual -= 1 # Resta 1 bala del cargador
            salud_enemigo -= dano_por_disparo # Reduce la salud del enemigo
            print(f"¡Disparaste! Quedan {municion_actual} balas en el cargador.")
            if salud_enemigo <= 0:
                 print("¡Has derrotado al objetivo!")
                 break # Sale del bucle si el enemigo es derrotado
        else:
            print("¡Click! No tienes munición en el cargador. ¡Necesitas recargar!")

    elif accion == 'R':
        # Lógica para recargar
        balas_necesarias = cargador_max - municion_actual # Cuántas balas faltan en el cargador
        
        if balas_necesarias == 0:
            print("¡El cargador ya está lleno!")
        elif municion_reserva == 0:
            print("No te queda munición en la reserva para recargar.")
        else:
            balas_a_recargar = min(balas_necesarias, municion_reserva) # Recarga solo las que necesitas o las que tienes
            municion_actual += balas_a_recargar # Añade balas al cargador
            municion_reserva -= balas_a_recargar # Resta balas de la reserva
            print(f"Recargaste {balas_a_recargar} balas. Ahora tienes {municion_actual}/{cargador_max} en el cargador.")

    elif accion == 'S':
        print("Saliendo del juego.")
        break # Sale del bucle y termina el programa

    else:
        print("Acción no válida. Presiona D, R o S.")

    # Opcional: pausa para simular el tiempo entre acciones
    # time.sleep(0.5)

# --- Fin del juego ---
if salud_enemigo <= 0:
     print("\n--- ¡Fin del Juego! ---")
     print("¡Victoria! El objetivo ha sido neutralizado.")
else:
     print("\n--- Fin del Juego ---")
     print("Has decidido salir.")
