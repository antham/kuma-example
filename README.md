
## Install

Run all commands in the current folder. 

Start the control plane :
Build first `docker-compose build` then run it with `docker-compose up control-plane`

Then generate the tokens for dataplanes in the `dataplane-config/tokens` folder:
Run `docker-compose exec control-plane generate-dataplane-token`

In 2 separated terminals run:
`docker-compose run service1`
`docker-compose run service2`

The address of the container is injected automatically in the dataplane config.

At this point we get 2 dataplanes running with the control plane but no services listening.

To start the example service run in a new terminal:
`docker-compose exec service1 service-with-healthcheck 127.0.0.1:8000`

Then you can request the service through the other datplane with: 
`docker-compose exec service2 curl 127.0.0.1:9000`
