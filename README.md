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

**(0, 0, values):** Este comando se utiliza para crear un nuevo registro en el modelo secundario de la relación y asociarlo con el registro principal.</br>
**(1, id, values):** Este comando se utiliza para actualizar un registro existente en el modelo secundario de la relación.</br>
**(3, id, 0):** Este comando remueve el registro de id "id" del set, pero no lo borra, no puede ser usado en create().</br>
**(4, id, 0):** Este comando añade un registro existente de id "id" al set.</br>
**(5, 0, 0):** Este comando remueve todos los registros del set, equivalente ausar el comando 3 en todos los registros explicitamente, no puede ser usado en create().</br>
**(6, 0, 0):** Este comando reemplaza todos los registros exitente establecidos por la lista de "ids", es equivalente ausar el comando 4 para cada "id" en "ids". </br>
