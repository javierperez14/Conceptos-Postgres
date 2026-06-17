# TALLER TEÓRICO – FUNDAMENTOS DEL MODELO RELACIONAL
## Capítulo 1: Modelo Relacional

---

**Nombre del aprendiz:** Javier Esteban Perez Aldana 
**Fecha de entrega:** 19/06/2026
**Programa:** Análisis y Desarrollo de Software
**Ficha:** 3228973 B
**Trimestre:** Cuarto
**Instructor:** Yeysson Contreras 

---

## ACTIVIDAD 1: COMPRENSIÓN CONCEPTUAL

**1. ¿Qué es el modelo relacional?**

El modelo relacional es básicamente la forma en que se organiza la información dentro de una base de datos. Lo que hace es separar los datos en estructuras llamadas relaciones, que en la práctica uno las ve como tablas con filas y columnas. Este modelo lo propuso un señor llamado Edgar Codd y desde ahí se volvió el estándar para casi todos los sistemas de bases de datos que existen hoy. La idea principal es que los datos no se guardan de manera desordenada sino agrupados por tipo de información, y esos grupos se pueden conectar entre sí. Por ejemplo en un sistema de una tienda, los clientes son una cosa, los productos son otra y los pedidos son otra, pero todo se puede relacionar.

**2. ¿Por qué el modelo relacional organiza los datos en relaciones?**

Porque si uno pusiera toda la información junta en un solo lugar sería un desastre. Imagínese una tabla donde cada vez que un cliente hace un pedido hay que repetir todos sus datos: nombre, dirección, teléfono, otra vez y otra vez. Eso desperdicia espacio y además si el cliente cambia de dirección toca actualizar en mil partes. Al organizar los datos en relaciones separadas, cada información se guarda una sola vez y desde otras tablas simplemente se hace referencia a ella. Eso hace todo más limpio, más fácil de mantener y más confiable.

**3. ¿Cuál es la diferencia entre una relación y una tabla?**

En términos técnicos son diferentes aunque en la práctica se usan casi como sinónimos. La relación es el concepto teórico y matemático que viene del modelo formal de Codd, representa un conjunto de datos con estructura definida. La tabla es la forma en que ese concepto se implementa en un motor de base de datos real como PostgreSQL. O sea, la relación existe en la teoría y la tabla es lo que uno ve y trabaja en el software. En el día a día cuando uno dice "tabla" está hablando de lo mismo que la teoría llama "relación".

**4. ¿Qué es un atributo?**

Un atributo es cada característica o dato que se quiere guardar sobre algo. Por ejemplo si tenemos una tabla de estudiantes, los atributos serían cosas como el número de documento, el nombre, el correo, el teléfono y la fecha en que se registró. Cada atributo es una columna de la tabla. Básicamente define qué información se almacena sobre esa entidad.

**5. ¿Qué es una tupla?**

Una tupla es un registro completo dentro de una tabla, o sea una fila. Si la tabla es de estudiantes, cada estudiante que se registra es una tupla. Esa fila tiene un valor para cada atributo que tenga la tabla: el documento del estudiante, su nombre, su correo, etc. Todo eso junto forma una tupla.

**6. ¿Qué es un dominio?**

El dominio es el conjunto de valores que puede tener un atributo. Define qué tipo de dato y qué valores son aceptables para ese campo. Por ejemplo el atributo "edad" tiene un dominio de números enteros positivos, no puede ser texto ni un número negativo. El atributo "estado de una cuenta" podría tener un dominio de solo tres valores posibles: activo, inactivo o suspendido. El dominio pone límites a lo que se puede ingresar en cada campo.

**7. ¿Por qué es importante definir dominios para los atributos?**

Porque sin dominios cualquier cosa podría entrar en cualquier campo y los datos perderían sentido. Si el campo "fecha de nacimiento" no tiene dominio definido, alguien podría escribir "mañana" o el número 99999 y el sistema lo aceptaría sin problema. Con dominios bien definidos el sistema valida automáticamente que lo que se ingresa tiene sentido para ese campo. Eso evita errores y garantiza que los datos sean consistentes y confiables desde el momento en que se ingresan.

**8. ¿Qué problemas pueden aparecer si una tabla no tiene clave primaria?**

Sin clave primaria no hay forma de asegurarse de que los registros sean únicos. Podrían quedar filas duplicadas con exactamente la misma información y el sistema no sabría cuál es cuál. Además otras tablas no podrían relacionarse con esa tabla porque no habría un identificador claro al que apuntar. Por ejemplo si en una tabla de clientes no hay clave primaria y se registran dos personas con el mismo nombre, cuando se intente crear un pedido para "Juan García" el sistema no sabría a cuál de los dos se refiere.

