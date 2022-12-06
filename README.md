### Many2one & One2Many
En el contexto de Odoo, many2one y one2many son dos tipos de campos de relación que se utilizan para establecer relaciones entre diferentes modelos de datos.

Un campo many2one se utiliza para establecer una relación de muchos a uno entre dos modelos de datos. Por ejemplo, si tienes un modelo de datos que representa a los clientes de una empresa y otro que representa a las órdenes de compra de esa empresa, podrías utilizar un campo many2one en el modelo de órdenes de compra para relacionar cada orden de compra con un cliente específico. De esta manera, cada orden de compra puede tener asociado un solo cliente, pero cada cliente puede estar relacionado con varias órdenes de compra.

Por otro lado, un campo one2many se utiliza para establecer una relación de uno a muchos entre dos modelos de datos. Por ejemplo, si sigues con el mismo ejemplo anterior, podrías utilizar un campo one2many en el modelo de clientes para relacionar cada cliente con sus órdenes de compra. De esta manera, cada cliente puede estar relacionado con varias órdenes de compra, pero cada orden de compra solo puede estar relacionada con un solo cliente.

En resumen, un campo many2one se utiliza para establecer una relación de muchos a uno entre dos modelos de datos, mientras que un campo one2many se utiliza para establecer una relación de uno a muchos. Ambos campos son útiles para organizar y relacionar diferentes modelos de datos en Odoo.

Para utilizar los campos many2one y one2many en Odoo, primero debes declararlos en el modelo de datos al que quieres agregarlos. Por ejemplo, si quieres agregar un campo many2one y un campo one2many al modelo de clientes, podrías agregar las siguientes líneas de código:
```python
class Customer(models.Model):
    _name = 'customer'

    name = fields.Char()
    email = fields.Char()
    phone = fields.Char()

    # many2one field
    orders = fields.Many2one('sale.order', string='Orders')

    # one2many field
    invoices = fields.One2many('account.invoice', 'customer_id', string='Invoices')

```
En este ejemplo, se ha declarado un modelo de datos llamado Customer que tiene tres campos de tipo Char (name, email y phone) y dos campos de relación: un campo many2one llamado orders que se relaciona con el modelo de datos sale.order, y un campo one2many llamado invoices que se relaciona con el modelo de datos account.invoice.

Para utilizar estos campos en la interfaz de usuario de Odoo, debes agregar los campos correspondientes a la vista del formulario del modelo de clientes. Por ejemplo, podrías agregar las siguientes líneas de código a la vista del formulario del modelo de clientes para mostrar los campos orders y invoices:
```xml
<form string="Customer" class="oe_form">
    <field name="name"/>
    <field name="email"/>
    <field name="phone"/>
    <field name="orders" widget="many2one" options="{'no_open': True}"/>
    <field name="invoices" widget="one2many"/>
</form>
```
En este ejemplo, se ha añadido un campo orders que utiliza el widget many2one para mostrar la relación con el modelo sale.order, y un campo invoices que utiliza el widget one2many para mostrar la relación con el modelo account.invoice.

Estos son solo ejemplos básicos de cómo utilizar los campos many2one y one2many en Odoo. Para obtener más información sobre cómo utilizar estos campos y otros aspectos de desarrollo en Odoo, puedes consultar la documentación oficial de Odoo o buscar tutoriales y recursos en línea.

### Como se usa domain en one2many odoo
En Odoo, el atributo domain se utiliza para especificar una condición que debe cumplirse para que un registro se muestre en un campo one2many. Por ejemplo, si quieres mostrar solo las órdenes de compra que estén en estado "Pendiente" en un campo one2many, podrías utilizar el atributo domain de la siguiente manera:
```xml
<form string="Customer" class="oe_form">
    <field name="name"/>
    <field name="email"/>
    <field name="phone"/>
    <field name="orders" widget="one2many" domain="[('state', '=', 'pending')]"/>
</form>
```
En este ejemplo, se ha añadido un campo one2many llamado orders que utiliza el widget one2many para mostrar la relación con el modelo sale.order. Además, se ha utilizado el atributo domain para especificar que solo se deben mostrar las órdenes de compra cuyo campo estado tenga el valor "Pendiente".

El atributo domain se utiliza en muchas situaciones en Odoo, no solo en campos one2many. Puedes utilizarlo para filtrar los datos que se muestran en una vista, para especificar las condiciones de una búsqueda avanzada, etc. Para obtener más información sobre cómo utilizar el atributo domain en Odoo, puedes consultar la documentación oficial o buscar tutoriales y recursos en línea.

