# architect-functions-python

Python runtime support for Architect provisioned AWS Lambda functions


## Install

```bash
cd path/to/lambda
pip install --target ./vendor architect-functions
```

## API

```python
# example lambda function
import json
import arc

def handler(event, context):
  return {'body': json.dumps(arc.reflect())}
```

### `arc`

`arc.reflect` returns a dict of the the current AWS resources.

Example output:
```
{
  "events": {
    "ping": "arn:aws:sns:us-east-1:555:TestStaging-PingTopic-11111111111",
  },
  "queues": {
    "continuum": "https://sqs.us-east-1.amazonaws.com/555/TestStaging-ContinuumQueue-8888888888"
  },
  "static": {
    "bucket": "teststaging-staticbucket-11111111",
    "fingerprint": "false"
  },
  "tables": {
    "noises": "TestStaging-NoisesTable-111111111"
  },
  "ws": {
    "https": "https://xxx.execute-api.us-east-1.amazonaws.com/production/@connections",
    "wss": "wss://xxx.execute-api.us-east-1.amazonaws.com/production"
  }
}
```

### `arc.http`
- `arc.http.session_read()`
- `arc.http.session_write()`

### `arc.ws`
- `arc.ws.send(id, payload)`

### `arc.events`
- `arc.events.publish(name, payload)`

### `arc.queues`
- `arc.queues.publish(name, payload)`

### `arc.tables`
- `arc.tables.name(tablename)`

---

## Development

Install [Pipenv](https://pipenv.pypa.io/en/latest/#install-pipenv-today)

```bash
pipenv install --dev
```

---

## Testing

```bash
pipenv run pytest
```

### Releasing

```bash
python3 setup.py sdist
```

```bash
twine upload dist/*
```