**9. ¿Por qué una clave primaria no debe repetirse?**

Porque su función es identificar de forma única cada registro. Si se repite deja de identificar algo de forma única y se pierde todo el propósito de tenerla. Es como si en un país dos personas tuvieran la misma cédula: habría un caos total porque ningún sistema podría saber con certeza a cuál de las dos se está haciendo referencia. Lo mismo pasa en una base de datos: si la clave primaria se repite, cualquier operación que dependa de ese identificador podría afectar al registro equivocado.

**10. ¿Qué significa que una clave primaria no pueda ser nula?**

Significa que todo registro debe tener sí o sí un valor en ese campo. Un nulo en la clave primaria sería como un registro sin identidad, y eso no tiene sentido porque si no sabemos quién es el registro, no podemos hacer nada con él ni relacionarlo con nada. Por ejemplo si se guarda un estudiante sin ningún identificador, no hay forma de saber de quién son las matrículas, las notas o cualquier otro dato relacionado. La clave primaria vacía hace que el registro sea básicamente inútil dentro del sistema.

---

## ACTIVIDAD 2: ANÁLISIS DE ENTIDADES

### CASO 1: Sistema académico

**1. ¿Qué relaciones identifica en el caso?**

Identifico tres relaciones:
- **Estudiantes**: guarda la información personal de cada estudiante.
- **Cursos**: guarda la información de cada curso que ofrece la institución.
- **Matrículas**: es la relación que conecta a los estudiantes con los cursos, registrando cada inscripción.

**2. ¿Qué atributos podría tener la relación Estudiantes?**

- id_estudiante (clave primaria)
- numero_documento
- nombres
- apellidos
- correo_electronico
- telefono
- fecha_nacimiento
- fecha_registro
- estado

**3. ¿Qué atributos podría tener la relación Cursos?**

- id_curso (clave primaria)
- nombre_curso
- descripcion
- duracion_horas
- nivel
- fecha_inicio
- fecha_fin
- estado

**4. ¿Qué atributos podría tener la relación Matrículas?**

- id_matricula (clave primaria)
- id_estudiante (clave foránea)
- id_curso (clave foránea)
- fecha_matricula
- estado_matricula
- nota_final

**5. ¿Cuál podría ser la clave primaria de Estudiantes?**

El **id_estudiante**, que sería un número único generado automáticamente por el sistema para cada estudiante registrado. También podría usarse el número de documento pero el id_estudiante es más seguro porque es generado internamente y no depende de datos externos que puedan cambiar o tener errores.

**6. ¿Cuál podría ser la clave primaria de Cursos?**

El **id_curso**, un identificador único para cada curso. Esto permite que existan cursos con nombres parecidos o que el mismo curso se ofrezca en diferentes períodos sin que se confundan.

**7. ¿Cuál podría ser la clave primaria de Matrículas?**

El **id_matricula**, un número único para cada registro de matrícula. También se podría usar la combinación de id_estudiante e id_curso como clave compuesta, asumiendo que un estudiante no puede matricularse dos veces en el mismo curso.

**8. ¿Qué claves foráneas podrían existir?**

En la tabla Matrículas:
- `id_estudiante` sería clave foránea que apunta a la tabla Estudiantes.
- `id_curso` sería clave foránea que apunta a la tabla Cursos.

**9. ¿Por qué se necesita una relación Matrículas?**

Porque la relación entre estudiantes y cursos es de muchos a muchos: un estudiante puede tomar varios cursos y un curso puede tener muchos estudiantes. Ese tipo de relación no se puede representar directamente entre dos tablas sin una tabla intermedia. La tabla Matrículas resuelve eso y además permite guardar información propia de la inscripción como la fecha o la nota final, datos que no pertenecen ni al estudiante ni al curso sino al vínculo entre los dos.

**10. ¿Qué problema aparecería si se registran los cursos directamente dentro de la relación Estudiantes?**

Habría redundancia masiva. Si un curso tiene 40 estudiantes, toda la información de ese curso (nombre, duración, fechas) se repetiría 40 veces. Si hay que cambiar el nombre del curso toca actualizar 40 filas en lugar de una. Además, si un estudiante toma tres cursos, no habría forma limpia de representar eso en una sola fila sin empezar a agregar columnas como curso1, curso2, curso3, lo cual es un diseño terrible. Todo eso se evita teniendo las tablas separadas y conectadas correctamente.

---

### CASO 2: Sistema de biblioteca

