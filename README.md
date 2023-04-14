# Ruby & Rails 7.0.3 
## Sigue el principio de convención sobre configuración (CoC)
Rails sigue el principio de convención sobre configuración, lo que significa que proporciona una estructura y convenciones predeterminadas para tus aplicaciones. Sigue estas convenciones para que tu código sea más fácil de entender y mantener.

Por ejemplo, Rails asume que tus modelos se relacionarán con tablas de la base de datos con nombres que son el plural de los modelos. Si tienes un modelo User, Rails buscará una tabla llamada `users` en la base de datos. Si necesitas cambiar este comportamiento predeterminado, puedes hacerlo mediante el uso de la sintaxis de configuración de Rails:
```rb
class User < ApplicationRecord
  self.table_name = 'my_users'
end
```
## Patrón Modelo-Vista-Controlador (MVC)
Rails utiliza el patrón Modelo-Vista-Controlador (MVC), que separa la lógica de negocio de la presentación y el control. Sigue este patrón para que tu código sea más modular y escalable.

**Por ejemplo**, si tienes una aplicación que muestra una lista de productos en una página, la vista mostrará los productos, el controlador manejará la lógica de negocio y el modelo manejará la interacción con la base de datos:
````rb
# app/models/product.rb
class Product < ApplicationRecord
  # código para interactuar con la base de datos
end

# app/controllers/products_controller.rb
class ProductsController < ApplicationController
  def index
    @products = Product.all
  end
end

# app/views/products/index.html.erb
<h1>Productos</h1>

<ul>
  <% @products.each do |product| %>
    <li><%= product.name %></li>
  <% end %>
</ul>
```
## Usa migraciones para manejar la base de datos
Las migraciones son archivos de Ruby que describen cómo la base de datos debe cambiar para satisfacer tus necesidades. Usa migraciones para modificar la base de datos en lugar de hacer cambios directamente en la base de datos.

Por ejemplo, para agregar una columna **age** a la tabla **users**, puedes crear una migración con el siguiente código:
```rb
class AddAgeToUsers < ActiveRecord::Migration[6.1]
  def change
    add_column :users, :age, :integer
  end
end
```

Usa scopes para encapsular la lógica de consulta
Usa scopes para encapsular la lógica de consulta en tu modelo. Los scopes son métodos de clase que te permiten definir consultas comunes que se pueden utilizar en diferentes partes de tu aplicación.

Por ejemplo, si tienes un modelo Post y quieres recuperar todos los posts que fueron publicados hace menos de una semana, puedes crear un scope con el siguiente código:
```rb
class Post < ApplicationRecord
  scope :recent, -> { where('created_at >= ?', 1.week.ago) }
end
```
Ahora puedes usarlo en cualquier parte de tu aplicación
```
@recent_posts = Post.recent
```