### Como se usa domain en one2many odoo en el modelo
Si quieres utilizar el atributo domain en un campo one2many en el modelo de datos de Odoo, debes agregarlo a la declaración del campo en el modelo. Por ejemplo, si quieres agregar un campo one2many al modelo de clientes que muestre solo las órdenes de compra que estén en estado "Pendiente", podrías agregar las siguientes líneas de código al modelo de clientes:
```python
class Customer(models.Model):
    _name = 'customer'

    name = fields.Char()
    email = fields.Char()
    phone = fields.Char()

    # one2many field with domain
    orders = fields.One2many('sale.order', 'customer_id', string='Orders', domain="[('state', '=', 'pending')]")
```
En este ejemplo, se ha declarado un campo one2many llamado orders que se relaciona con el modelo sale.order. Además, se ha utilizado el atributo domain para especificar que solo se deben mostrar las órdenes de compra cuyo campo estado tenga el valor "Pendiente".

Para utilizar este campo en la interfaz de usuario de Odoo, debes agregarlo a la vista del formulario del modelo de clientes. Por ejemplo, podrías agregar las siguientes líneas de código a la vista del formulario del modelo de clientes para mostrar el campo orders:
```xml
<form string="Customer" class="oe_form">
    <field name="name"/>
    <field name="email"/>
    <field name="phone"/>
    <field name="orders" widget="one2many"/>
</form>
```
En este ejemplo, se ha añadido un campo one2many llamado orders que utiliza el widget one2many para mostrar la relación con el modelo sale.order. Como el atributo domain se ha especificado en la declaración del campo en el modelo, solo se mostrarán las órdenes de compra que cumplan la condición especificada en el atributo domain.

Estos son solo ejemplos básicos de cómo utilizar el atributo domain en un campo one2many en el modelo de datos de Odoo. Para obtener más información sobre cómo utilizar este atributo y otros aspectos de desarrollo en Odoo, puedes consultar la documentación oficial o buscar tutoriales y recursos en línea.

### Como se usa context en one2many odoo en el modelo
En Odoo, el atributo context se utiliza para pasar información adicional a una vista o un campo de un modelo de datos. En el contexto de un campo one2many, el atributo context se puede utilizar para especificar información adicional que se debe utilizar para mostrar los datos del campo.

Por ejemplo, si quieres mostrar solo las órdenes de compra que estén en estado "Pendiente" en un campo one2many, podrías utilizar el atributo context de la siguiente manera:
```python
class Customer(models.Model):
    _name = 'customer'

    name = fields.Char()
    email = fields.Char()
    phone = fields.Char()

    # one2many field with context
    orders = fields.One2many('sale.order', 'customer_id', string='Orders', context="{'default_state': 'pending'}")
```
En este ejemplo, se ha declarado un campo one2many llamado orders que se relaciona con el modelo sale.order. Además, se ha utilizado el atributo context para especificar que se deben mostrar solo las órdenes de compra cuyo campo estado tenga el valor "Pendiente".

Para utilizar este campo en la interfaz de usuario de Odoo, debes agregarlo a la vista del formulario del modelo de clientes. Por ejemplo, podrías agregar las siguientes líneas de código a la vista del formulario del modelo de clientes para mostrar el campo orders:
```xml
<form string="Customer" class="oe_form">
    <field name="name"/>
    <field name="email"/>
    <field name="phone"/>
    <field name="orders" widget="one2many"/>
</form>
```
En este ejemplo, se ha añadido un campo one2many llamado orders que utiliza el widget one2many para mostrar la relación con el modelo sale.order. Como el atributo context se ha especificado en la declaración del campo en el modelo, solo se mostrarán las órdenes de compra que cumplan la condición especificada en el atributo context.

Estos son solo ejemplos básicos de cómo utilizar el atributo context en un campo one2many en el modelo de datos de Odoo. Para obtener más información sobre cómo utilizar este atributo y otros aspectos de desarrollo en Odoo, puedes consultar la documentación oficial o buscar tutoriales y recursos en línea.

### Como se usa context y domain en one2many odoo en el modelo
En Odoo, el atributo context y el atributo domain se pueden utilizar juntos en un campo one2many para especificar condiciones y pasar información adicional que se debe utilizar para mostrar los datos del campo.

