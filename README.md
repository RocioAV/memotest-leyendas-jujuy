# 🎃 Memoria Ancestral · Leyendas de Jujuy

Memotest (juego de memoria) con temática de **mitos y leyendas del noroeste argentino**, pensado para Halloween. Un único archivo HTML con todo el CSS y el JavaScript incluidos: sin dependencias, sin build, sin conexión necesaria.

## 🕯️ Cómo jugar

1. Abrí `index.html` en cualquier navegador (doble clic basta).
2. Elegí el modo:
   - **Un Jugador**: contador de intentos y cronómetro.
   - **Dos Jugadores (Local / Turnos)**: ingresás los nombres y cada pareja suma un punto al jugador en turno. Fallar pasa el turno al rival.
3. Volteá dos cartas: si son la misma leyenda, el par queda revelado, suena un brillo místico,
   **una voz en español pronuncia el nombre del personaje** (Web Speech Synthesis API) y, al
   terminar de hablar, entra **el sonido ambiental de terror característico de esa bestia**.
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
- **Secuencia multimedia al acertar un par** (dos efectos en orden, no se pisan):
  1. ✨ un brillo místico breve de feedback;
  2. 🎙️ `speechSynthesis` **nombra a la leyenda** en español (`lang = "es-AR"`, voz española elegida automáticamente);
  3. 👻 **recién cuando termina de hablar** entra el **sonido ambiental de terror** de esa bestia.
- **Un rugido / lamento / crujido por criatura**, sintetizado en vivo con Web Audio API (osciladores, ruido filtrado, vibrato, eco y paneo):

  | Leyenda | Ambiente |
  | --- | --- |
  | La Llorona | lamento que sube y baja, con eco y aliento de agua helada |
  | El Ucumar | rugido sordo y gutural con entrañas temblando |
  | El Pombero | crujidos de ramas + su silbido de aviso |
  | El Duende | risita traviesa con eco de escondite |
  | La Salamanca | rumor de cueva + campana de bronce + susurro |
  | El Familiar | siseo de serpiente y cascabel seco |
  | El Ahogado | corriente fría, burbujas y respiración bajo el agua |
  | La Telesita | destello celeste, luz que titila |

  El juego prefiere siempre el **archivo propio** (`sound/<leyenda>.mp3`, si existe) y usa el
  sintetizado como respaldo: es **audio 100 % local (sin URLs externas)**, no depende de la red,
  no hay problemas de licencia y sigue siendo un único HTML con sus carpetas `img/` y `sound/`.
- Resto de los efectos: volteo, fallo, victoria y clic, también con Web Audio API.
- Botón **🔊 Sonido** para silenciar voz + ambientes en cualquier momento.
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

## 🔊 Sonidos propios de las bestias (opcional)

Además de los ambientes sintetizados, cada leyenda puede tener **su propio archivo de sonido**
en la carpeta **`sound/`**. Si existe, se reproduce **ese** archivo (después de que la voz nombra
a la leyenda); si no, se usa el ambiente sintetizado de la tabla anterior. Mismo esquema que las
imágenes: sondeo automático y respaldo sin tocar el código.

| Leyenda | Nombre de archivo |
| --- | --- |
| La Llorona | `sound/llorona.mp3` (o `.ogg` / `.m4a` / `.wav`) |
| El Ucumar | `sound/ucumar.mp3` |
| El Pombero | `sound/pombero.mp3` |
| El Duende | `sound/duende.mp3` |
| La Salamanca | `sound/salamanca.mp3` |
| El Familiar | `sound/familiar.mp3` |
| El Ahogado | `sound/ahogado.mp3` |
| La Telesita | `sound/telesita.mp3` |

- Extensiones buscadas, en orden: `.mp3` → `.ogg` → `.m4a` → `.wav`.
- También se aceptan otros nombres: `sound/la llorona.mp3`, `sound/el duende.mp3`, etc.
- Podés forzar una ruta exacta con el campo `sound:"ruta/archivo.mp3"` en el array `LEGENDS`.
- Duración ideal: **2 a 4 segundos** (sonido ambiental corto, no música larga).
- El botón 🔊 Sonido corta el archivo al instante, igual que la voz.

## 🚀 Publicar en GitHub Pages

Subí el repo y activá **Settings → Pages → Deploy from a branch → `main` / root**. La juego queda disponible en `https://<usuario>.github.io/<repo>/`.

## 📄 Licencia

Usá y modificá libremente para proyectos personales, educativos o de Halloween. 🎃
