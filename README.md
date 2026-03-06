# crud-kd-electronics.
Taller 
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Taller CRUD - KD Electronics</title>
  <style>
    
  

  

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
    
