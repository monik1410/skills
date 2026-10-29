---
name: my-editing-style
description: Estilo de edición personal para videos verticales de formato corto (TikTok, Reels, Shorts, 1080x1920) a partir de charlas frente a cámara grabadas en varias tomas. Úsala siempre que edites, cortes, subtitules, agregues B-roll o mezcles audio de un video de la usuaria; se aplica ENCIMA de /video-use (cortes, transcripción, render) y /hyperframes (animaciones, textos de énfasis). Define ritmo, jump cuts, punch-ins, subtítulos rosados, textos de énfasis, B-roll, look, música/SFX y el gancho de 0–3 s.
---

# Mi estilo de edición

Estilo aprendido de dos Reels de referencia (creador de divulgación en español, 75–92 s, 1080x1920)
y adaptado a las preferencias de la usuaria: **acento rosado**, **varias tomas**, **duración libre**.

Esta skill dice QUÉ debe sentirse y con qué valores. El CÓMO (transcribir, EDL, render, animaciones)
lo resuelven `/video-use` y `/hyperframes`. Sus reglas duras (cortes en límite de palabra,
fades de 30 ms, subtítulos al final de la cadena, confirmar estrategia antes de cortar) siguen vigentes.

## Preferencias fijas de la usuaria

- **Material:** varias tomas. Elegir la mejor toma de cada idea y ordenarlas por lógica, no por orden de grabación.
- **Duración:** libre. La que pida el contenido; no recortar ideas para llegar a un número.
- **Color de acento:** rosado `#FF4FA3` (RGB 255,79,163). Blanco `#FFFFFF` para las palabras secundarias del énfasis.
- **Nada de clips de películas o material con derechos.** El B-roll sale de imágenes/clips generados, stock libre o animaciones propias.
- **Idioma:** español. Subtítulos con ortografía y puntuación completas (¿?, ¡!, tildes).

## 1. Ritmo

- Cambio de imagen (corte, punch-in, B-roll o texto de énfasis) cada **~1,5 s de mediana**; ningún plano estático
  de cámara más de ~4 s en las partes explicativas o de energía.
- **El ritmo sigue la emoción:** partes de energía/explicación 1–3 s por plano; momentos sinceros o el cierre
  pueden sostener planos de 8–15 s sin cortes.
- Los últimos 15–20 s bajan la velocidad: menos B-roll, menos cortes, mirada a cámara.

## 2. Jump cuts

- **Cero pausas.** Ningún silencio > 150 ms en el resultado final. Quitar respiraciones, muletillas
  ("eh", "este", "o sea" de relleno), arranques en falso y repeticiones.
- Padding de corte apretado: **~40 ms antes** de la primera palabra y **~60 ms después** de la última
  (dentro de la ventana 30–200 ms de video-use). Debe sentirse habla continua a ~4 palabras/s.
- Si un jump cut en el mismo plano se nota, taparlo con un punch-in, un cambio de encuadre o un texto de énfasis.

## 3. Zooms y punch-ins

- Alternar **dos tamaños**: plano base (encuadre original) y **punch-in 115–125 %** centrado en la cara
  (cara en el tercio superior, ojos ≈ y 600–700 / 1920).
- Punch-in en: preguntas directas al espectador, remates, palabras clave, y para disimular jump cuts.
  Plano base en: explicaciones y listas.
- Cambiar de tamaño en el corte (punch-in duro), no zooms lentos continuos. Escalar con `scale` + `crop`
  por segmento durante la extracción; nunca dejar ver bordes.
- Opcional, máximo una vez por video: golpe de zoom con desenfoque de movimiento (≈ 6 frames) en el primer frame
  o al entrar a la idea principal.

## 4. Textos en pantalla

### Subtítulos (siempre, ~85–90 % del tiempo en pantalla)
- Color `#FF4FA3`, **sin contorno**, sombra suave (negro 40–50 %, desplazamiento ~3 px) solo para legibilidad.
- Fuente sans bold geométrica: **Inter Bold** (alternativas: Instrument Sans Bold, Plus Jakarta Sans Bold).
  Verificar que la fuente esté instalada/cargada; nunca dejar que caiga a una de reserva.
- Tamaño ≈ 64–70 px de cuerpo sobre 1080x1920. Una sola línea, centrada.
- **2–3 palabras por subtítulo**, ~0,6–0,7 s cada uno; partir en puntuación y pausas; nunca un subtítulo < 0,35 s.
- **Mayúscula solo al inicio de oración** + puntuación completa. Números de lista visibles ("1.- ¿Qué sentiste…").
- **Posición fija:** centro de la línea ≈ **y 1300 / 1920** (68 % del alto), encima de la UI de la app.
- Siguen visibles sobre el B-roll con el mismo estilo.
- Estilo ASS de partida para `render.py` (libass escala desde PlayResY=288 → 1920):

