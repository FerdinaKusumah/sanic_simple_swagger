# Sanic OpenAPI
Real project in [https://github.com/huge-success/sanic-openapi](https://github.com/huge-success/sanic-openapi/blob/master/README.md)

This project just extends functional and fix some bugs
![Example Swagger UI](https://raw.githubusercontent.com/huge-success/sanic-openapi/master/images/code-to-ui.png "Swagger UI")

## Installation
```shell
pip install sanic-simple-swagger
```

#### Add OpenAPI and Swagger UI:
```python
from sanic_simple_swagger import swagger_blueprint, openapi_blueprint
app.blueprint(openapi_blueprint)
app.blueprint(swagger_blueprint)
```

You'll now have a Swagger UI at the URL `/swagger/index.html`.

Your routes will be automatically categorized by their blueprints.

## Example
```python
from sanic_simple_swagger import doc

@student.get('/student', strict_slashes=True)
@doc.summary("Show resource")
@doc.description("Display a listing of the resource.")
@doc.deprecated(True) #if the api is deprecated
@doc.produces(schema={'type': "object", 'additionalProperties': {'type': 'string', 'format': 'string'}}, status=200, description='Success result', content_type='application/json')
@doc.consumes({'name': str}, location='query', description='Student name', example={'name': 'john'})
async def index(request):
    ...

@student.post('/student', strict_slashes=True)
@doc.summary("Create resource")
@doc.description("Store a newly created resource in storage.")
@doc.consumes({'name': str}, location='body', description='Student name', example={'name': 'John meyer'}, required=True)
@doc.consumes({'address': str}, location='body', description='Student address', example={'address': 'San Francisco, CA 94109 hone : (301) 916-0860'}, required=True)
async def store(request):
    ...

@student.put('/student/<id>', strict_slashes=True)
@doc.summary("Update resource")
@doc.description("Update the specified resource in storage.")
async def update(request, id):
    ...

@student.delete('/student/<id>', strict_slashes=True)
@doc.summary("Remove resource")
@doc.description("Remove the specified resource from storage.")
async def delete(request, id):
    ...
```

### Configure all the things

```python
app.config['API_VERSION'] = '1.0.0'
app.config['API_TITLE'] = 'Swagger Petstore'
app.config['API_DESCRIPTION'] = 'This is a sample server Petstore server. You can find out more about Swagger at [http://swagger.io](http://swagger.io) or on [irc.freenode.net, #swagger](http://swagger.io/irc/). For this sample, you can use the api key `special-key` to test the authorization filters.'
app.config['API_TERMS_OF_SERVICE'] = 'http://swagger.io/terms/'
app.config['API_CONTACT_EMAIL'] = 'http://swagger.io/terms/'
app.config['API_LICENSE_NAME'] = 'Apache 2.0'
app.config['API_LICENSE_URL'] = 'http://www.apache.org/licenses/LICENSE-2.0.html'
app.config['schemes'] = ['http', 'https']
```

## Reference
1. [Sanic](https://github.com/huge-success/sanic)
2. [Sanic OpenAPI](https://github.com/huge-success/sanic-openapi)