Por ejemplo, si quieres mostrar solo las órdenes de compra que estén en estado "Pendiente" y que tengan un importe mayor a 100 en un campo one2many, podrías utilizar el atributo context y el atributo domain de la siguiente manera:
```python
class Customer(models.Model):
    _name = 'customer'

    name = fields.Char()
    email = fields.Char()
    phone = fields.Char()

    # one2many field with context and domain
    orders = fields.One2many('sale.order', 'customer_id', string='Orders', context="{'default_state': 'pending'}", domain="[('amount_total', '>', 100)]")
```
En este ejemplo, se ha declarado un campo one2many llamado orders que se relaciona con el modelo sale.order. Además, se ha utilizado el atributo context para especificar que se deben mostrar solo las órdenes de compra cuyo campo estado tenga el valor "Pendiente", y se ha utilizado el atributo domain para especificar que solo se deben mostrar las órdenes de compra cuyo campo importe_total sea mayor a 100.

Para utilizar este campo en la interfaz de usuario de Odoo, debes agregarlo a la vista del formulario del modelo de clientes. Por ejemplo, podrías agregar las siguientes líneas de código a la vista del formulario del modelo de clientes para mostrar el campo orders:
```xml
<form string="Customer" class="oe_form">
    <field name="name"/>
    <field name="email"/>
    <field name="phone"/>
    <field name="orders" widget="one2many"/>
</form>
```
En este ejemplo, se ha añadido un campo one2many llamado orders que utiliza el widget one2many para mostrar la relación con el modelo sale.order. Como el atributo context y el atributo domain se han especificado en la declaración del campo en el modelo, solo se mostrarán las órdenes de compra que cumplan las condiciones especificadas en ambos atributos.

Estos son solo ejemplos básicos de cómo utilizar el atributo context y el atributo domain en un campo one2many en el modelo de datos de Odoo. Para obtener más información sobre cómo utilizar estos atributos y otros aspectos de desarrollo en Odoo, puedes consultar la documentación oficial o buscar tutoriales y recurs

### Ejemplo uso one2many y many2one en odoo con el modulo nave espacial
El módulo de nave espacial en Odoo es un ejemplo ficticio que no existe realmente. Sin embargo, puedes utilizar los campos many2one y one2many en Odoo para modelar un sistema de gestión de naves espaciales de la siguiente manera:
```python
class Spacecraft(models.Model):
    _name = 'spacecraft'

    name = fields.Char()
    manufacturer = fields.Char()
    model = fields.Char()

    # many2one field
    captain = fields.Many2one('res.partner', string='Captain')

    # one2many field
    crew = fields.One2many('res.partner', 'spacecraft_id', string='Crew')
```
En este ejemplo, se ha declarado un modelo de datos llamado Spacecraft que tiene tres campos de tipo Char (name, manufacturer y model) y dos campos de relación: un campo many2one llamado captain que se relaciona con el modelo de datos res.partner, y un campo one2many llamado crew que se relaciona con el mismo modelo res.partner.

Para utilizar estos campos en la interfaz de usuario de Odoo, debes agregar los campos correspondientes a la vista del formulario del modelo de naves espaciales. Por ejemplo, podrías agregar las siguientes líneas de código a la vista del formulario del modelo de naves espaciales para mostrar los campos captain y crew:
```xml
<form string="Spacecraft" class="oe_form">
    <field name="name"/>
    <field name="manufacturer"/>
    <field name="model"/>
    <field name="captain" widget="many2one" options="{'no_open': True}"/>
    <field name="crew" widget="one2many"/>
</form>
```
En este ejemplo, se ha añadido un campo many2one llamado captain que utiliza el widget many2one para mostrar la relación con el modelo res.partner, y un campo one2many llamado crew que utiliza el widget one2many para mostrar la relación con el mismo modelo res.partner.

### Campos calculados
En Odoo, los campos calculados son aquellos campos que no se almacenan en la base de datos, sino que se calculan a partir de otros campos del modelo de datos. Estos campos se utilizan para mostrar información derivada o agregada que puede ser útil para los usuarios de la aplicación, pero que no necesita ser almacenada de forma permanente en la base de datos.

Por ejemplo, si un modelo de datos tiene campos para almacenar el precio y la cantidad de un producto, se puede crear un campo calculado llamado total que calcule el precio total multiplicando el precio por la cantidad. De esta manera, el usuario puede ver el precio total de un producto en el formulario sin necesidad de calcularlo manualmente.

