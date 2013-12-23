## Running web2Py on Heroku

Rapid web development <> Rapid web deployment.

### Steps

1. Download web2py: [http://www.web2py.com/examples/static/web2py_src.zip](http://www.web2py.com/examples/static/web2py_src.zip)
2. After you create your app, edit "db.py":

  replace -

  ```python
  if not request.env.web2py_runtime_gae:
      ## if NOT running on Google App Engine use SQLite or other DB
      db = DAL('sqlite://storage.sqlite',pool_size=1,check_reserved=['all'])
  ```

  with -


  ```python
  if not request.env.web2py_runtime_gae:
      ## if NOT running on Google App Engine use SQLite or other DB
      try: db = DAL(os.environ.get('DATABASE_URL'))
      except: db = DAL('sqlite://storage.sqlite',pool_size=1,check_reserved=['all'])
  ```

3. Run the deploy script from main web2py directory:
```shell
$ sh web2py-heroku.sh
```

> If you need to access to the admin, you will have to add a SSL certificate - https://addons.heroku.com/ssl


Enjoy.

### Examples

1. [Hello, World!](http://desolate-sea-4381.herokuapp.com/)
