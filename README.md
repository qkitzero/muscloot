# Muscloot

- [Muscloot Frontend](https://github.com/qkitzero/muscloot-frontend)
- [Auth Service](https://github.com/qkitzero/auth-service)
- [User Service](https://github.com/qkitzero/user-service)
- [Workout Service](https://github.com/qkitzero/workout-service)
- [Logging Service](https://github.com/qkitzero/logging-service)

```mermaid
flowchart TD
    user(User)

    subgraph gcp[GCP]
        subgraph cloud_run[Cloud Run]
            workout_frontend(Muscloot)
            auth_service(Auth Service)
            auth_service_gateway(Auth Service Gateway)
            user_service(User Service)
            user_service_gateway(User Service Gateway)
            workout_service(Workout Service)
            workout_service_gateway(Workout Service Gateway)
            logging_service(Logging Service)
        end
    end

    subgraph external[External]
        auth0(Auth0)
        user_db[(User DB)]
        workout_db[(Workout DB)]
        logging_db[(Logging DB)]
    end

    user --> workout_frontend

    workout_frontend --> auth0
    workout_frontend --> auth_service_gateway --> auth_service --> auth0
    workout_frontend --> user_service_gateway --> user_service
    workout_frontend --> workout_service_gateway --> workout_service

    user_service --> auth_service
    logging_service --> auth_service
    workout_service --> auth_service
    workout_service --> logging_service

    user_service --> user_db
    workout_service --> workout_db
    logging_service --> logging_db
```
