# Flask-Restdoc v0.0.1

Flask-Restdoc is a simple tool that generates RESTful API documentation automatically from python files.

<br />


## How-to

### Step 1. Make Restdoc Instance

First, you need to make an instance of `Restdoc`.

```
from flask import Flask
from restdoc import Restdoc

app = Flask(__name__)

restdoc = Restdoc(app)
```

Or you can initiate app later.

```
restdoc.init_app(app)
```

<br />

### Step 2. Configuration Output Path

You have to set output path at `app.config`. Path must includes output file name.

```
app.config['RESTDOC_OUTPUT'] = '/Users/xoul/Documents/api.md'
```

<br />

### Step 3. Decorate URL Endpoints

In your view.py (or something else), add decorators to url endpoints.

```
api = Blueprint('api', __name__)

@restdoc.api(api,
	description='asdasd',
	params=[
		('email', True),
		('password', True, 'SHA-1')
	],
	status=200,
	sample_response={
		'status': 'ok'
	},
	errors=[1001,1002])
@api.route('/login')
def login():
	pass
```

#### Parameters

##### blueprint

A blueprint object.


##### description

API description string.


##### params

URL Parameters or form data for request. List of tuple contains parameter name, required option(True if required) and description.


##### status

A HTTP status code for successful request. 200 is default.


##### sample_response

A sample response object. This will be written in JSON format.


##### errors

Error codes that can be occurred in this function.


<br />

### Step 4. Error Definition List (Optional)

Flask-Restdoc generates error information from error definition list. You have to make a list of error definitions. Each error object is tuple that contains HTTP status code, error code and message.

```
errors = [
	# (HTTP status, Error code, Message)
	(403,	1001,	'NOT_AUTHORIZED'),
	(400,	1100,	'NEED_EMAIL'),
	(400,	1101,	'NEED_PASSWORD')
]
```

Then, set error definition list to `restdoc` instance.

```
restdoc.set_errors(errors)
```

<br />

### Step 5. Generate

Just call method `generate` to generate documentation.

```
restdoc.generate()
```

<br />

## Sample Documentation

You can see sample  documentation here: [Sample REST API Documentation](https://github.com/devxoul/flask-restdoc/blob/master/sample.md)