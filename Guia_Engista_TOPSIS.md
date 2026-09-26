# Éngista TOPSIS

Guía de instalación, uso y documentación técnica de la aplicación `index.html` para aplicar el método TOPSIS (Technique for Order of Preference by Similarity to Ideal Solution). Versión 1.0.

Este aplicativo fue desarrollado por Mario Sergio Gómez Rueda. Su uso es de carácter académico y cualquier otro uso se regirá por el derecho de la propiedad intelectual. Sugerencias o dudas: mgomezr1@gmail.com

## 1. Descripción general

`index.html` es una aplicación web de un solo archivo construida con HTML5, CSS3 y JavaScript. Todos los cálculos ocurren en el navegador y los datos nunca salen del computador del evaluador. La única dependencia externa es SheetJS (`https://cdn.sheetjs.com/xlsx-0.20.3/package/dist/xlsx.full.min.js`), que se usa solo para generar el libro Excel de resultados. El informe PDF se genera con código propio y no necesita librerías ni conexión.

El modelo se construye digitando los datos en la interfaz. El número de alternativas (m) y de criterios (k) es dinámico: matrices, vectores, tablas, hojas de Excel y páginas del PDF se construyen con ciclos a partir de m y k.

La aplicación distingue dos orígenes de datos, visibles en la portada, en los resultados, en el Excel y en el PDF:

| Origen | Cómo se identifica |
|---|---|
| Datos digitados por el evaluador | «Datos digitados por el evaluador» |
| Datos de prueba | «Datos de prueba generados por la aplicación …; no provienen de expertos». Los archivos exportados llevan el prefijo `PRUEBA_` |

El nombre, la versión, el autor, el correo y la nota de uso están en una sola constante (`APLICATIVO`, al inicio del JavaScript). Si se cambian allí, se actualizan la interfaz, el Excel y el PDF.

## 2. Cómo guardar el archivo

1. Descargue `index.html` desde esta conversación.
2. Guárdelo en una carpeta de su computador, por ejemplo `Documentos/Engista_TOPSIS/`.
3. Conserve la extensión `.html`. Si lo edita, use un editor de texto plano (Bloc de notas, Visual Studio Code, Notepad++) y guarde con codificación UTF‑8.

## 3. Cómo ejecutarlo

1. Haga doble clic en `index.html`, o arrástrelo a una ventana de Chrome, Edge, Firefox o Safari en una versión reciente.
2. Para exportar a Excel se necesita conexión a internet la primera vez que se abre, porque el navegador descarga SheetJS. Sin conexión funcionan la configuración, los cálculos, la sensibilidad, las pruebas y el informe PDF.
3. No requiere instalar nada ni ejecutar un servidor local.

Uso sin conexión (opcional): descargue una vez `xlsx.full.min.js` de la dirección anterior, guárdelo junto a `index.html` y cambie la etiqueta del encabezado por `<script src="xlsx.full.min.js"></script>`.

## 4. Estructura de la interfaz

| Sección | Contenido |
|---|---|
| Riel lateral | Nombre del aplicativo, navegación por los seis pasos y el modo de prueba, y nota de autoría. Marca la sección visible y muestra un punto verde cuando el paso está listo o naranja cuando requiere atención. En tabletas y teléfonos se convierte en una barra superior |
| Portada | Nombre, origen de los datos, botón «Limpiar aplicación» y una demostración interactiva del eje de cercanía |
| Cómo funciona el método TOPSIS | Explicación en cuatro pasos, diagrama del eje ideal / anti ideal y nota de los tres indicadores clave |
| 1. Configuración | Objetivo, número de alternativas y criterios, y tipo de normalización. Un botón «Confirmar y construir la matriz» arma el paso 2 |
| 2. Matriz de decisión | Primero una tabla de criterios donde se nombra cada uno, se elige su sentido (Maximizar o Minimizar) y su peso relativo (deben sumar 1); luego la tabla de desempeño real de cada alternativa |
| 3. Resultados | Recomendación, ranking por coeficiente de cercanía, y tablas desplegables: configuración, pesos, matriz original, matriz normalizada, matriz ponderada y soluciones ideales |
| 4. Sensibilidad | Efecto de cambiar el peso de un criterio y puntos donde cambia el líder |
| 5. Exportación | «Exportar resultados a Excel» y «Descargar informe ejecutivo en PDF» |
| Modo de prueba | Cuatro escenarios ficticios y 14 pruebas automáticas |
| Pie | Autoría, nota de uso y referencias |

