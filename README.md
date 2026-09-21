class Pila:
    def __init__(self):
        self.elementos = []

    def esta_vacia(self):
        return len(self.elementos) == 0

    def apilar(self, elemento):
        self.elementos.append(elemento)

    def desapilar(self):
        return self.elementos.pop()

    def ver_tope(self):
        return self.elementos[-1]

    def vaciar(self):
        self.elementos = []


class NavegadorWeb:
    def __init__(self):
        self.pila_atras = Pila()
        self.pila_adelante = Pila()
        self.pagina_actual = None

    def visitar_pagina(self, url):
        if not url:
            print("Debes ingresar una URL válida.")
            return
        if self.pagina_actual is not None:
            self.pila_atras.apilar(self.pagina_actual)
        self.pila_adelante.vaciar()
        self.pagina_actual = url
        print(f"Página actual: {self.pagina_actual}")

    def retroceder(self):
        if self.pila_atras.esta_vacia():
            print("No hay páginas anteriores en el historial.")
            return
        self.pila_adelante.apilar(self.pagina_actual)
        self.pagina_actual = self.pila_atras.desapilar()
        print(f"Página actual: {self.pagina_actual}")

    def avanzar(self):
        if self.pila_adelante.esta_vacia():
            print("No hay páginas siguientes en el historial.")
            return
        self.pila_atras.apilar(self.pagina_actual)
        self.pagina_actual = self.pila_adelante.desapilar()
        print(f"Página actual: {self.pagina_actual}")

    def mostrar_pagina_actual(self):
        if self.pagina_actual is None:
            print("No se ha visitado ninguna página todavía.")
        else:
            print(f"Página actual: {self.pagina_actual}")

    def salir(self):
        print("Cerrando el navegador. ¡Hasta pronto!")


def menu():
    navegador = NavegadorWeb()
    while True:
        print("\n1. Visitar página")
        print("2. Back")
        print("3. Forward")
        print("4. Mostrar página actual")
        print("5. Exit")
        opcion = input("Selecciona una opción: ").strip()

        if opcion == "1":
            url = input("Ingresa la URL: ").strip()
            navegador.visitar_pagina(url)
        elif opcion == "2":
            navegador.retroceder()
        elif opcion == "3":
            navegador.avanzar()
        elif opcion == "4":
            navegador.mostrar_pagina_actual()
        elif opcion == "5":
            navegador.salir()
            break
        else:
            print("Opción no válida. Intenta nuevamente.")


if __name__ == "__main__":
    menu()
