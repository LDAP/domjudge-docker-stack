# DOMJUDGE docker-compose

THIS IS MENT FOR LOCAL TESTING!

## Usage

- Change the DB_PASS variable in the .env file
- Start the stack using

```
docker-compose up
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
docker-compose down
docker-compose up
```

