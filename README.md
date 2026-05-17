# PAQUETE-ESTUDIANTE-07
Instrucciones: Para cada ejercicio debes escribir: (1) la clase abstracta (usando ABC) con sus métodos abstractos, (2) la(s) subclase(s) que hereden e implementen dichos métodos, y (3) al menos un objeto de prueba con llamadas a los métodos. Recuerda importar ABC y abstractmethod del módulo abc.

"""
Ejercicio 1 FiguraGeometrica y Circulo    Nivel 1

Crea una clase abstracta FiguraGeometrica con un método abstracto calcular_area() y un método concreto describir() que imprima el tipo de figura. Crea una subclase Circulo que herede de FiguraGeometrica, reciba el atributo radio e implemente calcular_area() usando pi = 3.14.

Prueba con radio = 4 y radio = 10.
"""

from abc import ABC, abstractmethod

# se crea la clase figura geometrica como clase abstracta
class FiguraGeometrica(ABC):

    @abstractmethod 
    def calcular_area(self):
        pass

    def describir(self):
        print("Esta es una figura geométrica")


# Se crea la Subclase circulo que hereda de figurageometrica
class Circulo(FiguraGeometrica):

    def __init__(self, radio):
        self.radio = radio

    def calcular_area(self):
        return 3.14 * (self.radio ** 2)


# Se crean los Objetos de prueba con radio 4 y radio 10
circulo1 = Circulo(4)
circulo1.describir()
print("Área del círculo con radio 4:", circulo1.calcular_area())

print()

circulo2 = Circulo(10)
circulo2.describir()
print("Área del círculo con radio 10:", circulo2.calcular_area())


"""
Ejercicio 2 CuentaBancaria, Ahorros y Corriente    Nivel 2

Crea una clase abstracta CuentaBancaria con los atributos titular y saldo, y dos métodos abstractos: cobrar_comision() y mostrar_info(). Crea dos subclases: CuentaAhorros (sin comisión, genera rendimiento del 2% sobre el saldo) y CuentaCorriente (cobra comisión fija de $8.000). Cada subclase hereda e implementa ambos métodos. Instancia una cuenta de cada tipo y pruébalas.

"""
from abc import ABC, abstractmethod

# Se crea la clase abstracta cuentabancaria

class CuentaBancaria (ABC):
    
    def __init__(self, titular, saldo):
        self.titular = titular
        self.saldo = saldo

    @abstractmethod
    def cobrar_comision(self):
        pass

    @abstractmethod
    def mostrar_info(self):
        pass

    # Subclases 

# subclase cuenta de ahorros
class CuentaAhorros(CuentaBancaria):

        def cobrar_comision(self):
            rendimiento = self.saldo *0.02
            self.saldo += rendimiento

        def mostrar_info(self):

            print("Cuenta de Ahorros")
            print("Titular:", self.titular)
            print("Saldo:", self.saldo)


# Subclase CuentaCorriente
class CuentaCorriente(CuentaBancaria):

    def cobrar_comision(self):
        self.saldo -= 8000

    def mostrar_info(self):
        print("Cuenta Corriente")
        print("Titular: ", self.titular)
        print("Saldo: ", self.saldo)


# Objetos de prueba
cuenta1 = CuentaAhorros("Brahyan", 500000)
cuenta1.cobrar_comision()
cuenta1.mostrar_info()

print()

cuenta2 = CuentaCorriente("Sofia", 500000)
cuenta2.cobrar_comision()
cuenta2.mostrar_info()



"""
Ejercicio 3 Habitacion, Reserva, Estandar y VIP    Nivel 3

Crea una clase Habitacion (numero, tipo, precio_noche). Crea una clase abstracta Reserva con atributos cliente, habitacion (objeto Habitacion) y noches, y métodos abstractos calcular_total() y confirmar(). Crea subclases ReservaEstandar (paga solo el costo de las noches) y ReservaVIP (agrega desayuno de $25.000 por noche). Cada subclase recibe un objeto Habitacion. Prueba reservando 3 noches en cada modalidad.
"""



from abc import ABC, abstractmethod

# Se crea la Clase Habitacion
class Habitacion:

    def __init__(self, numero, tipo, precio_noche):
        self.numero = numero
        self.tipo = tipo
        self.precio_noche = precio_noche


# Se crea la Clase abstracta Reserva
class Reserva(ABC):

    def __init__(self, cliente, habitacion, noches):
        self.cliente = cliente
        self.habitacion = habitacion
        self.noches = noches

    @abstractmethod
    def calcular_total(self):
        pass

    @abstractmethod
    def confirmar(self):
        pass


# Subclase ReservaEstandar
class ReservaEstandar(Reserva):

    def calcular_total(self):
        return self.habitacion.precio_noche * self.noches

    def confirmar(self):
        print("Reserva Estándar confirmada")
        print("Cliente:", self.cliente)
        print("Habitación:", self.habitacion.numero)
        print("Total:", self.calcular_total())


# Subclase ReservaVIP
class ReservaVIP(Reserva):

    def calcular_total(self):
        desayuno = 25000 * self.noches
        return (self.habitacion.precio_noche * self.noches) + desayuno

    def confirmar(self):
        print("Reserva VIP confirmada")
        print("Cliente:", self.cliente)
        print("Habitación:", self.habitacion.numero)
        print("Total:", self.calcular_total())


# Objetos de prueba
habitacion1 = Habitacion(101, "Estándar", 120000)
habitacion2 = Habitacion(202, "VIP", 200000)

reserva1 = ReservaEstandar("Andrés", habitacion1, 3)
reserva1.confirmar()

print()

reserva2 = ReservaVIP("María", habitacion2, 3)
reserva2.confirmar()
