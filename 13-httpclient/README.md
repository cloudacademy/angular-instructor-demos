# Angular HttpClient Demo

## 1. Setup Project

### 1.1 Install JSON Server Dependencies

1. Change directory to `json-server`:

    ```.sh
    cd json-server
    ```
2. Install dependencies by running the following command:

    ```.sh
    npm install
    ```

### 1.2 Start JSON Server
1. Start JSON server:

    ```.bash
    npx json-server MOCK_DATA.json -p 3001
    ```

### 1.3 Install Angular Dependencies

1. Open new Terminal window.
2. Change directory to `calab`:

    ```.bash
    cd calab
    ```
2. Install dependencies by running the following command:

    ```.bash
    npm install
    ```

### 1.4 Start The Application

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._

## 2. Setup HttpClient

### 2.1 Update App Configuration

1. Open `src/app/app.config.ts` file and do the following:
    - Import `provideHttpClient`:

        ```.js
        import { provideHttpClient } from '@angular/common/http';
        ```

    - Provide `provideHttpClient` helper function:

        ```.js
        export const appConfig: ApplicationConfig = {
            providers: [ provideRouter(routes), provideClientHydration(), provideHttpClient() ]
        };
        ```

## 3. Create and configure a new Service

### 3.1 Create a new Service

1. Create a new component using CLI and name it `MovieService`:

    ```.bash
    npx -p @angular/cli ng generate service services/movie
    ```

### 3.2 Inject The HttpClient Service 

1. Open `src/app/services/movie.service.ts` file and do the following:
    - Import `HttpClient`:

        ```.js
        import { HttpClient } from '@angular/common/http';
        ```

    - Inject `HttpClient` as a dependency into `MovieService` constructor.

        ```.js
        export class MovieService {
            constructor(private httpClient: HttpClient) { }
        }        
        ```

## 4. Create a Movie Model

### 4.1 Create a new class representing a movie model
1. Create a new directory in `src/app/` called `models`.
2. Change directory to `src/app/models`
3. Create new `TypeScript` file called `movie.ts`
4. Add the following code inside `movie.ts`:

    ```.js
    export class Movie {
        constructor(
            public title: string,
            public genre: string,
            public release_date: string,
            public director: string,
            public rating: number,
            public duration_minutes: number,
        ) {}
    }
    ```

## 5. Making Http Requests

### 5.1 Create a GET http request
1. Open `src/app/services/movie.service.ts` file and do the following:
    - Import `Movie` model:

        ```.js
        import { Movie } from '../models/movie';
        ```

    - Declare a new function called `getAllMovies` that calls http get() method.

        ```.js 
        getAllMovies(){
            this.httpClient.get<Movie>('http://localhost:3001/movies').subscribe(data => {
                console.log(data);
            });
        }
        ```

### 5.2 Call method containing GET http request 
1. Open `src/app/app.component.ts` file and do the following:
    - Import MovieService:

        ```.js
        import { MovieService } from './services/movie.service';
        ```
    - Inject `MovieService` as dependency into `AppComponent`.

        ```.js
        export class AppComponent {
            constructor(private movieService: MovieService){}
            ...
        }
        ```
    - Inside constructor, make a call to getAllMovies() method.

        ```.js
        export class AppComponent {
            constructor(private movieService: MovieService){
                movieService.getAllMovies();
            }
            ...
        }
        ```

### 5.3 Review Changes

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._

2. Inspect developer console if using Chrome for any logs. You should see the following geting printed:

    ```.sh
    (20) [{…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}]
    ```

### 5.3 Create a POST http request
1. Open `src/app/services/movie.service.ts` file and do the following:
    - Declare a new function called `createMovie` that takes Movie as a parameter and calls http post() method.

        ```.js
        createMovie(movie: Movie){
            this.httpClient.post<Movie>('http://localhost:3001/movies', movie).subscribe(res => {
            console.log('Created movie:', res);
            });
        }
        ```

### 5.4 Call method containing POST http request 
1. Open `src/app/app.component.ts` file and do the following:
    - Import `Movie` model:

        ```.js
        import { Movie } from './models/movie';
        ```
    - Inside constructor, create an instance of a movie.

        ```.js
        const movie = new Movie( 
            "Forrest Gump",
            "Drama",
            "1994",
            "Robert Zemeckis",
            8.8,
            142
        );
        ```
    - Inside constructor, make a call to createMovie() method.

        ```.js
        movieService.createMovie(movie);
        ```

### 5.5 Review Changes

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._
2. Inspect developer console if using Chrome for any logs. You should see the following geting printed:
    ```.sh
    Created movie: {id: 'af2c', title: 'Forrest Gump', genre: 'Drama', release_date: '1994', director: 'Robert Zemeckis', …}
    ```


## 6. Interceptors

### 6.1 Define an Interceptor
1. Open `src/app/app.config.ts` file and do the following:

    - Import `withInterceptors`, `HttpEvent`, `HttpHandlerFn`, `HttpRequest` and `Observable`:

        ```.js
        import { HttpEvent, HttpHandlerFn, HttpRequest, provideHttpClient, withInterceptors } from '@angular/common/http';
        import { Observable } from 'rxjs';
        ```

    -  Define a `loggingInterceptor` helper function:

        ```.js
        export function loggingInterceptor(req: HttpRequest<unknown>, next: HttpHandlerFn): Observable<HttpEvent<unknown>> {
            console.log(`Request URL is: ${req.url}`);
            return next(req);
        }
        ```
    - Declare an interceptor inside `provideHttpClient` helper function:

        ```.js
        export const appConfig: ApplicationConfig = {
            providers: [provideRouter(routes), provideHttpClient(
                withInterceptors([loggingInterceptor]),
            ),]
        };
        ```

### 6.2 Start The Application

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve 
    ```
    > _Otherwise refresh the browser tab to see updated view._
2. Inspect developer console if using Chrome for any logs. You should see the following geting printed:
    ```.sh
    Request URL is: http://localhost:3001/movies
    ```
