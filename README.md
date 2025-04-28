# Actividad: Ramas, fusiones y colaboración - conflicto sin resolver en el clon

**Prerrequisitos:**

* Comprender los comandos básicos de Git: init, add, commit, status, log
* Tener una cuenta en esta plataforma, GitHub
* Tener creado un repositorio nuevo y vacío

**A medida que vaya realizando la actividad:**
Escriba las respuestas a las preguntas planteadas en esta actividad en un archivo de TEXTO aparte (.txt, no de Word ni ningún tipo de documento), fuera de la carpeta en donde trabajaran con el repositorio creado. Tendrá que versionar este archivo al final de la actividad.

## Configuración inicial del proyecto

Realice los siguientes pasos para configurar el entorno de trabajo para esta actividad:

1. **Cree y acceda a la carpeta del proyecto:**
    * Elija una ubicación en su sistema y cree una nueva carpeta para este proyecto
    * Ingrese a esa carpeta desde su consola (Ej: <code>cd ruta\a\\<nombre_de_carpeta></code>). **Todos los comandos siguientes se ejecutan dentro de esta carpeta.**
2. **Inicialice el repositorio Git:** <code>git init</code>
3. **Cree y confirme archivos iniciales:**
    * Cree un archivo de texto &lt;nombre_de_archivo&gt; con cualquier contenido para el proyecto
      <pre>
      git add &lt;nombre_de_archivo&gt;
      git commit -m "Commit inicial: Agrega &lt;nombre_de_archivo&gt;"
      </pre>
4. **Cree el repositorio remoto:**
    * Acceda al sitio web de GitHub
    * Cree un **nuevo repositorio** como vimos en clase
    * Copie la URL (HTTPS) del repositorio remoto
5. **Conecte el repositorio local al remoto:**
    * Reemplace &lt;url_del_repositorio_remoto&gt; con la URL copiada:
      <pre>git remote add origin &lt;url_del_repositorio_remoto&gt;</pre>
6. **Verifique la conexión remota:** <code>git remote -v</code>
    * **Pregunta:** ¿Qué información proporcionan las URLs listadas para el remoto origin?
7. **Suba el estado inicial al remoto:**
   <pre>
   git push -u origin main
   # (Use 'master' si su rama principal se llama así)
   </pre>
   * Verifique en la interfaz web del repositorio remoto que los archivos y commits iniciales ahora están presentes.

## Ejercicio 1: Introducción a las ramas (Branches)

1. **Liste y verifique las ramas:** <code>git branch</code>
    * **Pregunta:** ¿Qué indica el asterisco (*) al lado del nombre de las ramas?
2. **Cree una nueva rama:**
    * Elija un nombre descriptivo para una nueva característica o tarea (ej: desarrollo-login, fix-bug-123, mejora-ui). Ejecute: <code>git branch <nombre_de_su_rama></code>
    * Ejecute <code>git branch</code> nuevamente.
    * **Pregunta:** ¿Se lista la nueva rama que creó? ¿Cuál sigue siendo la rama activa según el indicador?
3. **Cámbiese a la nueva rama:** <code>git checkout <nombre_de_su_rama></code>
    * Ejecute: <code>git branch</code>
    * **Pregunta:** ¿Qué rama figura como activa ahora? ¿Qué referencia interna importante de Git cree que se actualizó para reflejar este cambio?
4. **Realice cambios en la nueva rama:**
    * Modifique uno de los archivos existentes o cree uno nuevo.
    * Prepare y confirme este cambio **en esta rama**, utilizando un mensaje de commit descriptivo:
      <pre>
      git add &lt;archivo_modificado_o_nuevo&gt;
      git commit -m "Su mensaje descriptivo del cambio"
      </pre>
    * **Pregunta:** ¿Cuál es la relación entre la rama activa (la que creó), el nuevo commit creado y la referencia HEAD?
5. **Compare con la rama principal:**
    * Vuelva a la rama principal: <code>git checkout main</code>
    * **Pregunta:** ¿Cuál es ahora la rama activa indicada por HEAD?
    * Revise el contenido del archivo que modificó en la otra rama.
    * **Pregunta:** ¿Está presente la modificación que realizó en la rama anterior? ¿Qué demuestra esto sobre el aislamiento entre ramas?