### Demostración interactiva de la portada

Está pensada para quien nunca ha usado TOPSIS. Muestra un eje entre la solución anti ideal (A−, coral) y la ideal (A+, esmeralda). Al mover la alternativa con el deslizador o con las flechas del teclado, se ve cómo su coeficiente de cercanía sube al acercarse a la ideal y baja al acercarse a la anti ideal. No afecta los datos del modelo.

### Sentido de los criterios

Cada criterio se marca en el paso 2 con un interruptor de dos botones: Maximizar, cuando más es mejor (por ejemplo calidad o garantía), y Minimizar, cuando menos es mejor (por ejemplo precio o tiempo de entrega). El botón activo se resalta: Maximizar en esmeralda y Minimizar en coral. En el encabezado de la matriz de decisión, cada criterio muestra su sentido, y «↓ minimizar» aparece en coral para distinguirlo a simple vista.

### Identidad visual

La interfaz usa un modo oscuro sobre fondo verde petróleo, sin bordes visibles: las superficies se separan por contraste de tono y sombras suaves. La identidad parte del par divergente del método: el esmeralda representa la proximidad a la solución ideal positiva (lo que se busca) y el coral la proximidad a la anti ideal negativa (lo que se evita). Esos colores tiñen el eje de la portada y el coeficiente de cercanía de cada alternativa. Los botones, pestañas, desplegables y mensajes tienen transiciones suaves, y la animación se reduce si el sistema operativo lo solicita.

Tipografía: no se enlaza ninguna fuente externa. Está activa la pila de fuentes del sistema. Para usar fuentes propias, descomente el bloque `@font-face` al inicio del CSS, coloque `MiFuenteTitulos.woff2` y `MiFuenteCuerpo.woff2` en una carpeta `fuentes` junto a `index.html` y active las variables de la Opción B. Todos los colores están centralizados como variables en `:root`.

## 5. Exportación a Excel

El libro contiene estas hojas:

| Hoja | Contenido |
|---|---|
| `Menu` | Datos del análisis (objetivo, origen, normalización, método de pesos, fecha, número de alternativas y criterios, alternativa recomendada) e índice con enlace a cada hoja. Al final, software, autor, contacto y nota de uso |
| `01_Decision` | Matriz de decisión con valores originales, tipo de cada criterio (beneficio o costo) y pesos aplicados, con la suma de pesos como fórmula |
| `02_Normalizada` | Matriz normalizada. Cada celda es una fórmula de Excel que referencia la hoja de decisión: raíz de suma de cuadrados en la vectorial, o mín-máx orientada según el tipo en la lineal |
| `03_Ponderada` | Tres bloques. A: matriz ponderada (normalizada × peso) como fórmulas. B: soluciones A+ y A− con `MAX`/`MIN` según el tipo. C: distancias D+ y D− con `SQRT(SUMXMY2(...))` y el coeficiente de cercanía Ci |
| `Resultado` | Ranking final por coeficiente de cercanía, con posición, alternativa, D+, D− y Ci |

Las fórmulas guardan también su valor calculado, de modo que el archivo se lee correctamente al abrirlo. El estudiante puede seguir el cálculo celda por celda: cambiar un valor en `01_Decision` recalcula toda la cadena.

## 6. Informe ejecutivo en PDF

El botón «Descargar informe ejecutivo en PDF» genera un documento tamaño carta con estas secciones:

1. Objetivo y recomendación: alternativa recomendada y su coeficiente de cercanía, diferencia con la segunda, criterio de mayor peso, método de normalización y de pesos, origen de los datos.
2. Clasificación de las alternativas con D+, D−, Ci y barras.
3. Peso de los criterios con su tipo y barras.
4. Soluciones ideal (A+) y anti ideal (A−).
5. Estabilidad de la recomendación: para cada criterio, qué pasa al variar su peso de 0 % a 100 %.
6. Nota metodológica, referencias y recuadro de autoría y uso.

