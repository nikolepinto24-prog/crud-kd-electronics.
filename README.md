# crud-kd-electronics.
Taller 
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Taller CRUD - KD Electronics</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; line-height: 1.6; }
    h1, h2 { color: #2c3e50; }
    pre { background: #f4f4f4; padding: 10px; border-radius: 5px; overflow-x: auto; }
    .section { margin-bottom: 40px; }
    img { max-width: 100%; margin: 10px 0; }
  </style>
</head>
<body>
  <h1>Taller de creación de CRUD - KD Electronics</h1>
  <p>Este taller implementa un sistema de gestión de inventario con un módulo de productos. Se desarrolla un CRUD (Create, Read, Update, Delete) en Java.</p>

  <div class="section">
    <h2>📦 Caso</h2>
    <p>La empresa KD-Electronics vende productos electrónicos y requiere un sistema para gestionar su inventario. El módulo de productos debe permitir:</p>
    <ul>
      <li>Registrar nuevos productos (Create).</li>
      <li>Consultar productos por código (Read).</li>
      <li>Actualizar información (Update).</li>
      <li>Eliminar lógicamente productos (Delete).</li>
    </ul>
  </div>

  <div class="section">
    <h2>📂 Clase Producto</h2>
    <pre><code>public class Producto {
    private String codigo;
    private String nombre;
    private String descripcion;
    private double precioBase;
    private double precioVenta;
    private String categoria;
    private int cantidad;
    private boolean activo;

    public Producto(String codigo, String nombre, String descripcion,
                    double precioBase, double precioVenta,
                    String categoria, int cantidad) {
        this.codigo = codigo;
        this.nombre = nombre;
        this.descripcion = descripcion;
        this.precioBase = precioBase;
        this.precioVenta = precioVenta;
        this.categoria = categoria;
        this.cantidad = cantidad;
        this.activo = true;
    }
    // Getters y setters...
}
</code></pre>
  </div>

  <div class="section">
    <h2>📂 Clase ProductoDAO</h2>
    <pre><code>import java.util.HashMap;
import java.util.Map;

public class ProductoDAO {
    private Map&lt;String, Producto&gt; inventario = new HashMap&lt;&gt;();

    public void crearProducto(Producto p) {
        inventario.put(p.getCodigo(), p);
    }

    public Producto consultarPorCodigo(String codigo) {
        Producto p = inventario.get(codigo);
        return (p != null && p.isActivo()) ? p : null;
    }

    public void actualizarProducto(String codigo, String nombre, String descripcion,
                                   double precioBase, double precioVenta,
                                   String categoria, int cantidad) {
        Producto p = inventario.get(codigo);
        if (p != null && p.isActivo()) {
            p.setNombre(nombre);
            p.setDescripcion(descripcion);
            p.setPrecioBase(precioBase);
            p.setPrecioVenta(precioVenta);
            p.setCategoria(categoria);
            p.setCantidad(cantidad);
        }
    }

    public void eliminarProducto(String codigo) {
        Producto p = inventario.get(codigo);
        if (p != null) {
            p.setActivo(false);
        }
    }
}
</code></pre>
  </div>

  <div class="section">
    <h2>🎛️ Clase Main</h2>
    <pre><code>public class Main {
    public static void main(String[] args) {
        ProductoDAO dao = new ProductoDAO();

        Producto p1 = new Producto("P001", "Laptop", "Laptop 15 pulgadas", 2000, 2500, "Computadores", 10);
        dao.crearProducto(p1);

        System.out.println("Consulta: " + dao.consultarPorCodigo("P001").getNombre());

        dao.actualizarProducto("P001", "Laptop Gamer", "Laptop con tarjeta gráfica", 2200, 2800, "Computadores", 8);
        System.out.println("Actualizado: " + dao.consultarPorCodigo("P001").getDescripcion());

        dao.eliminarProducto("P001");
        System.out.println("Después de eliminar: " + dao.consultarPorCodigo("P001"));
    }
}
</code></pre>
  </div>

  <div class="section">
    <h2>📸 Capturas y UML</h2>
    <p>Aquí puedes insertar tus capturas de pantalla del proyecto en NetBeans/Eclipse y el diagrama UML.</p>
    <img src="diagrama-uml.png" alt="Diagrama UML CRUD">
  </div>

  <div class="section">
    <h2>✅ Resultados esperados</h2>
    <ul>
      <li>Registro exitoso de producto.</li>
      <li>Consulta muestra nombre inicial.</li>
      <li>Actualización refleja cambios en descripción.</li>
      <li>Eliminación lógica devuelve <code>null</code> en la consulta.</li>
    </ul>
  </div>
</body>
</html>