6. **Visualice las ramas:** <code>git log --oneline --graph --all</code>
    * **Pregunta:** ¿Cómo representa el gráfico la separación de la historia entre main y la rama que creó? ¿Cómo identifica la posición actual (HEAD) en este gráfico?

## Ejercicio 2: Merge sin conflictos (Fast-Forward Merge)

1. **Asegúrese de estar en la rama receptora (main o master).**
2. **Fusione la rama de la característica:**
    * Fusione la rama que creó en el ejercicio anterior: <code>git merge &lt;nombre_de_su_rama&gt;</code>
    * **Pregunta:** ¿La salida del comando <code>git merge</code> indica qué tipo de fusión se realizó? ¿Qué implica ese tipo de fusión para el historial?
3. **Verifique el resultado:**
    * Revise el contenido del archivo que modificó en la rama fusionada.
    * **Pregunta:** ¿Contiene ahora las modificaciones realizadas en la rama fusionada?
    * Ejecute: <code>git log --oneline --graph</code>
    * **Pregunta:** ¿Cómo se refleja en el historial que main ahora incluye los cambios? ¿Qué indica la posición de la etiqueta main en el grafo?
4. **Elimine la rama fusionada:**
    * Una vez fusionada, puede eliminar la rama de característica: <code>git branch -d &lt;nombre_de_su_rama&gt;</code>
    * Ejecute: <code>git branch</code>
    * **Pregunta:** ¿Qué efecto tuvo el comando <code>git branch -d</code> en la lista de ramas?

## Ejercicio 3: Merge con conflictos

1. **Cree y cámbiese a una nueva rama, rama donde se provocará el conflicto:** <code>git checkout -b &lt;nombre_rama_conflicto&gt;</code>
2. **Modifique un archivo en la nueva rama:**
    * Elija un archivo y modifique una línea específica.
   <pre>
    git add &lt;archivo_modificado&gt;
    git commit -m "Su mensaje para el primer cambio conflictivo"
   </pre>
3. **Modifique la MISMA línea en la rama principal:**
    * Vuelva a main: <code>git checkout main</code>
    * Modifique la **misma línea** en el **mismo archivo** pero de forma **diferente**.
   <pre>
    git add &lt;archivo_modificado&gt;
    git commit -m "Su mensaje para el segundo cambio conflictivo en main"
   </pre>
4. **Intente la fusión:**
    * Asegúrese de estar en main y ejecute: <code>git merge &lt;nombre_rama_conflicto&gt;</code>
    * **Pregunta:** ¿Qué mensaje específico de Git le alerta sobre la existencia de un conflicto y en qué archivo?
5. **Inspeccione el estado y el archivo:**
    * Ejecute: <code>git status</code>
    * **Pregunta:** ¿Qué indica la sección "Unmerged paths" sobre el estado del archivo durante un conflicto?
    * Abra el archivo en conflicto con su editor.
    * **Pregunta:** ¿Qué versión del código representa el bloque delimitado por &lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD y =======? ¿Y el bloque entre ======= y &gt;&gt;&gt;&gt;&gt;&gt;&gt; &lt;nombre_rama_conflicto&gt;?
6. **Resuelva el conflicto manualmente:**
    * Edite el archivo, decida qué contenido final debe tener la sección conflictiva y **elimine completamente** las marcas de conflicto (&lt;&lt;&lt;&lt;&lt;&lt;&lt;, =======, &gt;&gt;&gt;&gt;&gt;&gt;&gt;).
7. **Marque el conflicto como resuelto:** <code>git add &lt;archivo_modificado_y_resuelto&gt;</code>
8. **Complete el commit de merge:**
    * Ejecute: <code>git status</code>
    * **Pregunta:** ¿Cómo cambió el estado del archivo después de ejecutar git add en el contexto de un conflicto resuelto?
    * Ejecute: <code>git commit</code> y confirme el mensaje en el editor.
9. **Verifique:**
    * Ejecute: <code>git log --oneline --graph</code>
    * **Pregunta:** ¿Cómo se visualiza en el historial la fusión completada después de resolver el conflicto? ¿Dónde se ubica HEAD tras este commit de merge?
    * (_Opcional_) Elimine la rama: <code>git branch -d &lt;nombre_rama_conflicto&gt;</code>