Cada página lleva:

- Pie de página: «Éngista TOPSIS versión 1.0 | Desarrollado por Mario Sergio Gómez Rueda | Uso académico | mgomezr1@gmail.com», la numeración «Página x de n» y la frase sobre propiedad intelectual.
- Marca de agua diagonal translúcida: «USO ACADÉMICO» con el nombre del aplicativo y del autor.

El PDF se construye con un generador propio en JavaScript que usa las fuentes estándar Helvetica.

## 7. Fundamento de cálculo

Sea X la matriz de decisión de m alternativas (filas) por k criterios (columnas), con x_ij el desempeño de la alternativa i en el criterio j.

### 7.1 Normalización

Vectorial (Hwang y Yoon, 1981):

    r_ij = x_ij / raíz( Σ_i x_ij² )

Lineal mín-máx, orientada según el tipo del criterio:

- Beneficio: r_ij = (x_ij − mín_i x_ij) / (máx_i x_ij − mín_i x_ij)
- Costo: r_ij = (máx_i x_ij − x_ij) / (máx_i x_ij − mín_i x_ij)

Si el rango de una columna es cero (todos los valores iguales), esa columna normalizada toma el valor 1.

### 7.2 Pesos

El evaluador escribe el sentido y el peso de cada criterio en la tabla de criterios del paso 2. Cada criterio se marca como Maximizar (beneficio, más es mejor) o Minimizar (costo, menos es mejor). Los pesos deben sumar 1 (100 %); la aplicación muestra la suma en vivo y avisa si no es correcta. Internamente se usan tal cual (w_j = p_j), ya que suman 1.

### 7.3 Matriz ponderada y soluciones ideales

Matriz ponderada: v_ij = w_j · r_ij.

- Solución ideal positiva A+: para cada criterio, máx_i v_ij si es de beneficio, mín_i v_ij si es de costo.
- Solución anti ideal negativa A−: para cada criterio, mín_i v_ij si es de beneficio, máx_i v_ij si es de costo.

### 7.4 Distancias y coeficiente de cercanía

Distancias euclidianas de cada alternativa a las dos soluciones:

    D+_i = raíz( Σ_j (v_ij − A+_j)² )
    D−_i = raíz( Σ_j (v_ij − A−_j)² )

Coeficiente de cercanía:

    Ci_i = D−_i / (D+_i + D−_i)

Ci está siempre entre 0 y 1. La alternativa con mayor Ci es la recomendada. Los empates comparten posición en el ranking.

### 7.5 Análisis de sensibilidad

Se fija un nuevo peso para un criterio y los demás se reajustan en proporción para que la suma siga siendo 1. Al barrer ese peso de 0 a 1 se detectan los puntos donde cambia la alternativa líder; cada punto se refina por bisección con 40 iteraciones.

### 7.6 Variantes y supuestos discutibles

- La normalización vectorial es la del método original, pero no está pensada para valores negativos: la aplicación lo advierte y sugiere la normalización mín-máx en ese caso.
- La distancia es euclidiana, como en el TOPSIS clásico. Otras distancias (por ejemplo Manhattan) darían un método distinto y no se incluyen.
- TOPSIS supone criterios independientes y preferencias monótonas (más es siempre mejor en beneficio, siempre peor en costo). Si esos supuestos no se cumplen, el resultado debe leerse con cautela.

## 8. Explicación de las funciones principales

- `normalizarVectorial`, `normalizarMinMax`, `normalizar`: normalización de la matriz.
- `normalizarPesos`: normaliza los pesos del evaluador a suma 1.
- `sentidoATipo` y `tipoASentido`: traducen el sentido visible (max/min) al tipo interno del motor (beneficio/costo).
- `ejecutarTopsis`: núcleo que devuelve matrices intermedias, soluciones ideales, distancias y cercanía.
- `ordenarPorCercania`: ranking con posiciones y empates.
- `calcularModelo`: arma el objeto de resultados completo a partir de un modelo.
- `ajustarPesos`, `barrerSensibilidad`: análisis de sensibilidad.
- `crearLibroResultados` y sus hojas: exportación a Excel con fórmulas reales.
- `DocumentoPDF` y `generarInformePDF`: generador de PDF propio e informe ejecutivo.
- `ejecutarPruebas`: batería de 14 pruebas automáticas.