**1. ¿Qué relaciones identifica?**

Identifico cuatro relaciones:
- **Libros**: información de cada libro que tiene la biblioteca.
- **Autores**: información de los autores de los libros.
- **Usuarios**: información de las personas registradas que pueden hacer préstamos.
- **Préstamos**: registra cada vez que un usuario lleva un libro prestado.

**2. ¿Qué atributos tendría la relación Libros?**

- id_libro (clave primaria)
- titulo
- isbn
- id_autor (clave foránea)
- editorial
- anio_publicacion
- genero
- ejemplares_disponibles

**3. ¿Qué atributos tendría la relación Usuarios?**

- id_usuario (clave primaria)
- numero_documento
- nombre_completo
- correo_electronico
- telefono
- fecha_registro
- estado

**4. ¿Qué atributos tendría la relación Préstamos?**

- id_prestamo (clave primaria)
- id_usuario (clave foránea)
- id_libro (clave foránea)
- fecha_prestamo
- fecha_devolucion_esperada
- fecha_devolucion_real
- estado_prestamo

**5. ¿Qué clave primaria podría tener cada relación?**

- Libros: id_libro
- Autores: id_autor
- Usuarios: id_usuario
- Préstamos: id_prestamo

**6. ¿Qué claves foráneas serían necesarias?**

- En Libros: `id_autor` apunta a la tabla Autores.
- En Préstamos: `id_usuario` apunta a la tabla Usuarios.
- En Préstamos: `id_libro` apunta a la tabla Libros.

**7. ¿Por qué no sería recomendable guardar todos los préstamos dentro de la tabla Usuarios?**

Porque un usuario puede hacer muchos préstamos a lo largo del tiempo y no hay forma de meter todos esos registros dentro de una sola fila de la tabla Usuarios. La tabla tendría que crecer horizontalmente de forma indefinida o se tendrían que duplicar filas del usuario, lo cual rompe toda la lógica relacional. Además la información del préstamo (qué libro, cuándo, cuándo se devolvió) no le pertenece al usuario, le pertenece al acto del préstamo. Mezclar todo en la misma tabla genera confusión y hace el sistema muy difícil de consultar y mantener.

**8. ¿Qué reglas deberían existir para evitar préstamos inválidos?**

- No se puede registrar un préstamo para un usuario que no existe en la base de datos.
- No se puede registrar un préstamo de un libro que no existe.
- No se puede prestar un libro que no tiene ejemplares disponibles.
- La fecha de devolución esperada debe ser posterior a la fecha del préstamo.
- Un préstamo debe tener siempre un usuario y un libro asociado, no puede quedar ninguno de esos campos vacío.

---

## ACTIVIDAD 3: CLAVES PRIMARIAS Y CLAVES FORÁNEAS

**1. "Una clave primaria puede repetirse si dos personas tienen el mismo nombre."**
**INCORRECTA.** El nombre no es la clave primaria. La clave primaria es un atributo diseñado específicamente para identificar de forma única cada registro, como un ID generado por el sistema. Que dos personas tengan el mismo nombre es algo completamente normal y no afecta para nada la clave primaria. Si la clave primaria fuera el nombre sí habría problema, pero precisamente por eso no se usa el nombre como clave primaria.

**2. "Una tabla puede tener varias claves primarias al mismo tiempo."**
**INCORRECTA.** Una tabla solo puede tener una clave primaria. Lo que sí puede pasar es que esa clave primaria sea compuesta, es decir que esté formada por varios atributos juntos. Pero sigue siendo una sola clave primaria, no varias. Definir dos claves primarias separadas en una misma tabla no es posible en el modelo relacional.

**3. "Una clave primaria puede estar formada por más de un atributo."**
**CORRECTA.** Eso se llama clave primaria compuesta. Por ejemplo en una tabla de matrículas donde no se quiere crear un id_matricula, se podría usar la combinación de id_estudiante e id_curso como clave primaria, porque esa combinación sí sería única: el mismo estudiante no puede matricularse dos veces en el mismo curso. Cada campo por separado se puede repetir pero juntos forman un identificador único.

**4. "Una clave foránea permite relacionar una tabla con otra."**
**CORRECTA.** Esa es exactamente su función. Al poner en una tabla el identificador de un registro de otra tabla, se crea el vínculo entre las dos. Por ejemplo, poner id_estudiante en la tabla Matrículas relaciona cada matrícula con un estudiante específico de la tabla Estudiantes.

