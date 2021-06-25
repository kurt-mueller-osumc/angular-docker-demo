# Angular Docker Demo

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 12.1.0. It demonstrates how to development, build, and deploy an Angular application via a docker image.

## Development

This app makes extensive use of VS Code's Remote Container extension. If you have that extension installed, opening this repo inside the editor will prompt you to reopen it inside a Docker container.

The extension mounts the local project folder, `angular-docker-demo` inside the running container as `workspaces/angular-docker-demo`. It also adds the project files to `/app`, the default working directory specified in the `Dockerfile`.

`.devcontainer/devcontainer.json` contains VS Code's configuration for the devcontainer, including local extensions, post create commands, the default remote user, as well as docke configuration.

## Development server

Inside the container, on the command line, you'll be able to start up a development server using the default `ng serve` command. When the app has booted, VS Code will prompt you to open a browser to see the app being served.

If, instead, you'd like to run the development server on the host machine, outside a running container, you can run commands similar to the following:

```bash
# build the docker image and target the `dev` stage
docker build . -t angular-docker-demo --target dev
# map port 80 to 4200; allow CTRL-C to stop the running container;  remove the container once it's done running
docker run -p 80:4200 -it --rm angular-docker-demo
```

Now open up `0.0.0.0` in your browser and you'll see the running web app.

To stop the container, open up another terminal and run the following commands:

```bash
# see the running docker processes, including the container id of the angular app
docker ps
docker container stop <CONTAINER_ID>
```

## Production server

Run the following commands to build the image for production use. It first builds the `dev` stage, including compiling everything into static assets, and then moves on to the `prod` stage, based off the `nginx` docker image, copying the compiled assets into the approprate directory to be served by `nginx` web server.

```bash
docker build . -t angular-docker-demo
# navigate to localhost to view the page
docker run --rm -it angular-docker-demo
```
