## Project structure example

> Example is by the https://github.com/geisonbiazus/blog/tree/main
> Note: the project holds only some of the folders and files just to demonstrate how applying the concepts of clean architecture could divide the app into the separate parts.

- **cmd** — Contains the main file for the delivery mechanism (web). deployment — Deployment scripts.
    - **web** *main.go* (calls app.NewContext(), heart of the app)

- **internal** — The *most important folder*, contains the implementation of all the layers and components.
    - *adapters*
        - cache
        - userrepo
            - memory
            - postgres
            - user_repo.go (CONSTRUCTOR)
        - oauth2provider
            - fake
            - github
            - oauth_2_provider.go (CONSTRUCTOR)
        - tokencoder
            - jwt
            - token_encoder.go (CONSTRUCTOR)
        - publisher
        - pubsub
            - memory
                - pubsub.go
                - pubsub_test.go
            - pubsub.go (CONSTRUCTOR)
        - idgenerator
            - fake
            - id_generator
            - id_generator.go (CONSTRUCTOR)
        - transactionmanager
            - postgres
            - fake
        - commentrepo
            - memory
            - postgres
            - comment_repo.go (CONSTRUCTOR)
    - *app*
        - context.go
    - *core*
        - auth
            - (usecases, entities, ports)
        - blog
            - entities.go
            - ports.go
            - view_post_use_case.go
            - view_post_use_case_test.go
            - list_posts_use_case.go
            - list_posts_use_case_test.go
        - discussion
            - (usecases, entities, ports)
        - shared
            - entities.go (e.g. Event struct)
            - ports.go (e.g. TransactionManager interface)
    - *ui*
        - web
            - handlers
                - list_post_handler.go
                - list_post_handler_test.go
                - log_handler.go
                - log_handler_test.go
                - template_handler.go
                - template_handler_test.go
                - ...
            - lib
                - template_renderer.go
            - ports
            - test
            - router.go
            - server.go
        - subscriptions

- **pkg** — Project independent packages with the intention of” extending” the language. Each one of these packages could be released as a standalone library.
    - dbrepo
    - migration
    - testhelper

- **posts/filestore** — Specific for this project. This is where the written posts using markdown are stored.
    - // storage place

- **test** — Contains integration tests and other test assets.
    - integration (api)
    - posts

- **web** — Web-related stuff like templates and static files.