**5. "Una clave foránea siempre debe apuntar a un dato válido en otra tabla."**
**CORRECTA.** Esto es parte de la integridad referencial. Si una clave foránea tiene un valor que no existe como clave primaria en la tabla referenciada, ese dato es inválido y el sistema debería rechazarlo. No puede haber una matrícula con un id_estudiante que no corresponda a ningún estudiante real en la base de datos.

**6. "La clave primaria sirve para identificar de manera única cada registro."**
**CORRECTA.** Esa es su función principal y la razón de su existencia. Gracias a la clave primaria el sistema puede distinguir un registro de otro aunque tengan datos similares, y otras tablas pueden hacer referencia a registros específicos de forma segura.

**7. "Una clave foránea y una clave primaria cumplen exactamente la misma función."**
**INCORRECTA.** Tienen funciones distintas aunque estén relacionadas. La clave primaria identifica registros dentro de su propia tabla. La clave foránea referencia la clave primaria de otra tabla para crear una relación entre las dos. La primaria define identidad, la foránea define conexión. No son lo mismo aunque trabajen juntas.

**8. "Una tabla de matrículas puede tener claves foráneas hacia estudiantes y cursos."**
**CORRECTA.** De hecho así es exactamente como funciona. La tabla Matrículas necesita saber a qué estudiante y a qué curso corresponde cada registro, entonces tiene id_estudiante como clave foránea hacia Estudiantes e id_curso como clave foránea hacia Cursos. Es el ejemplo más clásico de claves foráneas múltiples en una tabla.

**9. "Una clave primaria debería aceptar valores nulos."**
**INCORRECTA.** La clave primaria nunca puede ser nula. Si un registro no tiene valor en su clave primaria no tiene identidad, y sin identidad no se puede gestionar ese registro de ninguna forma. Es una regla básica del modelo relacional: la clave primaria siempre debe tener un valor definido.

**10. "Una clave foránea ayuda a mantener la integridad referencial."**
**CORRECTA.** La clave foránea es precisamente el mecanismo que hace posible la integridad referencial. Al exigir que sus valores existan en la tabla referenciada, evita que se creen relaciones inválidas entre tablas. Sin claves foráneas no habría forma de controlar automáticamente que las relaciones entre tablas sean coherentes.

---

## ACTIVIDAD 4: INTEGRIDAD REFERENCIAL

### Situación 1: Se registra una matrícula para un estudiante cuyo código no existe en la tabla Estudiantes.

**1. ¿Qué problema se presenta?**

Se presenta una violación de integridad referencial. La tabla Matrículas tiene una clave foránea que debe apuntar a un estudiante existente, pero el código ingresado no existe en la tabla Estudiantes. Esto crea lo que se llama un registro huérfano: una matrícula que dice pertenecer a alguien que no está registrado en el sistema. El dato no tiene sentido y contamina la base de datos.

**2. ¿Qué regla debería impedir esta situación?**

La restricción de integridad referencial sobre la clave foránea. Esta regla le dice al sistema que antes de aceptar un nuevo registro en Matrículas, debe verificar que el id_estudiante que se está ingresando sí exista como clave primaria en la tabla Estudiantes. Si no existe, el sistema debe rechazar el registro y no guardarlo.

**3. ¿Qué consecuencias tendría permitir este dato?**

La matrícula quedaría guardada pero sin un estudiante real al que pertenezca. Cualquier reporte que intente cruzar esa matrícula con los datos del estudiante no encontraría nada. Las estadísticas de matriculados estarían infladas con registros falsos. Si el sistema genera certificados o notas basándose en esas matrículas, habría información generada para un estudiante que no existe. Con el tiempo esos registros basura se acumulan y hacen el sistema cada vez menos confiable.

---

### Situación 2: Se elimina un curso que ya tiene estudiantes matriculados.

**1. ¿Qué podría ocurrir con las matrículas asociadas?**

Si el sistema permite la eliminación sin ningún control, las matrículas que tienen ese id_curso quedarían apuntando a un curso que ya no existe. Se convertirían en registros huérfanos igual que en la situación anterior. Hay matrículas registradas pero el curso al que pertenecen desapareció, entonces esos registros no tienen contexto válido.

**2. ¿Qué opciones podría tener el sistema antes de permitir la eliminación?**

El sistema podría:
- **Bloquear la eliminación** mientras existan matrículas activas asociadas a ese curso, que es la opción más segura para un sistema académico.
- **Eliminar en cascada** todas las matrículas relacionadas automáticamente, aunque esto es peligroso porque borra información sin que el usuario necesariamente lo sepa.
- **Poner en nulo** el id_curso en las matrículas afectadas, si la regla lo permite, para indicar que el curso fue eliminado.

