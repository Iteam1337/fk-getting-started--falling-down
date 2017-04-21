# Falling down

## Conference system

1. Schedule
2. Statistics/Logging
3. Dispatch (pick up speakers at the airport)

(Kill the dispatcher)
(Send a few pickup messages)

## Started vs listening

- Connections
- Solution
  - Build for retrying
  - Connect script at start-up for migrations and such

## Secrets

- Google apps key
  - .env
- Production secrets and certificates
  - Create certificate at build time and store in secret container
  - Vendors have solutions
    - Open Shift
    - Docker Swarm
    - Azure KeyVault
    - Vault from HashiCorp
- DON'T COPY/PASTE docker-compose INTO PRODUCTION!
  - DON'T COPY/PASTE docker-compose INTO PRODUCTION!

## Works on my machine

- Missing configuration
  - Setting up environments is not done every day and should not be rushed
  - Never trust your edited config - test it
- Non configured stuff - it works as long as it's on localhost
  - See above
  - Don't spread config values around your app
  - Test on CI
- DB and data volume must be on the same machine
  - Because reasons

## Versions

- Running :latest in production
  - Rollback = checkout hash + rebuild or reset master to create a new :latest
  - Compatibility of services
  - No history
- Running :latest in production - dependencies edition
  - Works on my machine
  - Putting someones code into production unchecked
- Solution
  - Tagging a release `docker build -t "some:$(git tag)" .`
  - Set specific versions on dependencies

## Who the f* knows Python?

- Just because you can doesn't mean you should
- Make sure the team knows the stack

## Monitoring

- Oh, look! The dispatcher died! Lets restart it :)
- Resilient, recoverable services tend to die in silence
- Recovering a service is not good enough if the events have expired
  - Monitor critical services and make sure they can be recovered easily
  - Use an orchestration thingy
    - Kubernetes

## Onboarding

- Clone four repos
- Install everything
- Edit the docker-compose to not run the stuff you're working on
- Change all the links
- Cry a bit
- Give up
- Solution
  - Tagged images