Para declarar un campo calculado en un modelo de datos de Odoo, se utiliza la clase fields.Compute y se especifica la función que se utilizará para calcular el valor del campo. 
Por ejemplo:
```python
class Product(models.Model):
    _name = 'product'

    name = fields.Char()
    price = fields.Float()
    quantity = fields.Integer()

    # computed field
    total = fields.Compute('_compute_total', store=True)

    def _compute_total(self):
        for record in self:
            record.total = record.price * record.quantity
```
En este ejemplo, se ha declarado un campo calculado llamado total que se calcula mediante la función _compute_total. La función recorre cada registro del modelo y calcula el valor del campo total multiplicando el precio por la cantidad.

Para obtener más información sobre cómo declarar y utilizar campos calculados en Odoo, puedes consultar la documentación oficial o buscar tutoriales y recursos en línea.

### Campos calculados: Searching, readonly & Multiplace
En Odoo, los campos calculados pueden tener diferentes opciones que afectan su comportamiento y uso. Algunas de estas opciones comunes son:

**searching:** Especifica si el campo puede ser utilizado para realizar búsquedas en la base de datos. Si se establece en True, el campo se incluirá en la lista de campos disponibles para realizar búsquedas en la interfaz de usuario de Odoo.<br />
**readonly:** Especifica si el campo es de solo lectura. Si se establece en True, el usuario no podrá editar el valor del campo en la interfaz de usuario.<br />
**multiple:** Especifica si el campo puede tener múltiples valores. Si se establece en True, el campo se mostrará como una lista de valores en la interfaz de usuario, en lugar de como un único valor.<br />
Por ejemplo, si un modelo de datos tiene un campo calculado llamado total que se calcula a partir del precio y la cantidad de un producto, se puede declarar de la siguiente manera:
```python
class Product(models.Model):
    _name = 'product'

    name = fields.Char()
    price = fields.Float()
    quantity = fields.Integer()

    # computed field
    total = fields.Compute('_compute_total', store=True, search=True, readonly=True)

    def _compute_total(self):
        for record in self:
            record.total = record.price * record.quantity
```
En este ejemplo, el campo calculado total se declara con las opciones `search=True` y `readonly=True`, lo que significa que el campo se puede utilizar para realizar búsquedas en la base de datos

### Campos pseudo-relacionales
En Odoo, los campos pseudo-relacionales son campos especiales que se utilizan para mostrar información de otro modelo de datos sin establecer una relación explícita entre ambos modelos. Estos campos se utilizan principalmente para mostrar información de un modelo secundario de forma sencilla y rápida, sin tener que crear campos many2one o one2many. </br>

Por ejemplo, si un modelo de datos tiene un campo para almacenar el ID de un usuario, se puede utilizar un campo pseudo-relacional para mostrar el nombre del usuario asociado al ID sin tener que crear un campo many2one con el modelo res.users.</br>

Para declarar un campo pseudo-relacional en un modelo de datos de Odoo, se utiliza la clase fields.Reference y se especifica el modelo secundario con el el que se relaciona. </br>
Por ejemplo:
```python
class Task(models.Model):
    _name = 'task'

    name = fields.Char()
    description = fields.Text()

    # pseudo-relational field
    user_id = fields.Reference('res.users', 'User')
```
En este ejemplo, se ha declarado un campo pseudo-relacional llamado user_id que se relaciona con el modelo res.users. Este campo se puede utilizar en la interfaz de usuario de Odoo para mostrar el nombre del usuario asociado a cada tarea, sin tener que crear un campo many2one con el modelo res.users. </br>

### Comandos especiales
En Odoo, los comandos especiales son un conjunto de operaciones que se utilizan para modificar relaciones many2one o one2many de forma sencilla y eficiente. Estos comandos son especiales porque no se utilizan directamente en la base de datos, sino que se pasan como parámetros a métodos específicos de los modelos de datos de Odoo, como create() o write(). </br>

Los comandos especiales en Odoo se representan mediante tuplas de tres elementos, en la forma (operación, ID, valores). La operación indica el tipo de operación que se desea realizar (crear, actualizar, borrar, etc.), el ID es el ID del registro que se desea modificar (si es necesario), y los valores son un diccionario con los campos y sus valores que se desean actualizar (si es necesario).  </br>
Algunos ejemplos comunes de comandos especiales en Odoo son:

