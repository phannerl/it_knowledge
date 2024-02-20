Object Relational Mapping (ORM) 
  - A technique used in creating a "bridge" between object-oriented programs and, in most cases, relational databases.
  - Put another way, you can see the ORM as the layer that connects object oriented programming (OOP) to relational databases.
  => Use ORMs and prepared statements to avoid SQL injections

A prepared statement            
  - Sent once to the database as a template with no values. It gets compiled and optimized by the database.
  - parameters are bound to that template with a different protocol. The statement can then be executed multiple times with high efficiency.
  => SQL injections cannot occur when using prepared statements
  - Django has its own ways of protecting from SQL injection (as noted in the docs https://docs.djangoproject.com/en/3.0/topics/security/#sql-injection-protection).
  - Reddit: https://www.reddit.com/r/django/comments/ffhr15/does_django_use_prepared_statements_to_execute/

Advantages of the ORM     
  - Hides and encapsulates changes in the data source 
  - Developers don't have to write any additional low-level code
  - Makes it easier and more cost-effective to maintain the application over time 

Disadvantages of the ORM  
  - Lead to an erosion in application speed and performance due to the extra code that is generated for abstraction.
  - In some cases, depending on ORM might result in poorly designed databases and make it harder to maintain applications.
  - Incorrect mapping between data tables and objects can also create application problems that may be difficult to recognize and can affect overall performance.
  - if the ORM layer is poorly written, it can become difficult to improve data schemas and to manage database migrations.

ORM tools 
  - Django        
    - Suitable for building web applications quickly.
    - Can interact with application data from many relational databases, including SQLite, PostgreSQL and MySQL.
  - SQLAlchemy    
    - Provides persistence patterns to speed up database access.
    - Declarative Mapping structure defines both a Python object model and database metadata that describes real SQL tables in a database.
