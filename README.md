# Example Docker Compose project for Telegraf, InfluxDB and Grafana

This an example project to show the TIG (Telegraf, InfluxDB and Grafana) stack.

## Start the stack with docker compose

```bash
$ docker-compose up
```

## Services and Ports

### Grafana
- URL: http://localhost:3000 
- User: admin 
- Password: admin 

### Telegraf
- Port: 8125 UDP (StatsD input)

### InfluxDB
- Port: 8086 (HTTP API)
- User: admin 
- Password: admin 
- Database: influx


Run the influx client:

```bash
$ docker-compose exec influxdb influx -execute 'SHOW DATABASES'
```

Run the influx interactive console:

```bash
$ docker-compose exec influxdb influx

Connected to http://localhost:8086 version 1.8.0
InfluxDB shell version: 1.8.0
>
```

The telegraf agents aggregates the incoming data and perodically persists the data into the InfluxDB database.

Grafana connects to the InfluxDB database and is able to visualize the incoming data.


Download telegraf:
```
brew update && brew install telegraf
```
Create telegraf config:
```
telegraf -sample-config --input-filter cpu:mem:net:disk:diskio:hddtemp --output-filter influxdb > telegraf.conf
```
Run telegraf:
```
brew services start telegraf |  brew services restart telegraf
```
Run docker-compose.yml:
```
docker-compose up -d
```
