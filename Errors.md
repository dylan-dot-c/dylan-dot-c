**Errors MD**

Python Flask
Route not found 404
issue was due to having another server running on the same port
so it rendered the first one instead  asds


**Flask**
Circular Import Error
when using bluepirnts and login make sure that you do everything sequentially

```python
from flask import Flask
from config import Config
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate
from flask_login import LoginManager
app = Flask(__name__)
# setting project config to app.config
app.config.from_object(Config)
login = LoginManager()
login.login_view = 'login'
login.init_app(app)
db = SQLAlchemy(app)
migrate = Migrate(app, db)
from app.blueprints.api import api 
app.register_blueprint(api)
# importing routes and forms so they can be used and access 
from . import routes, models
from . import forms

```
Previous Code
```python
from flask import Flask
from config import Config
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate
from flask_login import LoginManager
app = Flask(__name__)
# setting project config to app.config
app.config.from_object(Config)
db = SQLAlchemy(app)
migrate = Migrate(app, db)
from app.blueprints.api import api 
app.register_blueprint(api)
login = LoginManager()
login.login_view = 'login'
login.init_app(app)
# importing routes and forms so they can be used and access 
from . import routes, models
from . import forms

```

So the error was that after I register the blueprints I setup login but I had to seup login first then blueprints
Since it was saying some circular import error