La opción más recomendable es bloquear la eliminación y exigirle al usuario que primero cancele o reasigne las matrículas existentes.

**3. ¿Por qué esta situación debe controlarse?**

Porque los estudiantes matriculados en ese curso tienen derechos adquiridos. Si el curso simplemente desaparece de la base de datos sin control, se pierde el historial de quién estaba inscrito, las notas registradas, los pagos realizados y cualquier otra información relacionada. Eso puede tener consecuencias no solo técnicas sino también legales o disciplinarias para la institución.

---

### Situación 3: Se cambia el identificador de un estudiante que ya tiene matrículas registradas.

**1. ¿Qué podría pasar con las relaciones existentes?**

Todas las matrículas que tenían el ID anterior del estudiante quedarían apuntando a un ID que ya no existe. El estudiante tiene un ID nuevo pero sus matrículas siguen referenciando el viejo, que fue eliminado. El historial académico del estudiante básicamente se rompe porque las matrículas quedan huérfanas.

**2. ¿Qué debería hacer el sistema para conservar la consistencia?**

Debería aplicar una actualización en cascada: cuando se cambia la clave primaria de un estudiante, automáticamente se actualiza ese mismo valor en todos los registros de otras tablas que lo referencian como clave foránea. De esa manera las matrículas, notas y demás registros siguen apuntando al estudiante correcto aunque su ID haya cambiado. Otra opción es que el sistema directamente no permita modificar la clave primaria si hay registros relacionados.

**3. ¿Por qué no es recomendable modificar sin control una clave primaria?**

Porque la clave primaria es la base sobre la que se construyen todas las relaciones del sistema. Cambiarla sin control rompe todas esas conexiones de golpe. Además si el sistema tiene integraciones con otros sistemas externos que usan ese ID (plataformas de pago, sistemas de notas, portales web) esos también quedarían desactualizados. Por eso lo más recomendable es que las claves primarias sean valores generados automáticamente por el sistema que nunca necesiten cambiarse, no datos que dependen de información externa.

---

## ACTIVIDAD 5: ÍNDICES DESDE LA TEORÍA

**1. ¿Qué es un índice en una base de datos?**

Un índice es una estructura adicional que se crea sobre uno o varios campos de una tabla para que las búsquedas sean más rápidas. No cambia los datos que hay en la tabla, solo crea una especie de guía de referencia que le permite al sistema encontrar registros sin tener que revisar toda la tabla de arriba a abajo.

**2. ¿Por qué un índice puede mejorar la búsqueda de información?**

Porque sin índice, cuando el sistema busca un registro tiene que revisar cada fila de la tabla una por una hasta encontrar lo que necesita. Si la tabla tiene un millón de registros eso puede tardar mucho. Con un índice el sistema puede ir directamente al registro que busca sin revisar todo, lo que reduce enormemente el tiempo de respuesta. Es la diferencia entre buscar un nombre en una guía telefónica que está ordenada alfabéticamente versus buscar en una lista desordenada.

**3. ¿Qué similitud existe entre un índice de base de datos y el índice de un libro?**

El índice de un libro tiene los temas ordenados con el número de página donde están, entonces uno puede ir directamente a la página que necesita sin leer el libro completo. El índice de una base de datos hace lo mismo: tiene los valores de un campo ordenados con la referencia a dónde está ese registro, entonces el sistema puede ir directo al dato sin recorrer toda la tabla. En los dos casos el índice es una guía que ahorra tiempo.

**4. ¿Qué diferencia hay entre un índice simple y un índice compuesto?**

El índice simple se crea sobre un solo campo, por ejemplo un índice sobre el correo electrónico para buscar usuarios por correo rápidamente. El índice compuesto se crea sobre dos o más campos al mismo tiempo, por ejemplo un índice sobre id_estudiante e id_curso juntos en la tabla Matrículas para acelerar consultas que filtren por los dos campos a la vez. El índice compuesto es útil cuando las búsquedas frecuentes siempre usan esa combinación de campos.

**5. ¿Qué es un índice único?**

Es un índice que además de acelerar búsquedas impide que se repitan valores en el campo indexado. Funciona como una restricción de unicidad. Por ejemplo si se crea un índice único sobre el correo electrónico de los usuarios, el sistema no permitirá registrar dos usuarios con el mismo correo. Es útil para campos que deben ser únicos pero que no son la clave primaria.

**6. ¿Por qué una clave primaria normalmente tiene un índice asociado?**

