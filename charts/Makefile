build:
	-helm install timescaledb timescaledb-multinode -n timescaledb
	-/usr/local/bin/kubectl get all -n timescaledb

clean:
	-helm uninstall timescaledb timescaledb-multinode -n timescaledb
	-/usr/local/bin/kubectl get all -n timescaledb

install-grafana:
	-ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null
	-brew install grafana
	-brew update
	-brew install grafana
	-brew tap homebrew/services
	-brew services start grafana

port-forward:
	-kubectl -n timescaledb port-forward service/timescaledb 5432:5432

sql-statements:
	-CREATE DATABASE timeseries;
	-\c timeseries
	-CREATE EXTENSION IF NOT EXISTS timescaledb CASCADE;
	-CREATE TABLE conditions (time        TIMESTAMP WITH TIME ZONE NOT NULL,device_id   TEXT,temperature  NUMERIC,humidity     NUMERIC);
	-SELECT create_hypertable('conditions', 'time');
	-INSERT INTO conditions(time, device_id, temperature, humidity) VALUES (NOW(), 'weather-pro-000000', 84.1, 84.1);
	-INSERT INTO conditions VALUES (NOW(), 'weather-pro-000002', 71.0, 51.0), (NOW(), 'weather-pro-000003', 70.5, 50.5), (NOW(), 'weather-pro-000004', 70.0, 50.2);
	-INSERT INTO conditions VALUES (NOW(), 'weather-pro-000002', 70.1, 50.1) RETURNING *;
	-SELECT * FROM conditions LIMIT 10;

