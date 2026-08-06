# jigsaw — puzzles cooperativos para dos

Rompecabezas online sin servidor, sin cuentas y sin configuración: quien arma la mesa manda un enlace, y quien lo abre entra directo — teléfono o computadora.

- **`index.html`** — el juego completo (un solo archivo).
- **`redesign.html`** — el documento de diseño del que sale.

## Cómo funciona

- **Piezas reales.** Cada lado son tres curvas de Bézier con los puntos de control del [generador de Manuel Kasten](https://github.com/Draradech/jigsaw); las aristas se generan desde una semilla compartida, así que ambos jugadores cortan piezas idénticas sin transferirlas.
- **Multijugador punto a punto.** WebRTC vía [PeerJS](https://peerjs.com) y su broker público gratuito. No hay backend propio: la partida vive en la pestaña de quien invita, y los movimientos y cursores viajan directo entre navegadores.
- **Imágenes.** Libres de derechos desde [Lorem Picsum](https://picsum.photos), o una imagen propia — que viaja solo por el canal directo entre los dos dispositivos, sin subirse a ningún servidor.
- **Gestos en el teléfono.** Un dedo mueve la pieza (con la pieza elevada sobre el dedo), dos dedos mueven y acercan la mesa, doble toque encuadra.
- **Piezas giradas (opcional).** Doble toque sobre una pieza la gira 90°; solo encajan con la orientación correcta.
- **Pilas propias.** «＋ pila» pone sobre la mesa un área con el nombre que elijas y se arrastra por su rótulo. El sistema nunca clasifica piezas: solo recuerda las pilas que arma cada quien.
- **Chat y actividad.** Chat en la mesa con aviso de no leídos, y un feed que cuenta quién entró y quién encajó qué.
- **Pausa.** Tocar el contador de progreso pausa el tiempo para ambos.
- **Puzzle del día.** La misma imagen para todo el mundo, cada día, derivada de la fecha.
- **Guardado y estadísticas.** Varias partidas guardadas con miniatura, y récords locales: piezas encajadas, resueltos, racha de días y mejor tiempo por tamaño.
- **Privacidad.** «Con enlace» (entra quien lo tenga) o «Solo yo».

## Publicar en GitHub Pages

```bash
git init && git add . && git commit -m "jigsaw cooperativo"
gh repo create jigsaw-online --public --source . --push
gh api repos/{owner}/jigsaw-online/pages -X POST -f 'source[branch]=main' -f 'source[path]=/'
```

En un minuto queda en `https://<tu-usuario>.github.io/jigsaw-online/`. Cualquier hosting estático sirve igual.

## Límites conocidos

- La pestaña de quien invita debe seguir abierta: es donde vive la partida.
- La conexión directa atraviesa la mayoría de las redes domésticas (STUN); en redes muy restrictivas puede no establecerse — no hay servidor TURN porque no hay servidor.
- El broker público de PeerJS a veces tarda unos segundos en conectar.
- Si la imagen propia es muy pesada, la partida se juega igual pero puede no caber en el guardado local.
- Sin servidor no hay mesas públicas ni búsqueda de imágenes por descripción ni ranking global del puzzle del día: cualquier cosa que necesite un directorio compartido queda fuera por diseño.
