## Steps for Running web2Py on Heroku

1. Download web2py: [http://www.web2py.com/examples/static/web2py_src.zip](http://www.web2py.com/examples/static/web2py_src.zip)
2. After you create your app, edit "db.py".

  Replace:

  ```python
  if not request.env.web2py_runtime_gae:
      ## if NOT running on Google App Engine use SQLite or other DB
      db = DAL('sqlite://storage.sqlite',pool_size=1,check_reserved=['all'])
  ```

  with

  ```python
  if not request.env.web2py_runtime_gae:
      ## if NOT running on Google App Engine use SQLite or other DB
      try: db = DAL(os.environ.get('DATABASE_URL'))
      except: db = DAL('sqlite://storage.sqlite')
  ```

3. Run script from main web2py directory:
```shell
$ sh web2py-heroku.sh
```

if you need to access the admin, you will have to add a SSL certificate - https://addons.heroku.com/ssl


Enjoy.
