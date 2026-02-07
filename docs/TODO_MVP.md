# TODO MVP (priorizado)

1. **Integrar assets de Kenney (sprites + UI)**
   - Criterios de aceptación:
     - Sprites reales para jugador, obstáculos y monedas.
     - Carga de assets en preload sin errores.
     - Credits/licencia de Kenney documentados en README.

2. **Loop de juego final (balance y dificultad)**
   - Criterios de aceptación:
     - Curva de dificultad progresiva perceptible cada 10-15s.
     - Parámetros de spawn y velocidad configurables desde constantes.
     - No hay picos injustos en los primeros 15s.

3. **UI de resultados + reinicio**
   - Criterios de aceptación:
     - Pantalla de Game Over con score final y mejor score (localStorage).
     - Reinicio por tap/click o tecla.

4. **Input unificado y accesible**
   - Criterios de aceptación:
     - Tap/click controla izquierda/derecha.
     - Teclas A/D y flechas funcionan.
     - No hay dependencia de mantener presionado en móvil.

5. **Pulido visual mínimo**
   - Criterios de aceptación:
     - Fondo y UI coherentes con el pack de Kenney.
     - Texto legible en desktop y móvil.

6. **PWA-ready (manifest + icons)**
   - Criterios de aceptación:
     - `manifest.webmanifest` válido.
     - Íconos generados desde assets de Kenney.