`(0, 0, values)`: Este comando se utiliza para crear un nuevo registro en el modelo secundario de la relación y asociarlo con el registro principal.</br>
`(1, id, values)`: Este comando se utiliza para actualizar un registro existente en el modelo secundario de la relación.</br>
`(2, id, 0)`: Este comando se utiliza para borrar un registro existente en el modelo secundario de la relación.</br>
`(3, id, 0)`: Este comando se utiliza para desvincular un registro existente en el modelo secundario de la relación del registro principal, sin borrarlo.</br>
`(5, 0, 0)`: Este comando remueve todos los registros del set, equivalente ausar el comando 3 en todos los registros explicitamente, no puede ser usado en create().</br>
`(6, 0, 0)`: Este comando reemplaza todos los registros exitente establecidos por la lista de "ids", es equivalente ausar el comando 4 para cada "id" en "ids". </br>

### Modelos en space_mission
En Odoo, el módulo space_mission es una aplicación que se utiliza para gestionar misiones espaciales. Este módulo contiene diferentes modelos de datos relacionados con las misiones espaciales, como por ejemplo: </br>

`spacecraft`: Este modelo de datos almacena información sobre las naves espaciales, como su nombre, fabricante y modelo.</br>
`mission`: Este modelo de datos almacena información sobre las misiones espaciales, como su nombre, fecha de lanzamiento y objetivo.</br>
`mission_phase`: Este modelo de datos almacena información sobre las fases de una misión espacial, como su nombre, fecha de inicio y fecha de fin.</br>
`astronaut`: Este modelo de datos almacena información sobre los astronautas, como su nombre, nacionalidad y habilidades.</br>
```python

class Spacecraft(models.Model):
    _name = 'space_mission.spacecraft'

    name = fields.Char()
    manufacturer = fields.Char()
    model = fields.Char()
    launch_date = fields.Date()
    weight = fields.Float()
    payload_capacity = fields.Float()

    # many2one field
    # Una nave espacial puede estar asociada a una o varias misiones.
    missions = fields.Many2one('space_mission.mission', string='Missions')

    # one2many field
    # Una nave espacial puede tener una o varias tripulaciones de astronautas
    crew = fields.One2many('space_mission.astronaut', 'spacecraft_id', string='Crew')


class Mission(models.Model):
    _name = 'space_mission.mission'

    name = fields.Char()
    launch_date = fields.Date()
    objective = fields.Text()
    budget = fields.Float()
    status = fields.Selection([
        ('planning', 'Planning'),
        ('ongoing', 'Ongoing'),
        ('completed', 'Completed'),
        ('cancelled', 'Cancelled'),
    ], default='planning')

    # many2one field
    # Una misión puede estar asociada a una nave espacial.
    spacecraft = fields.Many2one('space_mission.spacecraft', string='Spacecraft')

    # many2many field
    # Una misión puede tener uno o varios astronautas, y un astronauta puede estar asociado a una o varias misiones
    astronauts = fields.Many2many('space_mission.astronaut', 'mission_astronaut_rel', 'mission_id', 'astronaut_id', string='Astronauts')

    # one2many field
    # Una misión puede tener una o varias fases
    phases = fields.One2many('space_mission.mission_phase', 'mission_id', string='Phases')


class MissionPhase(models.Model):
    _name = 'space_mission.mission_phase'

    name = fields.Char()
    start_date = fields.Date()
    end_date = fields.Date()
    objective = fields.Text()

    # many2one field
    # Una fase de una misión puede estar asociada a una misión
    mission = fields.Many2one('space_mission.mission', string='Mission')
    
    
class Astronaut(models.Model):
    _name = 'space_mission.astronaut'

    name = fields.Char()
    nationality = fields.Char()
    skills = fields.Text()
    photo = fields.Binary(attachment=True)

    # many2one field
    # Un astronauta puede estar asociado a una nave espacial
    spacecraft = fields.Many2one('space_mission.spacecraft', string='Spacecraft')

    # many2many field
    # Un astronauta puede estar asociado a una o varias misiones y una misión puede tener uno o varios astronautas
    missions = fields.Many2many('space_mission.mission', 'mission_astronaut_rel', 'astronaut_id', 'mission_id', string='Missions')
```
> En Odoo, los campos one2many, many2one y many2many se utilizan para establecer relaciones entre diferentes modelos de datos. Estos campos tienen diferentes parámetros que se utilizan para especificar la relación entre los modelos. </br>

