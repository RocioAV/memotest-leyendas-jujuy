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

## 🖼️ Imágenes de las leyendas (opcional)

Cada leyenda tiene su propia ilustración en la carpeta **`img/`**. Podés reemplazarlas por las tuyas:

| Leyenda | Nombre de archivo |
| --- | --- |
| La Llorona | `img/llorona.jpg` (o `.png` / `.webp` / `.svg`) |
| El Ucumar | `img/ucumar.jpg` |
| El Pombero | `img/pombero.jpg` |
| El Duende | `img/duende.jpg` |
| La Salamanca | `img/salamanca.jpg` |
| El Familiar | `img/familiar.jpg` |
| El Ahogado | `img/ahogado.jpg` |
| La Telesita | `img/telesita.jpg` |

- **Cualquier tamaño y proporción sirve**: cuadradas, apaisadas o verticales. El CSS usa una caja de altura fija con `object-fit: contain`, así la imagen siempre queda **proporcional, centrada y sin deformarse** (cuadradas o rectangulares van perfecto).
- Extensiones buscadas automáticamente, en orden: `.jpg` → `.jpeg` → `.png` → `.webp` → `.svg`.
- También se aceptan otros nombres: `img/la llorona.jpg`, `img/el duende.png`, etc. (probado como segunda opción).
- Podés forzar una ruta exacta agregando el campo `img:"ruta/archivo.jpg"` al personaje dentro del array `LEGENDS`.
- Si **no existe** la imagen, se muestra un respaldo (SVG con la runa y el nombre, o el emoji) para que ninguna carta quede vacía.
- Las imágenes con **fondo blanco o transparente** se ven mejor sobre la carta oscura.

## 🚀 Publicar en GitHub Pages

Subí el repo y activá **Settings → Pages → Deploy from a branch → `main` / root**. La juego queda disponible en `https://<usuario>.github.io/<repo>/`.

## 📄 Licencia

Usá y modificá libremente para proyectos personales, educativos o de Halloween. 🎃