Porque la clave primaria es el campo más consultado en todo el sistema. Cada vez que otra tabla hace referencia a un registro mediante clave foránea, el motor debe buscar ese valor en la tabla referenciada. Si no hubiera índice sobre la clave primaria, cada una de esas verificaciones sería una búsqueda lenta sobre toda la tabla. Por eso los motores de base de datos crean automáticamente un índice cuando se define una clave primaria.

**7. ¿En qué casos podría ser útil crear un índice sobre el correo de un estudiante?**

Sería útil si el sistema constantemente necesita buscar estudiantes por su correo, por ejemplo cuando el estudiante inicia sesión, cuando se verifica si un correo ya está registrado antes de crear una cuenta nueva, o cuando se envían notificaciones masivas por correo. Si esas operaciones se hacen muchas veces al día, tener un índice sobre ese campo mejora notablemente el rendimiento del sistema.

**8. ¿Por qué no todos los atributos deberían tener índices?**

Porque los índices tienen un costo. Ocupan espacio en disco y cada vez que se inserta, actualiza o elimina un registro, el motor también tiene que actualizar todos los índices de esa tabla. Si hay demasiados índices, las operaciones de escritura se vuelven más lentas. Hay que crear índices solo sobre los campos que realmente se consultan con frecuencia, no sobre todos porque sí.

**9. ¿Qué relación existe entre índices y rendimiento?**

Los índices mejoran el rendimiento de las lecturas y búsquedas pero pueden afectar negativamente el rendimiento de las escrituras. En un sistema que lee mucho y escribe poco, como un sistema de reportes, tener más índices es beneficioso. En un sistema que escribe constantemente, como un sistema de registro de transacciones en tiempo real, demasiados índices pueden volverse un problema. El balance entre cuántos índices tener depende de cómo se usa el sistema.

**10. ¿Un índice cambia los datos almacenados o solo ayuda a encontrarlos más rápido?**

Solo ayuda a encontrarlos más rápido. Los datos originales en la tabla no se tocan para nada cuando se crea un índice. El índice es una estructura separada que funciona como una guía de referencia. Si se elimina el índice los datos siguen ahí intactos, simplemente las búsquedas sobre ese campo vuelven a ser más lentas. El índice no modifica, no mueve ni altera los datos de ninguna forma.

---

## ACTIVIDAD 6: MAPA CONCEPTUAL

```
                    ┌──────────────────────────────┐
                    │       MODELO RELACIONAL       │
                    │    (propuesto por E. Codd)    │
                    └──────────────┬───────────────┘
                                   │
                  organiza la información en
                                   │
                    ┌──────────────▼───────────────┐
                    │           RELACIÓN            │
                    │   (estructura teórica formal) │
                    └──────────────┬───────────────┘
                                   │
               en la práctica se representa como
                                   │
                    ┌──────────────▼───────────────┐
                    │            TABLA              │
                    │   (implementación concreta)   │
                    └────────┬──────────────┬──────┘
                             │              │
                    formada por          formada por
                             │              │
              ┌──────────────▼──┐    ┌──────▼──────────────┐
              │    ATRIBUTOS    │    │       TUPLAS         │
              │   (columnas)    │    │       (filas)        │
              └───────┬─────────┘    └─────────────────────┘
                      │
           cada atributo tiene definido un
                      │
              ┌───────▼─────────┐
              │     DOMINIO     │
              │ (valores válidos│
              │  para ese campo)│
              └─────────────────┘


         MECANISMOS DE IDENTIFICACIÓN Y RELACIÓN
         ─────────────────────────────────────────

    ┌─────────────────────────┐      ┌──────────────────────────┐
    │     CLAVE PRIMARIA      │      │      CLAVE FORÁNEA       │
    │                         │      │                          │
    │ identifica de forma     │      │ conecta una tabla con    │
    │ única cada tupla        │      │ otra tabla               │
    │                         │      │                          │
    │ - no se repite          │      │ apunta a la clave        │
    │ - no puede ser nula     │      │ primaria de otra         │
    │ - puede ser compuesta   │      │ relación                 │
    └─────────────────────────┘      └─────────────┬────────────┘
                                                   │
                                    hace posible y garantiza
                                                   │
                                   ┌───────────────▼────────────┐
                                   │    INTEGRIDAD REFERENCIAL  │
                                   │                            │
                                   │ - evita registros          │
                                   │   huérfanos                │
                                   │ - garantiza que las        │
                                   │   relaciones entre         │
                                   │   tablas sean válidas      │
                                   │ - protege la consistencia  │
                                   │   de los datos             │
                                   └────────────────────────────┘


         ESTRUCTURAS DE BÚSQUEDA
         ─────────────────────────────────────────

                    ┌──────────────────────────────┐
                    │           ÍNDICE             │
                    │                              │
                    │ acelera búsquedas sin        │
                    │ modificar los datos          │
                    │ (como el índice de un libro) │
                    └──────────┬───────────────────┘
                               │
              se clasifica en tres tipos básicos
                               │
        ┌──────────────────────┼─────────────────────┐
        │                      │                      │
┌───────▼────────┐  ┌──────────▼─────────┐  ┌────────▼──────────┐
│ ÍNDICE SIMPLE  │  │  ÍNDICE COMPUESTO  │  │  ÍNDICE ÚNICO     │
│                │  │                    │  │                   │
│ sobre un solo  │  │ sobre dos o más    │  │ no permite        │
│ atributo       │  │ atributos a la vez │  │ valores repetidos │
└────────────────┘  └────────────────────┘  └───────────────────┘

        La CLAVE PRIMARIA tiene siempre un índice
        asociado automáticamente para que las
        búsquedas y verificaciones de integridad
        referencial sean eficientes.
```

