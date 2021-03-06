# prometheus-http-sd

Prometheus service discovery using with HTTP API and `file_sd_config`.

## Usage

```
./prometheus-http-sd --api.url="http://api.example.com/service_discovery.json" --output.file=/path/to/http_sd.json --refresh.interval=60
```

## HTTP API format

HTTP API response should be follow prometheus `file_sd_config` format like below:

```json
[
	{
		"targets": [
			"192.0.2.1:8080",
			"192.0.2.2:8080",
		],
		"labels": {
			"service": "web",
			"role": "role-1"
		}
	},
	{
		"targets": [
			"192.0.3.1:3306"
		],
		"labels": {
			"service": "db",
			"role": "role-2"
		}
	}
]
```

## Example prometheus settings

The part of your `prometheus.yml` is probably as follows.

```
  scrape_configs:
    - job_name: 'http_sd'
      file_sd_configs:
        - files:
          - /path/to/http_sd.json
```