```
FontName=Inter,FontSize=10,Bold=1,
PrimaryColour=&H00A34FFF,OutlineColour=&H00000000,BackColour=&H80000000,
BorderStyle=1,Outline=0,Shadow=1,
Alignment=2,MarginV=90
```
  (ASS usa BGR: `&H00A34FFF` = `#FF4FA3`. Ajustar FontSize/MarginV mirando un frame real: línea centrada en y≈1300.)

### Textos de énfasis (1 cada ~12–15 s, 4–6 por video)
- **Reemplazan** al subtítulo normal durante esa frase (no mostrar ambos).
- Texto gigante **apilado** sobre el pecho (centro, y ≈ 900–1150): 1–2 palabras secundarias en **blanco**
  (~110 px) + la **palabra clave en rosado**, más grande (~150–180 px), extra bold, interlineado apretado.
  Ej.: "también / **vicios**", "no sea / **así**", "tanto tiempo / **evitando**".
- Variante para emociones/listas cortas: todo en blanco con sombra ("frustrado, / cansado.").
- Entrada rápida (pop de escala 0,85→1 en ~5 frames, ease-out), aparece en la palabra hablada, sale en el corte.
  Construir con HyperFrames (WebM con alfa) o PIL; ver `/hyperframes`.
- Elegir las palabras de mayor carga emocional o conceptual de la transcripción, no al azar.

## 5. Gráficos y B-roll

- **Sin emojis, sin pop-ups, sin stickers, sin barras de progreso.** Lo gráfico es solo subtítulos + énfasis.
- **B-roll a pantalla completa** cada ~10–15 s, bloques de 1,5–8 s, que **ilustran literalmente la frase**
  o desarrollan una metáfora como mini historia (personaje recurrente, mismo mundo visual).
  Fuentes: imágenes/clips generados, stock libre de derechos, animaciones HyperFrames.
  Mantener la paleta cálida del video (dorados, naranjas, rosados).
- Usar el **audio de la charla por debajo del B-roll** (L-cut): el B-roll entra y sale en límites de palabra.
- **Objetos en cámara** (accesorios que la usuaria tenga en mano) cuentan como B-roll en vivo; preferir
  cortar a la toma donde el objeto se ve.
- **Blanco y negro** (~2–4 s) solo en el momento de mayor vulnerabilidad del relato; máximo una vez.

## 6. Color y look

- Cálido: piel cálida, negros densos, contraste medio-alto, saturación natural. Nada de teal/orange exagerado.
- Empezar con el auto-grade de `grade.py` y, si hace falta, sumar calidez suave
  (p. ej. `colorbalance=rs=0.04:gs=0.01:bs=-0.04,eq=contrast=1.06:saturation=1.03`). Revisar tonos de piel.
- Misma corrección para todas las tomas para que la mezcla no salte de color.

## 7. Sonido

- **Música de fondo suave y constante** todo el video, **15–20 dB por debajo de la voz**, sin subidas;
  baja (fade 1–2 s) al final con la última frase. Preferir pianos/pads/lo-fi cálidos; ofrecer 2 opciones a la usuaria.
- **SFX escasos (3–5 por video):** solo al entrar a un bloque de B-roll o a un texto de énfasis fuerte
  (whoosh ascendente, brillo tipo "ding"). Nunca en cada corte.
- Voz compresa y pareja (rango ~5–7 LU). Master: loudnorm a **-14 LUFS**, true peak ≤ **-1 dBTP**.
- Medir siempre (`ebur128`) y reportar números; no afirmar que "suena bien".

## 8. El gancho (0–3 s)

- **Habla desde el frame 0.** Sin logo, sin título, sin silencio, sin intro.
- Fórmulas que funcionan (elegir la que permita el material, no inventar frases que no dijo):
  - **Pregunta directa al espectador:** "¿Sabes qué es lo más difícil de…?"
  - **Promesa numerada + tensión:** "Estas son 10 … antes de que…" → cortar a B-roll emotivo a los ~2 s
    con la frase en suspenso.
- **Movimiento inmediato:** gesto grande u objeto en mano, punch-in o B-roll, y 2–3 cambios de imagen en 3 s.
- Si la mejor frase-gancho está en el medio de una toma, **moverla al inicio**.

## Cierre

- Termina en frase de cierre o CTA hablado (p. ej. "…nos vemos en el siguiente post"), sin tarjeta final.
- Mantener ≥ 0,5 s después de la última palabra antes del final.

## Checklist antes de mostrar un preview

1. 0 silencios > 150 ms (`silencedetect=n=-35dB:d=0.15` sobre la pista de voz).
2. Mediana de duración de plano ≈ 1,5–2 s en las partes de energía.
3. Subtítulos rosados `#FF4FA3`, 2–3 palabras, línea en y≈1300, legibles sobre B-roll.
4. 4–6 textos de énfasis, ninguno superpuesto a un subtítulo.
5. Gancho: voz en frame 0 y ≥ 2 cambios de imagen en los primeros 3 s.
6. Audio: -14 LUFS, TP ≤ -1 dBTP, música 15–20 dB bajo la voz, ≤ 5 SFX.
7. Sin material con derechos de autor en el B-roll.
