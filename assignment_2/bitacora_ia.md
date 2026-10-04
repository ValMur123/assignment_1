# Bitácora de uso de IA – Assignment 2

## Parte 1 – Scraping
Uso de IA en la Parte 1: Scraping (Paso 4: error al ejecutar la prueba de extracción)
Al ejecutar la celda de prueba del paso 4 apareció el error "NameError: name 'extraer_articulo' is not defined". Se le pidió a la IA que revisara por qué aparecía el error si la función estaba escrita en el notebook. La IA explicó que el código no tenía errores. En Jupyter, una función solo existe después de ejecutar la celda que la define; como esa celda no se había ejecutado en la sesión actual del kernel, Python todavía no la conocía. También explicó que el navegador seguía abierto porque, si no, el error habría sido name 'navegador' is not defined, ya que esa línea va antes en la celda. Entonces, la solución fue ejecutar primero la celda con def extraer_articulo(art): y luego la celda de prueba, que funcionó correctamente sin repetir el paso 2.
- Ivette Mamani

## Parte 3 – Cruce y analisis (Paso 8: Gráfico de barras):
Problema: La IA sugirió ordenar alfabéticamente los empates usando .sort_values(), pero "Áncash" aparecía al final porque Python procesa las letras con tilde con un código mayor.
Solución: Se añadió una columna auxiliar sin tildes (str.normalize("NFKD")) exclusiva para el ordenamiento, logrando la secuencia alfabética correcta (Áncash, Junín, Moquegua y Puno).
