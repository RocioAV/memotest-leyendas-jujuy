# 🎃 Memoria Ancestral · Leyendas de Jujuy

Memotest (juego de memoria) con temática de **mitos y leyendas del noroeste argentino**, pensado para Halloween. Un único archivo HTML con todo el CSS y el JavaScript incluidos: sin dependencias, sin build, sin conexión necesaria.

## 🕯️ Cómo jugar

1. Abrí `index.html` en cualquier navegador (doble clic basta).
2. Elegí el modo:
   - **Un Jugador**: contador de intentos y cronómetro.
   - **Dos Jugadores (Local / Turnos)**: ingresás los nombres y cada pareja suma un punto al jugador en turno. Fallar pasa el turno al rival.
3. Volteá dos cartas: si son la misma leyenda, el par queda revelado, suena un arpegio místico y **una voz en español pronuncia el nombre del personaje** (Web Speech Synthesis API).
4. Descubrí las 8 parejas del tablero 4 × 4 para completar el ritual.

## 👻 Bestiario (las 8 cartas)

| Leyenda | Dominio |
| --- | --- |
| La Llorona | Los ríos |
| El Ucumar | El monte |
| El Pombero | El monte |
| El Duende | Las casas |
| La Salamanca | La cueva |
| El Familiar | La brujería |
| El Ahogado | El río |
| La Telesita | El cielo |

## ✨ Detalles técnicos

- **Modo oscuro** obligatorio: negros/grises profundos, naranja fuego (calabaza), morados místicos y bordes dorados rústicos.
- Animación de volteo **3D flip** con `transform-style: preserve-3d` y `backface-visibility`.
- **Voz nativa**: `window.speechSynthesis` con `lang = "es-AR"` y selección automática de una voz española.
- **Efectos de sonido** sintetizados en tiempo real con Web Audio API (osciladores + ruido filtrado): volteo, fallo, pareja y victoria.
- Indicador visual de turno, marcador por jugador, cronómetro y estadísticas finales.
- Accesibilidad: cartas como botones reales con `aria-label` dinámico, región `aria-live`, foco visible y soporte de `prefers-reduced-motion`.

## 🚀 Publicar en GitHub Pages

Subí el repo y activá **Settings → Pages → Deploy from a branch → `main` / root**. La juego queda disponible en `https://<usuario>.github.io/<repo>/`.

## 📄 Licencia

Usá y modificá libremente para proyectos personales, educativos o de Halloween. 🎃