Un campo one2many tiene los siguientes parámetros:</br>
*Muestra una tabla para elegir un obj relacionado, se pueden elegir varios registros*</br>
**comodel_name:** El nombre del modelo de datos al que está relacionado este campo.</br>
**inverse_name:** El nombre del campo many2one en el modelo relacionado que se utilizará para establecer la relación inversa.</br>
**string:** Una cadena de texto que se utilizará como etiqueta para el campo en la interfaz de usuario.</br>

Un campo many2one tiene los siguientes parámetros:</br>
*Muestra un dropdown para elegir un obj relacionado*</br>
**comodel_name:** El nombre del modelo de datos al que está relacionado este campo.</br>
**string:** Una cadena de texto que se utilizará como etiqueta para el campo en la interfaz de usuario.</br>

Un campo many2many tiene los siguientes parámetros:</br>
*Muestra una lista de checkbox de registros donde se peuden elegir varios*</br>
**comodel_name:** El nombre del modelo de datos al que está relacionado este campo.</br>
**relation:** El nombre de la tabla de relación que se utilizará para almacenar las relaciones entre los registros de los dos modelos.</br>
**column1:** El nombre de la columna de la tabla de relación que almacenará los IDs de los registros del primer modelo.</br>
**column2:** El nombre de la columna de la tabla de relación que almacenará los IDs de los registros del segundo modelo.</br>
**string:** Una cadena de texto que se utilizará como etiqueta para el campo en la interfaz de usuario.</br>

```python
class Libros(models.Model):
    _name = 'libros'
    
    name = fields.Char(string="Nombre del libro", required=True)
    editorial = fields.Char(string="Editorial", required=True)
    isbn = fields.Char(string="ISBN", required=True)
    
    # Un libro puede tener un autor
    author_id = fields.Many2one(comodel_name="autor", string="Autor")

class Autor(models.Model):
    _name = 'autor'
    
    name = fields.Char(string="Nombre")
```
## Vistas avanzadas
### Vista kanban
La vista kanban en Odoo es una forma de visualizar y gestionar tareas o elementos de trabajo en un flujo de trabajo. Se representan mediante tarjetas, que se organizan en columnas que representan cada etapa del proceso. Esta vista se encuentra en un punto intermedio entre una vista de lista y un formulario no editable.

Los registros pueden agruparse en columnas para facilitar su visualización y manipulación en un flujo de trabajo. También pueden desagruparse para mostrar los registros individualmente. Por defecto, se deberían agrupar los registros en la vista kanban, aunque esto puede cambiarse en la configuración.

Sin embargo, se recomienda tener un máximo de 10 columnas en la vista kanban para evitar sobrecargar la interfaz y mejorar la usabilidad. Si se utilizan más de 10 columnas, puede que se cierren algunas de ellas para evitar sobrecargar la interfaz.

`default_group_by:` permite especificar uno o más campos por los cuales se deben agrupar los registros en la vista kanban.
`quick_create:` habilita la opción de crear registros rápidamente desde la vista kanban.
`create_button:` muestra un botón para crear un nuevo registro en la vista kanban.
`pagination:` habilita o deshabilita la paginación en la vista kanban.
`limit:` establece el número máximo de registros que se deben mostrar en la vista kanban.
`colors:` permite asignar colores a las columnas y tarjetas en la vista kanban para facilitar su identificación.

#### kanban group_create
En Odoo, el atributo group_create de la vista kanban permite agrupar los elementos que se crean rápidamente en la vista kanban en una columna específica. Por defecto, este atributo está desactivado y los elementos que se crean rápidamente se agregarán a la última columna de la vista kanban.

Para activar el atributo group_create en la vista kanban, se puede establecer su valor en True en la configuración de la vista. Esto hará que los elementos que se creen rápidamente en la vista kanban se agrupen en una columna específica, que se puede definir en el atributo group_create_col_id.

Por ejemplo, si se establece el atributo group_create_col_id en el ID de la columna "Pendientes", los elementos que se creen rápidamente en la vista kanban se agruparán en la columna "Pendientes". Esto puede ser útil para organizar mejor los elementos en la vista kanban y facilitar su gestión.

#### kanban group_delete
En Odoo, el atributo group_delete de la vista kanban permite agrupar los elementos que se eliminan en la vista kanban en una columna específica. Por defecto, este atributo está desactivado y los elementos que se eliminan se quitarán de la vista kanban sin agruparse en ninguna columna.

