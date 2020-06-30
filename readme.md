### Deploy

##### Step 1 	:

deploy using current docker-compose.yaml file, just update `environment` as required. Do not change `QUEUE_CONNECTION=database`. Make sure to check the logs, it should finish running stating something like this :

```sh
app_1  | Monica v2.18.0 is set up, enjoy.
app_1  | cron is not launched by default. Add CRON_LEGACY=true, use another container, or use supervisor.
```

##### Step 2	:

Stop Running containers or stack or run `docker-compose stop`. Now open and edit `docker-compose.yaml` file. 

Change these :

```sh
app:
    #image: arizawan/monicahq-supervisor
    image: monicahq/monicahq
    depends_on:
```

To these :

```sh
app:
    image: arizawan/monicahq-supervisor
    #image: monicahq/monicahq
    depends_on:
```

Now, run this command to rebuild and deploy `docker-compose up --build` or, if you are using portainer, stop all related containers and run stack again.

Why we are doing this?

* MonicaHQ docker container is not build to run the application with supervisor when freashly build. We have to setup the database/migration etc first with the original MonicaHQ image and then update it with the supervisor image.
