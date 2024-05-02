# Angular Dependency Injection Demo

### Install Dependencies

-   Change directory to `calab`:
    ```
    cd calab
    ```
-   Install dependencies by running the following command:
    ```
    npm install
    ```

## Creating Injectable Service

### Create a new Course Service and Implement it's logic

- Create a new `CourseService` using CLI:
    ```
    npx -p @angular/cli ng generate service course/course 
    ```
- Open `src/app/course/course.service.ts` file and do the following:
    - Import Mock course data from the following file:
        ```
        import  COURSES   from './MOCK_COURSE_DATA.json';
        ```
    - Add the following method just after the `constructor`:
        ```
          getCourses(){
            return COURSES;
        }
        ```

### Implement Course Model Class
- Inside `src/app/course` folder create a new file called `course.ts`.
- Open `course.ts` and add the following code:
    ```
    export class Course{
        course_id: number | undefined;
        course_name: string | undefined;
        course_description: string | undefined;
        course_duration: number | undefined;
    }
    ```

### Inject Course Service Into AppComponent

- Open `src/app/app.component.ts` file and do the following:
    - Import Course model:
        ```
        import { Course } from './course/course';
        ```
    - Inside `AppComponent` class declare variable called courses with type of list of Courses:
        ```
        courses: Course[] = [];
        ```
        
    - Add the `CourseService` as a parameter into the  `constructor`.
        ```
        constructor(private courseService: CourseService){}
        ```
    - Fetch list of courses by calling `getCourses()` method from `courseService` and assign responce to variable declared above.
        ```
        this.courses = courseService.getCourses();
        ```

### Render List of Courses

- Open `src/app/app.component.html` file and just below the `<div class="divider">` add the following code that loops list of courses and renders each course in a list:
    ```
      <ul>
        @for (course of courses; track course.course_id) {
          <li>
            <div>
              <p><strong>Id</strong> {{ course.course_id }}</p>
              <p><strong>Title: </strong>{{ course.course_name }}</p>
              <p><strong>Description: </strong>{{ course.course_description }}</p>
              <p><strong>Duration: </strong>{{ course.course_duration }} weeks</p>

              <div class="divider" role="separator" aria-label="Divider"></div>
            </div>
            
          </li>
        }
      </ul>
    ```

### Start The Application

-   Start Angular Development Server:
    ```
    npx -p @angular/cli ng serve  --host 0.0.0.0 
    ```
- Inspect the Rendered Screen, you should see list of courses on your screen.

## Injecting services in other services 

### Create a new Logger and Implement it's logic

- Create a new `Logger` using CLI:
    ```
    npx -p @angular/cli ng generate service logger/logger 
    ```
- Open `src/app/logger/logger.service.ts` file and do the following:
    - Create logging methods just below the `constructor` :
        ```
        log(msg: unknown) { console.log(msg); }
        error(msg: unknown) { console.error(msg); }
        warn(msg: unknown) { console.warn(msg); }
        ```

### Inject Logger Service Into Course Service and Log When Courses are Fetched

- Open `src/app/course/course.service.ts` file and do the following:
    - Import Logger service:
        ```
        import { LoggerService } from '../logger/logger.service';
        ```

    - Add the `CourseService` as a parameter into the  `constructor`.
        ```
        constructor(private logger: LoggerService) { }
        ```
    - Inside `getCourses()` method log that courses are getting fetched.
        ```
        this.logger.log('Fetching Courses');
        ```


## Configuring Dependency Providers


### Creating Enhanced Logger

- Create a new `TimedLoggerService` using CLI:
    ```
    npx -p @angular/cli ng generate service logger/timed-logger 
    ```

- Open `src/app/logger/timed-logger.service.ts` file and do the following:
    - Extend `LoggerService` with `TimedLoggerService`:
        ```
        export class TimeLoggerService extends LoggerService {...}
        ```
    - Override logging methods just below the `constructor` :
        ```
        constructor() {
            super()
        }
        override log(msg: unknown) { 
            const date = Date.now();
            console.log(`${date}: ${msg}`); 
        }
        override error(msg: unknown) { 
            const date = Date.now();
            console.error(`${date}: ${msg}`); 
        }
        override warn(msg: unknown) { 
            const date = Date.now();
            console.warn(`${date}: ${msg}`); 
        }
        ```

### Configure an app-wide provider in the ApplicationConfig of bootstrapApplication, it overrides one configured for root in the @Injectable() metadata.

- Open `app.config.ts` file and add the following:
    - Update providers with the following:
    ```
      providers: [provideRouter(routes), provideClientHydration(), {provide: LoggerService, useClass: TimeLoggerService}]
    ```

### Review Changes

- Inspect console and see whether your application logs with new Enhanced Timed Logger.
    ```
    1714649534570: Fetching Courses
    ```