Para activar el atributo group_delete en la vista kanban, se puede establecer su valor en True en la configuración de la vista. Esto hará que los elementos que se eliminen en la vista kanban se agrupen en una columna específica, que se puede definir en el atributo group_delete_col_id.

Por ejemplo, si se establece el atributo group_delete_col_id en el ID de la columna "Eliminados", los elementos que se eliminen en la vista kanban se agruparán en la columna "Eliminados". Esto puede ser útil para organizar mejor los elementos en la vista kanban y facilitar su gestión.

#### kanban group_edit
En Odoo, el atributo group_edit de la vista kanban permite agrupar los elementos que se editan en la vista kanban en una columna específica. Por defecto, este atributo está desactivado y los elementos que se editan se mantienen en la misma columna de la vista kanban.

Para activar el atributo group_edit en la vista kanban, se puede establecer su valor en True en la configuración de la vista. Esto hará que los elementos que se editen en la vista kanban se agrupen en una columna específica, que se puede definir en el atributo group_edit_col_id.

Por ejemplo, si se establece el atributo group_edit_col_id en el ID de la columna "Editados", los elementos que se editen en la vista kanban se agruparán en la columna "Editados". Esto puede ser útil para organizar mejor los elementos en la vista kanban y facilitar su gestión.

#### archivable
En Odoo, el atributo archivable de la vista kanban indica si los elementos que se eliminan en la vista kanban se moverán a una columna de elementos archivados o se eliminarán definitivamente. Por defecto, este atributo está desactivado y los elementos que se eliminan se eliminarán definitivamente.

Para activar el atributo archivable en la vista kanban, se puede establecer su valor en True en la configuración de la vista. Esto hará que los elementos que se eliminen en la vista kanban se muevan a una columna de elementos archivados en lugar de eliminarse definitivamente. La columna de elementos archivados se puede definir en el atributo archived_column_id.

Por ejemplo, si se establece el atributo archived_column_id en el ID de la columna "Archivados", los elementos que se eliminen en la vista kanban se moverán a la columna "Archivados" en lugar de eliminarse definitivamente. Esto puede ser útil para facilitar la recuperación de elementos eliminados accidentalmente en la vista kanban.

#### quick_create
En Odoo, el atributo quick_create de la vista kanban indica si se permitirá crear elementos rápidamente desde la vista kanban. Por defecto, este atributo está desactivado y no se permitirá crear elementos rápidamente en la vista kanban.

Para activar el atributo quick_create en la vista kanban, se puede establecer su valor en True en la configuración de la vista. Esto habilitará la opción de crear elementos rápidamente en la vista kanban, lo que permitirá agregar nuevos elementos a la vista de forma rápida y sencilla.

Además, el atributo quick_create_options permite definir las opciones que se mostrarán al crear un elemento rápidamente en la vista kanban. Por ejemplo, se pueden definir campos obligatorios, valores predeterminados o campos ocultos para facilitar la creación de elementos en la vista kanban.

#### quick_create_view
En Odoo, el atributo quick_create_view de la vista kanban indica la vista que se utilizará para crear elementos rápidamente en la vista kanban. Por defecto, este atributo se establece en quick_create y se utilizará una vista de creación rápida predeterminada para crear elementos en la vista kanban.

Para utilizar una vista personalizada para crear elementos rápidamente en la vista kanban, se puede establecer el atributo quick_create_view en el ID de la vista personalizada en la configuración de la vista kanban. Esto permite utilizar una vista personalizada que contenga solo los campos relevantes para la creación rápida de elementos en la vista kanban.

Además, el atributo quick_create_options permite definir las opciones que se mostrarán al crear un elemento rápidamente en la vista kanban. Por ejemplo, se pueden definir campos obligatorios, valores predeterminados o campos ocultos para facilitar la creación de elementos en la vista kanban.
```xml
<kanban>
    <field name="name"/>
    <field name="stage_id"/>
    <templates>
        <t t-name="kanban-box">
            <div class="oe_kanban_global_click">
                <field name="name"/>
                <field name="stage_id"/>
            </div>
        </t>
    </templates>
    <attrs>
        <att name="quick_create">True</att>
        <att name="quick_create_view">my_quick_create_view</att>
    </attrs>
</kanban>
```
En este ejemplo, se ha habilitado el atributo quick_create en la vista kanban mediante el uso del elemento attrs. Esto permitirá crear elementos rápidamente en la vista kanban mediante una vista de creación rápida personalizada.

