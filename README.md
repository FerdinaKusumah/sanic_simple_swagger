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

class Student:
    name = str
    address = str

@student.get('/student', strict_slashes=True)
@doc.summary("Show resource")
@doc.description("Display a listing of the resource.")
@doc.deprecated(True) #if the api is deprecated
@doc.produces(content_type='application/json')
@doc.consumes({'name': str}, location='query', description='Student name', example={'name': 'john'})
async def index(request):
    ...

@student.post('/student', strict_slashes=True)
@doc.summary("Create resource")
@doc.description("Store a newly created resource in storage.")
@doc.consumes(Student, location='body' required=True)
@doc.response_success(status=201, description='If successful created')
async def store(request):
    ...

@student.put('/student/<id>', strict_slashes=True)
@doc.summary("Update resource")
@doc.description("Update the specified resource in storage.")
@doc.response_success(status=201, description='If successful updated')
async def update(request, id):
    ...

@student.delete('/student/<id>', strict_slashes=True)
@doc.summary("Remove resource")
@doc.description("Remove the specified resource from storage.")
@doc.response_success(status=201, description='If successful deleted')
async def delete(request, id):
    ...
```

### Configure all the things

```python
app.config['API_VERSION'] = '1.0.0'
app.config['API_TITLE'] = 'Swagger student API'
app.config['API_DESCRIPTION'] = 'This is a sample server Student api.'
app.config['API_TERMS_OF_SERVICE'] = ...
app.config['API_CONTACT_EMAIL'] = ...
app.config['API_LICENSE_NAME'] = 'Apache 2.0'
app.config['API_LICENSE_URL'] = 'http://www.apache.org/licenses/LICENSE-2.0.html'
app.config['schemes'] = ['http', 'https']
```

## Reference
1. [Sanic](https://github.com/huge-success/sanic)
2. [Sanic OpenAPI](https://github.com/huge-success/sanic-openapi)