**Frases de conexión del mapa:**

- "El modelo relacional organiza la información en relaciones."
- "Una relación se representa en la práctica como una tabla."
- "Una tabla está formada por atributos (columnas) y tuplas (filas)."
- "Cada atributo tiene un dominio que define qué valores son válidos."
- "La clave primaria identifica de forma única cada tupla dentro de una tabla."
- "La clave foránea conecta una tabla con otra apuntando a su clave primaria."
- "La clave foránea hace posible la integridad referencial."
- "La integridad referencial garantiza que las relaciones entre tablas sean válidas y consistentes."
- "Un índice acelera las búsquedas sin modificar los datos almacenados."
- "Los índices pueden ser simples, compuestos o únicos según los campos que cubren."
- "La clave primaria siempre tiene un índice asociado automáticamente."

---

## ACTIVIDAD 7: PREGUNTAS DE ANÁLISIS CRÍTICO

**1. ¿Por qué el modelo relacional sigue siendo importante en los sistemas actuales?**

Porque la gran mayoría de sistemas que usamos en el día a día están construidos sobre bases de datos relacionales: los bancos, los hospitales, los colegios, las plataformas de e-commerce, los sistemas del gobierno. El modelo relacional lleva décadas funcionando y probándose en escenarios reales, lo cual genera confianza. Además hay una cantidad enorme de herramientas, documentación y profesionales capacitados en este modelo, lo que hace que sea la opción natural para la mayoría de proyectos. No es que no haya alternativas, pero para datos estructurados el modelo relacional sigue siendo muy difícil de superar.

**2. ¿Qué ventajas tiene organizar la información en tablas relacionadas?**

La principal ventaja es que cada dato se guarda una sola vez. Si un cliente cambia su dirección, se actualiza en un solo lugar y eso se refleja en todos los pedidos, facturas y registros relacionados. También hace más fácil hacer consultas cruzadas: puedo saber cuántos pedidos hizo un cliente específico, qué productos vendí más en un mes, cuántos estudiantes están activos en un curso. Eso sería muy difícil de hacer si todo estuviera mezclado. Las tablas relacionadas también hacen el sistema más fácil de modificar porque los cambios en una tabla no necesariamente afectan a las otras.

**3. ¿Qué riesgos existen cuando se almacena información duplicada?**

El riesgo más grande es la inconsistencia. Si el mismo dato está guardado en varios lugares y se actualiza en uno pero no en todos, quedan versiones contradictorias de la misma información. Por ejemplo si la dirección de un proveedor está duplicada en diez tablas diferentes y solo se actualiza en tres, el sistema tiene siete copias desactualizadas. Eso puede llevar a enviar facturas a la dirección equivocada, hacer reportes con datos incorrectos o tomar decisiones basadas en información falsa. Además la duplicación desperdicia espacio de almacenamiento innecesariamente.

**4. ¿Por qué las reglas de integridad son necesarias en una base de datos?**

Porque los datos sin reglas son vulnerables a cualquier error. Un empleado que ingresa datos manualmente puede equivocarse, un programa con un bug puede enviar valores incorrectos, o simplemente puede surgir una situación que no se previó. Las reglas de integridad actúan como una red de seguridad que atrapa esos errores antes de que los datos incorrectos queden guardados. Sin esas reglas la base de datos se va llenando poco a poco de datos inconsistentes y eventualmente deja de ser confiable. La integridad no es un lujo, es una necesidad.

**5. ¿Qué podría ocurrir en una empresa si sus datos no tienen consistencia?**

