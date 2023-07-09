## Link al curso completo de Javascript en Youtube:
[VIDEO CURSO GRATIS COMPLETO: JavaScript Desde Cero por Sergie Code](https://youtu.be/N8Xt5rP_DUo)


# Tutorial de búsqueda de películas con JavaScript

Link para ver resultado: [BUSCADOR PELICULAS FINALIZADO](https://buscador-peliculas-javascript.netlify.app/)

Este es un tutorial que te guiará a través del proceso de creación de una aplicación de buscador de películas utilizando JavaScript. La aplicación utiliza la API de The Movie Database (TMDb) para buscar películas y mostrar sus detalles. A continuación, se proporciona una explicación paso a paso del código JavaScript necesario para que funcione la aplicación.

## Paso 1: Configuración de la API

Antes de comenzar, necesitarás obtener una clave de API de TMDb. Puedes obtener una clave de API registrándote en el sitio web de TMDb. Una vez que tengas tu clave de API, reemplaza `'API_KEY'` en el código con tu clave de API.

    let api_key = 'TU_CLAVE_DE_API'

## Paso 2: Definición de las URL de la API

A continuación, definiremos las URL base de la API y la URL base de las imágenes de las películas. Estas URL se utilizarán para realizar la búsqueda de películas y mostrar las imágenes de las mismas respectivamente.

    let urlBase = 'https://api.themoviedb.org/3/search/movie'
    let urlImg = 'https://image.tmdb.org/t/p/w200'

## Paso 3: Obtención de elementos del DOM

En este paso, obtenemos los elementos HTML necesarios para interactuar con la aplicación. Utilizamos `getElementById` para obtener el botón de búsqueda y el campo de entrada de texto.

    document.getElementById('searchButton').addEventListener('click', searchMovies)
    let resultContainer = document.getElementById('results')

## Paso 4: Función de búsqueda de películas

La función `searchMovies` se ejecuta cuando se hace clic en el botón de búsqueda. Obtiene el valor ingresado en el campo de entrada de texto y realiza una solicitud a la API de TMDb para buscar películas que coincidan con el término de búsqueda.

    function searchMovies(){
        resultContainer.innerHTML = 'Cargando...'
        let searchInput = document.getElementById('searchInput').value
        fetch(`${urlBase}?api_key=${api_key}&query=${searchInput}`)
        .then(response => response.json())
        .then(response => displayMovies(response.results))
    }

## Paso 5: Función para mostrar las películas encontradas

La función `displayMovies` se utiliza para mostrar los resultados de la búsqueda de películas. Borra el contenido anterior del contenedor de resultados y luego itera sobre la lista de películas encontradas. Para cada película, crea elementos HTML para mostrar su título, fecha de lanzamiento, descripción y póster.

    function displayMovies(movies){
        resultContainer.innerHTML = ''
    
        if(movies.length === 0){
            resultContainer.innerHTML= '<p>No se encontraron resultados para tu búsqueda </p>'
            return
        }
    
        movies.forEach(movie => {
            let movieDiv = document.createElement('div')
            movieDiv.classList.add('movie')
    
            let title = document.createElement('h2')
            title.textContent = movie.title
    
            let releaseDate = document.createElement('p')
            releaseDate.textContent = 'La fecha de lanzamiento fue: ' + movie.release_date
    
            let overview = document.createElement('p')
            overview.textContent = movie.overview
    
            let posterPath = urlImg + movie.poster_path
            let poster = document.createElement('img')
            poster.src = posterPath
    
            movieDiv.appendChild(poster)
            movieDiv.appendChild(title)
            movieDiv.appendChild(releaseDate)
            movieDiv.appendChild(overview)
    
            resultContainer.appendChild(movieDiv)
        })
    }

¡Y eso es todo! Siguiendo estos pasos, habrás creado una aplicación de buscador de películas en JavaScript utilizando la API de TMDb. Ahora puedes probar tu aplicación y ver cómo muestra los resultados de búsqueda de películas.

Recuerda que debes tener el HTML y el CSS correspondiente disponibles en tu repositorio de GitHub para que la aplicación funcione correctamente.
