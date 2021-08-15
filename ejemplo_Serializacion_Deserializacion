

/*SERIALIZACIÓN
 * ____________
 * 
 * Vamos a pasar a bytes una serie de datos de empleados almacenados en un array
 */

package ficheros;

import java.util.*;
import java.io.*;
public class empleado implements Serializable{


	private String nombre;
	private String apellidos;
	private int sueldo;
	private int antiguedad;
	private String categoria;
	
	
	public empleado(String nombre, String apellidos, String categoria,int sueldo, int antiguedad) {
		this.nombre=nombre;
		this.apellidos=apellidos;
		this.sueldo=sueldo;
		this.antiguedad=antiguedad;
		this.categoria=categoria;
	}
	public String getNombre() {
		return nombre;
	}


	public String getApellidos() {
		return apellidos;
	}


	public int getSueldo() {
		return sueldo;
	}


	public int getAntiguedad() {
		return antiguedad;
	}

	public String getCategoria(String categoria) {
		return categoria;
	}
	
	@Override
	public String toString() {
		return "empleado [nombre=" + nombre + ", apellidos=" + apellidos + ",categoría= "+categoria+", sueldo=" + sueldo + ", antiguedad="
				+ antiguedad + "]";
	}


	
	public static void main(String[] args) throws FileNotFoundException, IOException, ClassNotFoundException {
		
		empleado[] personal=new empleado[3];
		
		
		personal[0]=new empleado ("Juan","Pérez","Jefe de departamento",3000,25);
		personal[1]=new empleado("Andrea","Aguilar","becaria",570,1);
		personal[2]=new empleado("Jorge","Guillén","Agente de ventas",1500,15);
		
		System.out.println("Los empleados de la empleados de la empresa son los siguientes:");
		System.out.println();
		for(int i=0;i<personal.length;i++) {
			System.out.println(personal[i]);
		}
		
		//Serialización:
		
		
			//Creamos el flujo de datos externo
			ObjectOutputStream fichero_empleados=new ObjectOutputStream(new FileOutputStream("C:/Users/User/Desktop/empleado.dat"));
			
			//Escribimos el contenido del array en el fichero
			fichero_empleados.writeObject(personal);
			
			//Cerramos el fichero
			fichero_empleados.close();
			
			//Recuperamos el archivo y lo pasamos de .dat a tipo object al programa
			ObjectInputStream recuperar_fichero=new ObjectInputStream(new FileInputStream ("C:/Users/User/Desktop/empleado.dat"));
			empleado[] personal_recuperado=(empleado[])recuperar_fichero.readObject();
			recuperar_fichero.close();
			System.out.println();
			System.out.println("El personal recuperado es: ");
			System.out.println();
			for(empleado e:personal_recuperado) {
				System.out.println(e);
			}
		
	}

}
