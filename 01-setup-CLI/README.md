# 1. Install CLI tools localy and create Angular application

### 1.1 Create Workspace called "calab" with local CLI tools instance.

1. Type the following inside newly opened terminal window:

    ```.bash
    npx -p @angular/cli ng new calab
    ```

    > _You should see be asked to configure your workspace._

2. Select the following options:

    ```.bash
    Need to install the following packages:
    @angular/cli@17.3.4
    Ok to proceed? (y) y
    ? Which stylesheet format would you like to use? CSS [https://developer.mozilla.org/docs/Web/CSS]
    ? Do you want to enable Server-Side Rendering (SSR) and Static Site Generation (SSG/Prerendering)? Yes
    ```

3. Change directory to "calab":

    ```.bash
    cd calab
    ```

4. Start your newly created Angular application using local Angular CLI instance.

    ```.bash
    npx -p @angular/cli ng serve --host 0.0.0.0
    ```

    > _--host 0.0.0.0  means that IP address 0.0.0.0 is used on servers to designate a service may bind to all network interfaces. It tells a server to "listen" for and accept connections from any IP address._
