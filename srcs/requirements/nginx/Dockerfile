FROM debian:bullseye

#--no-install-recommends flag tells it to not install recommended packages besides the explicitly mentioned one keeping the Docker image size small.
RUN		apt-get update --no-install-recommends -y
RUN		apt-get install --no-install-recommends -y \ 
                nginx \
                openssl

COPY ./tools/script.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/script.sh

COPY ./conf/nginx.conf /etc/nginx/conf.d/nginx.conf

#nginx default port for http is 80 and for https is 443
EXPOSE	443

#dumb-init is a lightweight process manager that handles signals and termination and resource management gracefully by acting as PID 1 ie parent process
RUN apt-get install --no-install-recommends -y dumb-init

ENTRYPOINT ["/usr/bin/dumb-init", "--"]

#This line sets the CMD instruction, which defines the default command to be executed when the container starts. It uses the following arguments:
# nginx: The main Nginx executable.
# -g: This flag tells Nginx to run in the foreground. By default, Nginx would daemonize itself (run in the background). 
# The ; at the end likely suppresses output from a shell command within the configuration file.

CMD ["nginx", "-g", "daemon off;"]
