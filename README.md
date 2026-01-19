# Solución al Desafío: Data Detective (Books To Scrape)

Este repositorio contiene la solución completa al desafío técnico de extracción y análisis de datos planteado bajo la narrativa de "Detective de Datos". El objetivo principal fue desarrollar un pipeline ETL (Extracción, Transformación y Carga) desde cero, sin utilizar frameworks de alto nivel, para analizar el mercado de libros del sitio *Books To Scrape*.

## Descripción del Proyecto

El proyecto consiste en un script de Python que automatiza la navegación web, extrae información detallada de libros, normaliza los datos y los almacena en una base de datos relacional diseñada a medida. Finalmente, se utiliza SQL para generar reportes de inteligencia de negocios y optimizar el rendimiento de las consultas.

## Tecnologías Utilizadas

* **Lenguaje:** Python 3
* **Web Scraping:** BeautifulSoup4, Requests, Urllib
* **Base de Datos:** SQLite3 (SQL estándar)
* **Análisis y Reportes:** Pandas
* **Enriquecimiento de Datos:** OpenLibrary API

## Estructura del Repositorio

* `escrapear.ipynb`: El Jupyter Notebook principal que contiene todo el código fuente (scraping, modelado de BD y consultas).
* `libreria.db`: El archivo de base de datos SQLite generado resultante de la ejecución del script.

## Detalles de la Implementación

El desarrollo se divide en cuatro fases clave, todas contenidas en `escrapear.ipynb`:

### 1. Web Scraping (Extracción)
El script recorre iterativamente las 50 categorías del sitio web.
* **Paginación:** Maneja automáticamente la navegación a través de múltiples páginas por categoría.
* **Limpieza:** Convierte datos crudos (precios con símbolos, calificaciones en texto) a formatos numéricos procesables.
* **API Externa:** Se implementó una conexión a la API de OpenLibrary para intentar identificar autores reales basados en los títulos de los libros.

### 2. Modelado de Base de Datos
Se diseñó un esquema relacional en SQLite (`libreria.db`) cumpliendo con el requisito de una relación **Muchos a Muchos**.

**Esquema de Tablas:**
* `categorias`: ID y nombre del género.
* `autores`: ID y nombre del autor.
* `libros`: Detalles del libro (precio, rating, stock).
* `libro_autor`: Tabla intermedia que vincula libros con autores.

### 3. Consultas SQL (Análisis)
Se ejecutaron consultas complejas utilizando `JOIN`, `GROUP BY` y funciones de agregación para responder preguntas de negocio, tales como:
* Identificación de libros de alta calidad (5 estrellas).
* Búsqueda de oportunidades (libros de bajo costo en categorías específicas).
* Análisis de volumen de inventario por categoría.

### 4. Optimización de Rendimiento
Se incluye una prueba de concepto sobre indexación en bases de datos.
* Se midió el tiempo de respuesta de una búsqueda de texto en la columna `titulo`.
* Se aplicó un índice (`CREATE INDEX`) y se demostró la reducción en el tiempo de ejecución de la consulta.