## Ejercicio 4: Subir cambios al repositorio remoto (push)

1. **Suba la rama principal (main):**
    * Asegúrese de estar en main.
   <pre>
    git push origin main
    # O simplemente 'git push'
   </pre>
2. **Verifique en el remoto:**
    * Visite la página web de su repositorio remoto.
    * **Pregunta:** ¿Se sincronizó el historial remoto con los últimos cambios de su rama main local?
3. **Suba otra rama cualquiera:**
    * Si tuviera otra rama local con commits que desea compartir o respaldar, ¿cómo la subiría al remoto origin?

## Ejercicio 5: Simular colaboración y bajar cambios (pull)

Para practicar el flujo de trabajo colaborativo, simularemos que otra persona (o usted mismo desde otra ubicación) realiza cambios en el repositorio remoto.

1. **Navegue fuera del directorio original:**
    * En su consola, asegúrese de estar dentro de otra carpeta, diferente de la que estuvo usando hasta el momento.
2. **Clone el repositorio remoto en dicha carpeta:**
    * Utilice <code>git clone</code> seguido de la URL de *su* repositorio remoto para clonarlo: <code>git clone &lt;url_del_repositorio_remoteo&gt;</code>
    * **Pregunta:** ¿Observa mensajes indicando que se está clonando el repositorio? ¿Se creó una nueva carpeta llamada de la misma forma en la cual nombró al repositorio?
3. **Ingrese al repositorio clonado y realice cambios:**
    * Acceda a la nueva carpeta creada debido a la clonación.
    * Ejecute: <code>git status</code> para verificar que se encuentra en la carpeta correcta.
    * Abra y modifique un archivo cualquiera en este clon, o agregue algún archivo.
4. **Confirme y suba los cambios desde el clon:**
    * Prepare y confirme el cambio realizado en el clon con un mensaje descriptivo:
   <pre>
      git add &lt;archivo_modificado_en_clon&gt;
      git commit -m "Su mensaje descriptivo del cambio desde el clon"
   </pre>
    * Suba este commit desde el clon al repositorio remoto origin:
   <pre>
      git push origin main
      # (O la rama principal que esté usando)
   </pre>
    * **Pregunta:** ¿El comando push se ejecutó correctamente, indicando que los cambios se subieron al remoto?
5. **Regrese al repositorio original:**
    * Salga de la carpeta del repositorio clonado y vuelva a ingresar a su carpeta de trabajo original.
    * Verifique que se encuentra en el directorio correcto con los comandos ya dados.
6. **Obtenga y fusione los cambios remotos en el repositorio original:**
    * Ahora, desde su repositorio original, obtenga los cambios que "otra persona" (usted, desde el clon) subió al remoto. Asegúrese de estar en la rama main.
    * Ejecute:
    <pre>
      git pull origin main
      # O simplemente 'git pull' si el seguimiento está configurado
   </pre>
7. **Verifique los cambios localmente:**
    * **Pregunta:** ¿Qué información relevante le proporciona la salida del comando <code>git pull</code> acerca de los cambios bajados y la estrategia de integración utilizada (merge, fast-forward, etc.)?
    * Revise el contenido del archivo que modificó desde el clon.
    * **Pregunta:** ¿Contiene ahora la modificación realizada desde el repositorio clonado?
    * Ejecute: <code>git log --oneline --graph</code>.
    * **Pregunta:** ¿Cómo se representa en el historial local el commit realizado "externamente"? ¿Cómo se integró este commit en relación a la rama main y a la referencia HEAD?

## Ejercicio 6: Merge con remotos

Sin instrucción previa y según lo visto en clase, intente crear un conflicto con cambios hechos en el remoto, que usted aún no tenga en su rama local. Debe usar los conocimientos de este trabajo práctico y los métodos vistos en clase para recrear este escenario común en la práctica laboral.

## Ejercicio 7: Push de las respuestas

Copie y pegue el archivo de las respuestas solicitado al principio de esta actividad en la carpeta del repositorio creado. Cree una versión del repositorio con este archivo y haga push de esta nueva versión con las respuestas al repositorio remoto.

## Ejercicio final:

Próximamente :)
