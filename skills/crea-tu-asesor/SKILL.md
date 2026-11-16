---
name: crea-tu-asesor
description: >
  Guía paso a paso para destilar el pensamiento de un autor o experto (Jakob Nielsen, una
  autora de research, tu contadora, un abogado) en una base consultable con fuente y fecha
  en cada afirmación, y armar con ella un asesor que responde citando y dice "no sé" cuando
  el material no cubre algo. Disparar ante frases como "quiero un asesor de [autor]",
  "ármame un asesor", "créame un asesor", "quiero consultar a [experto] con sus fuentes",
  "destila los artículos de [autor]", "actúa como [experto] pero con fuentes". Al detectar
  que aplica, confirmar antes de empezar: "¿Armamos tu asesor de [autor]? Primero te voy a
  pedir las fuentes y las preguntas reales que quieres que responda."
---

# Crea tu asesor con fuentes

Si le dices a una IA "actúa como [experto]", te responde con lo que más circula en internet sobre esa persona, que suele ser lo que decía hace diez años. Un asesor armado con este método responde con lo que el autor dice en sus fuentes, **cita de dónde sale cada afirmación y dice "no sé" cuando el material no lo cubre**.

El objetivo no es resumir al autor. Es capturar **cómo razona**: qué exige saber antes de opinar, en qué orden descarta opciones, qué se niega a responder. Así se puede consultar y aplicar a casos propios, con la fuente y la fecha de cada afirmación a la vista.

Sirve para cualquier fuente: un canal de video, un blog, un newsletter, un archivo de artículos o libros que la persona tenga.

---

## Antes de empezar: qué pedirle a la persona

1. **¿De quién es el asesor?** Un autor o experto con material propio suficiente (idealmente 10 piezas o más).
2. **¿Dónde está el material?** Archivos, links o una carpeta. Formato preferido: texto (.md o .txt). Los PDF se convierten a texto antes de destilar.
3. **¿Qué preguntas reales quiere hacerle?** Entre 3 y 5, de su trabajo. Se congelan ahora y sirven de prueba al final.
4. **¿Dónde lo va a usar?** En Claude Code el método corre completo. En claude.ai (Proyectos) o NotebookLM se hace la versión liviana: ver "Versión liviana" al final.

Aclarar una sola vez: **la base es de uso personal.** El material del autor no se publica ni se redistribuye. La base guarda análisis propio y citas cortas con su fuente.

---

## Los cinco principios que mandan sobre todo lo demás

### 1. Congelar lo que la IA ya cree saber, ANTES de leer nada

El riesgo mayor es que el modelo mezcle lo que observó en el material con lo que ya sabía del autor por entrenamiento previo. El resultado sería un autor genérico de internet con una capa fina de citas encima: lo mismo que ya responde cualquier chatbot.

Contramedida, y va primero, antes de la ingesta:

- Escribir un archivo con **todo lo que el modelo cree saber del autor**, fechado y exhaustivo: frameworks, cifras, frases que cree que repite, su supuesto orden de razonamiento.
- Ese archivo queda **en cuarentena**: ningún paso de destilación o consolidación lo puede abrir.
- Al final, un paso distinto, el único autorizado, lo contrasta con el material. Cada creencia previa queda `confirmada` con al menos 2 citas reales, o `descartada`.

**Cómo leer el resultado:** si sobrevive la gran mayoría, NO es buena noticia. Significa que la destilación se guió por lo que se esperaba encontrar. Una tasa alta de descarte es el resultado sano. Lo más informativo son los **confirmados con corrección**: el tema estaba bien y el detalle, mal.

### 2. Todo lleva fuente y ubicación

Cada afirmación de la base lleva el identificador de la pieza y su ubicación exacta (minuto, o fecha y sección). Sin excepción. Es lo que permite auditar después y lo que hace que el asesor pueda decir "esto lo dijo aquí" en vez de "esto suena a él".

### 3. Doble respaldo, contado por tema y no por fuente

Toda afirmación del modelo de razonamiento necesita **2 observaciones independientes o más**. Con una sola, se marca como inferida. Con cero, no entra.

La independencia se cuenta por tema, no por pieza: tres aplicaciones a tres situaciones distintas dentro de una misma pieza valen más que la misma frase repetida en dos piezas.

### 4. No reproducir el material

El material original es **insumo descartable**, no el resultado. Vive en una carpeta `raw/` que no se comparte. La base guarda análisis derivado y citas ancla cortas, con un **tope de 25 palabras**, siempre atribuidas. Ningún archivo de la base contiene texto corrido del original.

### 5. Declarar los huecos en vez de rellenarlos

Cuando el material no cubre algo, se dice. "El material no lo trata" vale más que una extrapolación con tono seguro. El asesor separa visiblemente **lo citado** de **lo extrapolado**: misma voz, distinto estatus.

---

## Las fechas son estructura, no un dato más

Un autor activo cambia de opinión con el tiempo, y muchas veces con razón. **Eso no es un error a corregir: es un hallazgo a registrar.**

- Cada ficha lleva la fecha de la pieza.
- Cuando el autor dice lo contrario en otra pieza, se agrega un campo `contradicho por:` con **las dos fechas**, y se mantienen **las dos fichas**. Fusionarlas obliga a elegir un ganador.
- La dirección del cambio importa: la versión que el autor abandona puede seguir siendo la correcta para alguien en otra situación.