Además, se ha establecido el atributo quick_create_view en el ID de la vista personalizada my_quick_create_view. Esta vista personalizada contendrá solo los campos relevantes para la creación rápida de elementos en la vista kanban, como el nombre y el estado del elemento.

En la plantilla kanban-box, se han definido dos campos, name

#### records_draggable
En Odoo, el atributo records_draggable de la vista kanban indica si los elementos de la vista kanban se pueden mover entre las diferentes columnas mediante arrastrar y soltar. Por defecto, este atributo está desactivado y los elementos no se podrán mover entre las columnas mediante arrastrar y soltar.

Para activar el atributo records_draggable en la vista kanban, se puede establecer su valor en True en la configuración de la vista. Esto habilitará la opción de mover elementos entre las columnas mediante arrastrar y soltar en la vista kanban, lo que permite reordenar los elementos de forma rápida y sencilla.

Además, el atributo records_editable permite habilitar la edición de elementos en la vista kanban mediante doble clic o clic en el botón de edición. Esto permite modificar los valores de los campos de los elementos en la vista kanban de forma sencilla y rápida.
```xml
<kanban>
    <field name="name"/>
    <field name="stage_id"/>
    <templates>
        <t t-name="kanban-box">
            <div class="oe_kanban_global_click">
                <field name="name"/>
                <field name="stage_id"/>
            </div>
        </t>
    </templates>
    <attrs>
        <att name="records_draggable">True</att>
    </attrs>
</kanban>
```
En este ejemplo, se ha habilitado el atributo records_draggable en la vista kanban mediante el uso del elemento attrs. Esto permitirá mover los elementos de la vista kanban entre las diferentes columnas mediante arrastrar y soltar.

Además, se han definido dos campos, name y stage_id, que se mostrarán en cada tarjeta de la vista kanban. Estos campos se mostrarán en la plantilla kanban-box, que se utilizará para dar formato a las tarjetas de la vista kanban. De esta forma, se pueden personalizar la apariencia y el contenido de las tarjetas de la vista kanban.

#### Elementos de kanban
fields: muestran los valores de los campos de los elementos en las tarjetas de la vista kanban. Por ejemplo, se pueden mostrar los campos name, stage_id o progress en cada tarjeta para mostrar información relevante del elemento.</br>
Barra de progreso: muestra el progreso de cada elemento en forma de barra de progreso en las tarjetas de la vista kanban. Esto permite visualizar de forma sencilla el avance de cada elemento en el flujo de trabajo.</br>
groups: agrupan las tarjetas en diferentes columnas de la vista kanban en función de un campo específico. Por ejemplo, se pueden agrupar las tarjetas por el campo stage_id para mostrar las tarjetas en las diferentes etapas del flujo de trabajo.</br>
Tags: muestran etiquetas en las tarjetas de la vista kanban para indicar el estado o la prioridad de cada elemento. Esto permite identificar rápidamente los elementos que requieren atención.</br>

Aunque he mencionado algunos de los atributos más comunes de la vista kanban en Odoo, hay muchos más atributos que se pueden utilizar para personalizar su apariencia y comportamiento. Algunos de estos atributos adicionales incluyen:</br>

`create_button:` indica si se mostrará un botón para crear nuevos elementos en la vista kanban.</br>
`quick_create_class:` define la clase CSS que se utilizará para el formulario de creación rápida en la vista kanban.</br>
`deactivate_drag_and_drop:` indica si se desactivará la función de arrastrar y soltar en la vista kanban.</br>
`default_order:` establece el orden en que se mostrarán los elementos en la vista kanban.</br>
`sequence:` define el orden en que se mostrarán las columnas en la vista kanban.</br>
`foldable:` indica si se permitirá plegar y desplegar las columnas en la vista kanban.</br>
`default_folded:` establece si las columnas se mostrarán plegadas o desplegadas por defecto en la vista kanban.</br>
`resequence_on_drop:` indica si se reordenarán automáticamente los elementos en la vista kanban cuando se cambien de columna.</br>
`date_start:` especifica el campo que se utilizará como fecha de inicio para los elementos en la vista kanban.</br>
`date_delay:` define el campo que se utilizará como retraso para los elementos en la vista kanban.</br>
`date_stop:` establece el campo que se utilizará como fecha de fin para los elementos en la vista kanban.</br>
`date_deadline:` especifica el campo que se utilizará como fecha límite para los elementos en la vista kanban.</br>
