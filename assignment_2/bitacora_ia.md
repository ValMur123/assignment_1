# Bitácora de uso de IA – Assignment 2

## Parte 1 – Scraping
Uso de IA en la Parte 1: Scraping (Paso 4: error al ejecutar la prueba de extracción)
Al ejecutar la celda de prueba del paso 4 apareció el error "NameError: name 'extraer_articulo' is not defined". Se le pidió a la IA que revisara por qué aparecía el error si la función estaba escrita en el notebook. La IA explicó que el código no tenía errores. En Jupyter, una función solo existe después de ejecutar la celda que la define; como esa celda no se había ejecutado en la sesión actual del kernel, Python todavía no la conocía. También explicó que el navegador seguía abierto porque, si no, el error habría sido name 'navegador' is not defined, ya que esa línea va antes en la celda. Entonces, la solución fue ejecutar primero la celda con def extraer_articulo(art): y luego la celda de prueba, que funcionó correctamente sin repetir el paso 2.
- Ivette Mamani

## Parte 2: API de lluvias 

Le pedimos el código para leer con `pd.read_html` la tabla de departamentos de Wikipedia y quedarnos con las columnas departamento y capital, para luego geocodificar cada capital con Open-Meteo.

La IA nos dio un código que busca la tabla con columnas "departamento" y "capital" y compara cada nombre con nuestra lista de 25 departamentos:

    for dep in departamentos:
        coincide = wiki[wiki["dep_norm"] == normalizar(dep)]
        capital = coincide.iloc[0]["capital"] if len(coincide) > 0 else None

El resultado estaba incompleto: la tabla extraída solo tenía 24 departamentos. Nos dimos cuenta en la celda de verificación, que imprimió:

    Departamentos encontrados: 24 de 25
    Departamentos que faltan: ['Callao']

La tabla de Wikipedia no incluye al Callao, porque es una Provincia Constitucional y no un departamento. Si no lo hubiéramos revisado, el Callao no tendría lluvia y el cruce de la Parte 3 no llegaría a 25 filas.
Además, la capital de Lima venía como "Huacho (de facto)". Con ese texto, la API de geocodificación no habría encontrado la ciudad.

- Agregamos el Callao a mano con capital "Callao", según la división político-administrativa del INEI (ubigeo 07).
- Limpiamos la columna capital con una expresión regular que quita los textos entre paréntesis, así "Huacho (de facto)" quedó como "Huacho".
- Volvimos a correr la verificación y la tabla quedó con 25 filas y ninguna capital vacía (`assert` sin errores).

## Parte 3 – Cruce y analisis (Paso 8: Gráfico de barras):
Problema: La IA sugirió ordenar alfabéticamente los empates usando .sort_values(), pero "Áncash" aparecía al final porque Python procesa las letras con tilde con un código mayor.
Solución: Se añadió una columna auxiliar sin tildes (str.normalize("NFKD")) exclusiva para el ordenamiento, logrando la secuencia alfabética correcta (Áncash, Junín, Moquegua y Puno).
