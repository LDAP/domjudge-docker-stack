# DomJudge docker-stack

DOMJUDGE WEB SERVICE BINDS TO 0.0.0.0:PORT! CONFIGURE A PROPER FIREWALL TO RESTRICT ACCESS!

## Usage

- Change the DB_PASS variable in the .env file
- Start the stack using

```
docker swarm init
docker stack deploy -c <(docker-compose -f docker-compose.yml config) DomJudge
# Monitor logs
docker service logs -f DomJudge_domserver 
```

- Wait until the domserver connects to the database and displays:

```
domserver_1  | Initial admin password is XXXXXXXXXX
domserver_1  | 
domserver_1  | Initial judgehost password is XXXXXXXXXXXXX
```

- Copy the judgehost password to JUDGE_PASS in the .env file
- Log in via admin password and user admin
- Change the admin password
- _THEN_ restart with

```
# Stop the stack
docker stack rm DomJudge
# Restart
docker stack deploy -c <(docker-compose -f docker-compose.yml config) DomJudge
```

## Advanced

- Set the number of JudgeHosts
```
docker service scale Domjudge_judge=number
```
- Add nodes to the swarm: This distributes the judgehosts along the nodes (rescaling may be needed)
```
# Retrieve the join command for a worker (on the manager)
docker swarm join-token worker
# Add the node (on the worker)
docker swarm join --token <token> IP:Port
```
- Set the data path  
    Edit the PATH Variable in the .env file
