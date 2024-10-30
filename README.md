# Principios-generales-y-SOLID
## Ejercicio Práctico 1 (3 Puntos): Creación de una Clase en Python que Representa una Matriz

Para este ejercicio, deberás crear una clase que representa una matriz. Las operaciones que esta clase debe permitir son:

- La creación de una matriz a partir de una lista de listas.
- La impresión de la matriz en una forma legible.
- El cálculo de la transpuesta de la matriz.

Asegúrate de que cada método tenga una única responsabilidad.

```python
class Matriz:
    def __init__(self, elementos):
        self.elementos = elementos

    def imprimir(self):
        for fila in self.elementos:
            print(fila)

    def transpuesta(self):
        return Matriz([[fila[i] for fila in self.elementos] for i in range(len(self.elementos[0]))])

m = Matriz([[1, 2], [3, 4]])
m.imprimir()
print()
m_transpuesta = m.transpuesta()
m_transpuesta.imprimir()

Esto deberia dar como resultado
[1, 2]
[3, 4]

[1, 3]
[2, 4]

'''python


## Criterio de Evaluación

Se debe evaluar la implementación correcta de la **responsabilidad única** (cada método hace una sola cosa), la **claridad del código** y la **correcta utilización de las características de Python**.

### Criterios

1. **Claridad y limpieza del código** (30%)
2. **Implementación correcta de la responsabilidad única** (40%)
3. **Uso correcto de las características de Python** (30%)

---

## Ejercicio 2 (7 Puntos): La Pizzería

Estás creando un sistema de gestión de pedidos de pizza en línea utilizando Python. Este sistema consta de varios componentes que interactúan entre sí. Los componentes principales son:

- **DataBaseManager**: Esta clase es responsable de manejar la conexión con la base de datos y realizar operaciones CRUD.
- **Authenticator**: Esta clase se utiliza para manejar la autenticación de usuarios, posiblemente utilizando un servicio externo o una base de datos local.
- **OrderManager**: Esta clase se encarga de la gestión de los pedidos, incluyendo la creación, actualización, y eliminación de los pedidos de los usuarios.
- **PaymentProcessor**: Esta clase es responsable de manejar las transacciones de pago, utilizando un servicio de procesamiento de pagos externo.

Estos componentes no deben crearse ni gestionarse dentro de cada clase que los utiliza, sino que deben ser creados en algún lugar centralizado e “inyectados” en las clases que los necesitan.

### Instrucciones

Tu tarea es implementar este sistema utilizando el concepto de **inyección de dependencias**. Debes definir cada clase y sus dependencias, luego inyectar las dependencias a través de los constructores de las clases. Por ejemplo, la clase `OrderManager` debería recibir instancias de `DataBaseManager`, `Authenticator`, y `PaymentProcessor` a través de su constructor.

Al implementar este sistema, considera los siguientes aspectos:

- **Desacoplamiento de las clases**: Las clases no deben crear sus propias dependencias. En lugar de eso, deben recibir las dependencias ya creadas. Esto promueve un código más limpio y modular.
- **Pruebas**: La inyección de dependencias debe facilitar las pruebas de las clases. Deberías poder crear "mocks" o "stubs" de las dependencias para probar las clases de manera aislada.
- **Reutilización de código**: Si varias clases necesitan la misma dependencia, no debes crear una nueva instancia para cada una. En lugar de eso, crea una instancia de la dependencia y pásala a todas las clases que la necesiten.

Para concluir, debes demostrar cómo crearías las instancias de las dependencias y cómo las inyectarías en las clases que las necesitan. Asegúrate de que tu implementación sea robusta, fácil de entender y fácil de mantener.

Aquí está cómo se podrían ver nuestras clases:

```python
class DataBaseManager:
    def __init__(self, connection_string):
        self.connection_string = connection_string

class Authenticator:
    def __init__(self, user_database):
        self.user_database = user_database

class PaymentProcessor:
    def __init__(self, api_key):
        self.api_key = api_key

class OrderManager:
    def __init__(self, database_manager, authenticator, payment_processor):
        self.database_manager = database_manager
        self.authenticator = authenticator
        self.payment_processor = payment_processor
'''
Ahora, en lugar de crear las instancias de las dependencias dentro de OrderManager, puedes crearlas en algún lugar centralizado y pasarlas como argumentos al constructor de la OrderManager.

# Crear instancias de nuestras dependencias
database_manager = DataBaseManager("my-database-connection-string")
authenticator = Authenticator(database_manager)
payment_processor = PaymentProcessor("my-payment-api-key")

# Crear una instancia de OrderManager, pasando nuestras dependencias
order_manager = OrderManager(database_manager, authenticator, payment_processor)

Rúbrica de Evaluación del Ejercicio de Inyección de Dependencias

Creación de Clases y Métodos (25 puntos)

	1.	Clase DataBaseManager correctamente implementada (5 puntos)
	2.	Clase Authenticator correctamente implementada (5 puntos)
	3.	Clase OrderManager correctamente implementada (5 puntos)
	4.	Clase PaymentProcessor correctamente implementada (5 puntos)
	5.	Cada clase contiene los métodos apropiados para su funcionalidad (5 puntos)

Inyección de Dependencias (25 puntos)

	1.	Las dependencias se pasan a las clases a través de los constructores (10 puntos)
	2.	Ninguna clase crea sus propias dependencias (10 puntos)
	3.	Las clases utilizan las dependencias pasadas en lugar de crear las suyas propias (5 puntos)

Pruebas (25 puntos)

	1.	Se pueden crear “mocks” o “stubs” de las dependencias para probar las clases de manera aislada (10 puntos)
	2.	Se escriben y ejecutan pruebas unitarias para cada clase y método (10 puntos)
	3.	Las pruebas demuestran que las clases y los métodos funcionan como se esperaba (5 puntos)

Reutilización de Código y Principios de Diseño de Software (25 puntos)

	1.	No se crea una nueva instancia de una dependencia para cada clase que la necesita (5 puntos)
	2.	El código está organizado y es fácil de leer (10 puntos)
	3.	Se siguen buenas prácticas de codificación y principios de diseño de software (10 puntos)

Cada criterio será calificado con el puntaje mencionado, y la puntuación total se calculará sumando los puntajes de todos los criterios. Una solución perfecta, que satisface todos los criterios al máximo, recibirá 100 puntos.