## 9. Ejemplo de uso con resultados verificados

Escenario «seleccionar proveedor» (datos de prueba), 3 alternativas y 4 criterios, normalización vectorial, pesos [0,40; 0,30; 0,20; 0,10]:

| Alternativa | Precio (costo) | Calidad (beneficio) | Garantía (beneficio) | Entrega (costo) |
|---|---|---|---|---|
| Proveedor A | 1200 | 8 | 24 | 15 |
| Proveedor B | 1000 | 7 | 12 | 10 |
| Proveedor C | 1400 | 9 | 36 | 20 |

Resultado verificado en navegador: la recomendación es **Proveedor C** con un coeficiente de cercanía de 0,5760; el segundo es Proveedor A con 0,5000.

Verificación analítica independiente (escenario «caso analítico 3 × 4», pesos iguales, todos beneficio): los coeficientes obtenidos son 0,6121, 0,3114 y 0,4553, que coinciden con el cálculo manual celda por celda y con la solución documentada en la literatura.

## 10. Pruebas automáticas

La sección «Modo de prueba» ejecuta 14 pruebas y muestra su resultado en una tabla:

1. Interpretación de valores (enteros, decimales con coma y punto, negativos y errores).
2. Normalización vectorial contra el cálculo manual.
3. Normalización mín-máx orientada según beneficio y costo.
4. Caso analítico 3 × 4 con los coeficientes esperados y Ci en [0, 1].
5. Caso límite: una alternativa dominante da Ci = 1 y la peor Ci = 0.
6. El sentido Minimizar invierte la preferencia (un criterio de costo elige el menor valor).
7. Pesos manuales normalizados a 1 sin alterar proporciones.
8. Ajuste de pesos en sensibilidad que conserva la suma 1.
9. Tamaños dinámicos (m de 2 a 8, k de 2 a 12) en las dos normalizaciones.
10. Ranking descendente, posiciones y empates compartidos.
11. Puntos críticos de sensibilidad confirmados numéricamente.
12. Estructura del Excel: hojas, enlaces del menú, fórmulas y valores releídos.
13. Estructura del PDF: encabezado, tabla xref, longitudes de flujo, pie y marca de agua.
14. Diferenciación de los datos de prueba.

## 11. Verificación realizada

La aplicación se ejecutó en un navegador real (Chromium). Las 14 pruebas automáticas pasan. No hay errores en la consola. El Excel se abre sin avisos, sus fórmulas coinciden con los valores guardados y los enlaces del menú funcionan. El PDF abre sin errores, con pie y marca de agua en todas las páginas. La página no presenta desplazamiento horizontal a 400 px de ancho. La autoría y la nota de uso aparecen en la interfaz, en el Excel y en el PDF. Los resultados coinciden con un cálculo independiente hecho por fuera de la aplicación.

## 12. Limitaciones

- TOPSIS es un método de apoyo a la decisión; el resultado depende de la calidad de los datos y de los pesos, y no sustituye el criterio profesional.
- La normalización vectorial no es apropiada con valores negativos; use la mín-máx en ese caso.
- El método supone criterios independientes y preferencias monótonas.

## 13. Cómo citar

En formato APA 7:

Gómez Rueda, M. S. (2026). *Éngista TOPSIS* (Versión 1.0) [Software]. https://mgomezr1.github.io/engista-topsis/

## 14. Referencias

Behzadian, M., Otaghsara, S. K., Yazdani, M., & Ignatius, J. (2012). A state-of the-art survey of TOPSIS applications. *Expert Systems with Applications, 39*(17), 13051–13069. https://doi.org/10.1016/j.eswa.2012.05.056

Hwang, C.-L., & Yoon, K. (1981). *Multiple attribute decision making: Methods and applications*. Springer-Verlag. https://doi.org/10.1007/978-3-642-48318-9

Tzeng, G.-H., & Huang, J.-J. (2011). *Multiple attribute decision making: Methods and applications*. CRC Press.
