# Programa-de-la-tarea-2
  class InventarioTienda:
    def __init__(self, nombre_tienda):
        self.nombre_tienda = nombre_tienda
        self.productos = []

    def agregar_producto(self, nombre, precio, cantidad):
        if precio <= 0 or cantidad <= 0:
            print(" El precio y la cantidad deben de ser positivos.")
            return
        
        for producto in self.productos:
            if producto["nombre"].lower() == nombre.lower():
                producto["cantidad"] += cantidad
                print(f" Se agrego stock al producto '{nombre}'.")
                return
        
        nuevo_producto = {"nombre": nombre, "precio": precio, "cantidad": cantidad}
        self.productos.append(nuevo_producto)
        print(f" El producto '{nombre}' se agrego correctamente.")

    def vender_producto(self, nombre, cantidad):
        for producto in self.productos:
            if producto["nombre"].lower() == nombre.lower():
                if cantidad <= 0:
                    print(" La cantidad que se va a vender debe de ser positiva.")
                    return
                if producto["cantidad"] >= cantidad:
                    producto["cantidad"] -= cantidad
                    print(f" Se realizo la venta: {cantidad} unidades de '{nombre}'.")
                else:
                    print(" No hay suficiente stock para realizar la venta.")
                return
        print(" Ese producto no existe.")

    def mostrar_inventario(self):
        if not self.productos:
            print(" Esta vacio el inventario.")
        else:
            print(f"\n Inventario de {self.nombre_tienda}:")
            for producto in self.productos:
                print(f"- {producto['nombre']} | Precio: ${producto['precio']} | Cantidad: {producto['cantidad']}")
            print()

    def producto_mas_caro(self):
        if not self.productos:
            print(" El inventario no tiene productos.")
            return
        producto_caro = max(self.productos, key=lambda p: p["precio"])
        print(f" El producto mas caro es '{producto_caro['nombre']}' con un precio de ${producto_caro['precio']}.")



def menu():
    tienda = InventarioTienda("Mi tienda")

    while True:
        print("\n--- MENU ---")
        print("1. Agregar un producto")
        print("2. Vender un producto")
        print("3. Ver el inventario")
        print("4. Ver el producto mas caro")
        print("5. Salir")

        opcion = input("Elige una opcion: ")

        if opcion == "1":
            nombre = input("Nombre del producto: ")
            try:
                precio = float(input("Precio del producto: "))
                cantidad = int(input("Cantidad: "))
                tienda.agregar_producto(nombre, precio, cantidad)
            except ValueError:
                print(" El precio o la cantidad no son validos.")

        elif opcion == "2":
            nombre = input("Nombre del producto que se va a vender: ")
            try:
                cantidad = int(input("Cantidad que se va a vender: "))
                tienda.vender_producto(nombre, cantidad)
            except ValueError:
                print(" La cantidad es invalida.")

        elif opcion == "3":
            tienda.mostrar_inventario()

        elif opcion == "4":
            tienda.producto_mas_caro()

        elif opcion == "5":
            print(" Saliendo del programa...")
            break

        else:
            print(" La opcion no valida, intenta de nuevo.")

if __name__ == "__main__":
    menu()


if __name__ == "__main__":
    menu()
