# Éngista TOPSIS

Aplicación web académica para tomar decisiones con el método **TOPSIS** (Technique for Order of Preference by Similarity to Ideal Solution) de Hwang y Yoon: escriba el desempeño real de cada alternativa, pondere los criterios y obtenga el ranking por cercanía a la solución ideal.

**Abrir la aplicación:** https://mgomezr1.github.io/engista-topsis/

No requiere instalación ni registro. Funciona en cualquier navegador moderno, en computador, tableta o teléfono.

## Qué permite hacer

- Definir un objetivo, las alternativas y los criterios, en la cantidad que necesite.
- Marcar cada criterio como de beneficio (más es mejor) o de costo (menos es mejor).
- Normalizar por el método vectorial clásico o por mín-máx.
- Ponderar los criterios manualmente o con la entropía de Shannon calculada a partir de los datos.
- Ver las soluciones ideal y anti ideal, las distancias y el coeficiente de cercanía de cada alternativa.
- Hacer análisis de sensibilidad y ver en qué pesos cambiaría la recomendación.
- Descargar los resultados en Excel (con fórmulas paso a paso) y un informe ejecutivo en PDF.

## Cómo usarla

1. Lea la sección «Cómo funciona el método TOPSIS» y pruebe la demostración de la portada.
2. En **Configuración**, escriba el objetivo, el número de alternativas y de criterios, registre los nombres y el tipo de cada criterio, y confirme.
3. En **Matriz de decisión**, escriba el desempeño real de cada alternativa.
4. En **Pesos**, escriba los pesos o elija la entropía de Shannon.
5. Pulse **Calcular resultados** y revise el ranking por coeficiente de cercanía.
6. Si quiere, explore la **Sensibilidad** y descargue el **Excel** o el **informe PDF**.

El **modo de prueba** carga ejemplos con datos ficticios para practicar; esos datos no provienen de expertos.

## Privacidad

Todos los cálculos se hacen en su navegador. Los datos no se envían a ningún servidor ni se guardan: al cerrar o recargar la página se pierden, así que descargue el Excel o el PDF antes de salir.

## Requisitos

- Navegador actualizado (Chrome, Edge, Firefox o Safari) con JavaScript activo.
- Conexión a internet para exportar a Excel, porque la aplicación descarga la biblioteca SheetJS. El informe PDF funciona sin conexión.

## Documentación

La guía completa (método, fórmulas, funciones, exportaciones y limitaciones) está en [docs/Guia_Engista_TOPSIS.md](docs/Guia_Engista_TOPSIS.md).

## Cómo citar

Gómez Rueda, M. S. (2026). *Éngista TOPSIS* (Versión 1.0) [Software]. https://mgomezr1.github.io/engista-topsis/

## Autoría y uso

Este aplicativo fue desarrollado por Mario Sergio Gómez Rueda. Su uso es de carácter académico y cualquier otro uso se regirá por el derecho de la propiedad intelectual. Consulte los términos en [LICENSE.md](LICENSE.md). Sugerencias o dudas: mgomezr1@gmail.com

## Fundamento metodológico

- Hwang, C.-L., & Yoon, K. (1981). *Multiple attribute decision making: Methods and applications*. Springer-Verlag. https://doi.org/10.1007/978-3-642-48318-9
- Behzadian, M., Otaghsara, S. K., Yazdani, M., & Ignatius, J. (2012). A state-of the-art survey of TOPSIS applications. *Expert Systems with Applications, 39*(17), 13051–13069. https://doi.org/10.1016/j.eswa.2012.05.056
- Shannon, C. E. (1948). A mathematical theory of communication. *The Bell System Technical Journal, 27*(3), 379–423. https://doi.org/10.1002/j.1538-7305.1948.tb01338.x
- Tzeng, G.-H., & Huang, J.-J. (2011). *Multiple attribute decision making: Methods and applications*. CRC Press.

## Componentes de terceros

La exportación a Excel usa [SheetJS Community Edition](https://sheetjs.com), distribuida bajo la licencia Apache 2.0 y cargada desde cdn.sheetjs.com.
