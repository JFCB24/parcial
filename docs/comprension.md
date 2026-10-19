# Comprensión del diseño — Enunciado C
**Nombre:** Juan Felipe Castellanos Bran
**Fecha:** 19/10/2026

Responde con tus palabras, basándote en `docs/UML-final.md`. Respuestas
concisas (2–4 líneas por pregunta). Evidencia que entendiste el contrato
**antes** de programar.

---

### 1. Herencia y polimorfismo
¿Por qué `Curso` es una clase abstracta y no concreta? Menciona qué método
obliga a cada subclase a implementar y qué gana el sistema con eso.

> _Tu respuesta:Es abstracta porque un curso siempre tiene un tipo específico: obligatorio, electivo o nivelatorio. Obliga a implementar dificultadEsperada(), lo que permite calcular la dificultad de cursos distintos en una misma lista gracias al polimorfismo._

---

### 2. Composición vs. agregación
Explica la diferencia entre `PlanEstudios ◆— Curso` (composición) y
`Facultad ◇— PlanEstudios` (agregación). ¿Qué pasaría con los cursos si se
elimina el plan? ¿Y con los planes si se elimina la facultad?

> _Tu respuesta:En la composición, PlanEstudios crea sus cursos dentro de su constructor. Si el plan deja de existir, sus cursos pierden toda referencia y desaparecen con él. En la agregación, los planes se crean fuera y se registran con agregarPlan(). Si la Facultad desaparece, los planes siguen existiendo porque su ciclo de vida es independiente.._

---

### 3. Asociación
En `Estudiante — Curso`, ¿quién es dueño de quién? ¿Por qué se modela como
N:M y no como composición?

> _Tu respuesta:Ninguno de los dos es dueño del otro. Estudiante solo guarda referencias en su lista inscritos, y los cursos se crean antes; inscribirCurso() no crea el curso. Es N:M porque un estudiante cursa varios cursos y un curso lo cursan varios estudiantes. No es composición porque el curso existe aunque el estudiante no esté inscrito._

---

### 4. Dependencia
¿Por qué `Recomendador` **depende** de `HistorialAcademico` en lugar de
**tenerlo** como atributo? ¿Qué ventaja tiene pasar el servicio como
parámetro?

> _Tu respuesta:Recomendador no guarda HistorialAcademico como atributo: lo recibe en recomendar(). Así no tiene estado propio y queda desacoplado, de modo que el mismo recomendador sirve para cualquier historial. La sección 5 del UML prohíbe guardar el historial como atributo, porque rompería la dependencia._

---

### 5. Listas
En este proyecto se usan dos estructuras distintas:
- `int[] notas` en `Estudiante`
- `ArrayList<Curso>` en `PlanEstudios` y `Estudiante`

Explica por qué en cada caso se eligió esa estructura y no la otra. ¿Qué
pasa si el estudiante intenta registrar más notas que la capacidad del
arreglo?

> _Tu respuesta: Se usa int[] para las notas porque la capacidad es fija y se conoce de antemano. Se usa ArrayList para los cursos porque la cantidad cambia al inscribirse. Si se intenta registrar una nota extra, registrarNota() no la guarda y el contador no aumenta. No hay error ni desbordamiento._