---

## Las capas de la base

1. **`raw/`**: material original, sin compartir, descartable.
2. **`notas/<id>.md`**: una por pieza. Mapa de qué hay adentro y dónde. Es el rastro de auditoría.
3. **`fichas/`**: la unidad depende del autor.
   - Si diagnostica casos concretos: una ficha por caso.
   - Si publica estudios: una ficha por estudio (contexto, método, muestra, hallazgo, recomendación, fecha).
   - Si escribe doctrina: frameworks, heurísticas y analogías.
   **La unidad es la idea, no la pieza**: una pieza puede dar quince fichas.
4. **`INDEX.md`**: mapa compacto que se carga entero en cada consulta. Con un índice cuidado, buscar texto en markdown funciona mejor que una base vectorial y no necesita nada instalado.
5. **`MODELO-RAZONAMIENTO.md`**: la única síntesis. No sale de una pieza: sale de leer todas. Qué exige saber antes de opinar, en qué orden, qué se niega a atender, reglas de voz y limitaciones declaradas.

---

## El validador: lo que vuelve verificable el trabajo del modelo

Destilar es trabajo de un modelo leyendo y escribiendo fichas, normalmente imposible de verificar. Un script corto lo vuelve aprobado o rechazado:

- las secciones obligatorias de cada ficha están presentes;
- la fuente existe y tiene el formato correcto;
- ninguna cita supera el tope de palabras, **en todo el archivo** y no solo en el campo de cita;
- los campos que podrían quedar vacíos tienen un valor explícito.

Cada tanda pasa el validador antes de seguir. Si falla, se arreglan las fichas: **nunca se afloja el validador**.

Detalle técnico real: en las expresiones regulares de cada campo usar `[ \t]*` y no `\s*`. `\s` incluye saltos de línea, así que un campo vacío "se llena" con el texto de la sección siguiente y pasa la validación.

---

## Orden de trabajo

1. **Congelar lo que la IA cree saber** (antes de leer el material).
2. **Ingesta**: reunir el material, limpiarlo y escribir un manifiesto con el estado de cada pieza, para poder retomar.
3. **Piloto con una sola pieza.** Destilarla, mirar las fichas con la persona y recién ahí decidir si el formato sirve. Descubrir que falta un campo cuesta una pieza en vez de cincuenta.
4. **Congelar el formato** al cerrar el piloto. Los huecos que aparezcan después se anotan, no se aplican sobre la marcha.
5. **Destilar por tandas**, guardando avance pieza por pieza.
6. **Control temprano**: medir lo que decide si el proyecto sirve cuando todavía se gastó poco.
7. **Consolidar**: unir fichas repetidas entre piezas y generar el índice.
8. **Sintetizar** el modelo de razonamiento, con doble respaldo.
9. **Contexto de quien consulta**: los datos de su situación, por entrevista y no copiados de documentos viejos.
10. **Armar el asesor** con la plantilla de `plantilla-asesor.md` (en Claude Code, como subagente de solo lectura limitado a su carpeta).
11. **Probarlo** con los tres tests.

---

## Los tres tests

**Auditoría de citas.** Elegir fichas al azar y verificar cada cita contra el material original en su ubicación.

**Aceptación.** Las preguntas reales que la persona congeló al principio. Si la base no las responde con citas reales, la base está mal, por prolija que se vea.

**Reserva.** Apartar dos casos antes de sintetizar y, al final, darle al asesor su contexto para comparar su diagnóstico con el registrado.

⚠️ Apartar el *archivo* de un caso **no aparta el caso**: la consolidación lo cita igual (en el índice, en otras fichas, en el modelo de razonamiento) y la prueba queda contaminada. Para una reserva limpia: destilar un caso nuevo y **no consolidarlo**.

---

## Reglas del asesor final

- Siempre carga: modelo de razonamiento, índice completo y contexto de quien consulta. Después abre entre 3 y 8 fichas según el tema.
- Solo lectura, limitado a su propia carpeta.
- **Contrasta el contexto con lo que el autor exige saber y pregunta solo lo que falta.** Si no falta nada, va directo al diagnóstico.
- Nombra **una** cosa, no cinco.
- Separa lo citado de lo extrapolado en cada respuesta.
- **Traduce el contexto**: si la situación de quien consulta es distinta a la del material, da el mecanismo y su equivalente, nunca la instrucción literal.
- Un punto ciego solo se señala **anclado** a una contradicción concreta o a un caso del material.
- Sabe devolver la pregunta cuando el criterio de quien consulta sobre su propio terreno es mejor que el del autor.
- Dice "no sé" cuando el material no cubre algo.

---

## Versión liviana (claude.ai o NotebookLM)

Si la persona no usa Claude Code:

1. Crear un **Proyecto** en claude.ai y subir los artículos o transcripciones como archivos de texto.
2. Pedir fichas **de un artículo por vez**, con el formato de este método (fuente, fecha, idea, cita de 25 palabras como máximo).
3. Guardar las fichas como archivos del Proyecto y pegar en las instrucciones del Proyecto las "Reglas del asesor final".
4. Si solo quiere consultar un libro, alcanza con NotebookLM.

Es menos riguroso (no hay validador ni cuarentena), pero conserva lo importante: fuente en cada respuesta y "no sé" cuando corresponde.