Podrían pasar cosas bastante graves. El área contable podría tener cifras distintas a las del área de ventas para el mismo período. Se podrían generar facturas duplicadas o enviar pedidos a clientes equivocados. Los reportes para la gerencia mostrarían información incorrecta y las decisiones estratégicas se basarían en datos que no reflejan la realidad. En casos extremos esto puede causar pérdidas económicas importantes, demandas legales o pérdida de clientes. La confiabilidad de los datos es fundamental para que una empresa funcione bien.

**6. ¿Por qué no basta con guardar datos, sino que también es necesario controlarlos?**

Guardar datos sin control es como tener una bodega donde se mete todo sin organización. Al principio parece que funciona pero cuando se necesita encontrar algo específico el caos es total. Los datos necesitan ser validados cuando entran, relacionados correctamente con otros datos, protegidos de modificaciones accidentales y organizados para que se puedan consultar eficientemente. Sin ese control los datos almacenados pueden ser incorrectos, inconsistentes o simplemente inútiles porque nadie puede confiar en ellos.

**7. ¿Qué diferencia hay entre almacenar datos y diseñar correctamente una base de datos?**

Almacenar datos es simplemente guardar información en algún formato. Diseñar correctamente una base de datos implica pensar antes de construir: identificar qué entidades existen, cómo se relacionan, qué atributos tienen, qué restricciones aplican, qué consultas se harán y cómo estructurarlo todo para que sea eficiente y escalable. Un buen diseño previene que más adelante haya que rehacer todo porque la estructura no soporta las necesidades reales del sistema. Diseñar bien es la diferencia entre un sistema que funciona a largo plazo y uno que se convierte en un problema con el tiempo.

**8. ¿Cómo ayuda una clave foránea a representar situaciones del mundo real?**

En el mundo real las cosas no existen solas: un empleado trabaja para una empresa, un estudiante asiste a un colegio, un paciente es atendido por un médico, un producto pertenece a una categoría. Las claves foráneas permiten representar esas conexiones dentro de la base de datos. Al poner el identificador de una entidad en la tabla de otra, el modelo refleja fielmente la relación que existe en la realidad. Sin claves foráneas cada tabla sería una isla de información aislada y la base de datos no podría representar el mundo real de forma coherente.

**9. ¿Por qué una matrícula necesita relacionar estudiantes y cursos?**

Porque una matrícula por definición es el vínculo entre una persona y un curso. No es solo información del estudiante ni solo información del curso, es la representación de que esa persona específica se inscribió en ese curso específico. Sin relacionar ambas entidades la matrícula no tendría significado completo. Además la tabla Matrículas puede guardar información propia del vínculo como la fecha de inscripción, el estado o la nota final, que no pertenecen ni al estudiante ni al curso por separado sino a ese acto específico de matricularse.

**10. ¿Qué importancia tiene pensar primero en el diseño antes de construir la base de datos?**

Es fundamental porque los errores de diseño son muy costosos de corregir después. Si se empieza a construir sin pensar bien la estructura y luego se descubre que una tabla está mal diseñada o que faltan relaciones importantes, corregir eso cuando ya hay datos reales puede requerir migrar millones de registros, modificar todas las aplicaciones que usan esa base de datos y gestionar tiempos de inactividad del sistema. Un buen diseño al principio ahorra muchísimo tiempo, dinero y dolores de cabeza después. En el SENA nos enseñan que antes de tocar SQL hay que tener claro el modelo.

---

## CONCLUSIÓN PERSONAL

Después de desarrollar este taller puedo decir que entendí algo que antes no tenía claro: una base de datos no es solo un lugar donde se guardan datos, sino un sistema con reglas que garantizan que esos datos tengan sentido y sean confiables.

Lo que más me impactó fue entender la integridad referencial. Antes pensaba que las claves foráneas eran solo una forma de conectar tablas, pero ahora entiendo que también son un mecanismo de protección. Evitan que el sistema acepte información que no tiene sentido, como una matrícula sin estudiante o un pedido sin cliente.

También me quedó claro por qué es tan importante diseñar antes de construir. En los proyectos que hemos hecho en el trimestre muchas veces uno se lanza a crear tablas sin pensar bien, y después surgen problemas que son difíciles de resolver. Este taller me ayudó a entender que ese tiempo de análisis inicial no es tiempo perdido sino que es lo que hace que todo lo demás funcione bien.

El modelo relacional será la base de todo lo que vamos a hacer en SQL, normalización y diseño de bases de datos. Tiene sentido haberlo estudiado primero desde la teoría porque así uno entiende el por qué de cada cosa, no solo el cómo.

---
