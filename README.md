package programacion;

import java.util.Scanner;


public class main {

    public static void salida(int a) {
        if ( a == 0) {
            System.out.println("Se ha quedado sin intentos");
            System.out.println("Su cuenta sera bloqueada");
            System.exit(0);
        }
    }

    public static void main(String[] args) {
        Scanner entrada = new Scanner(System.in);

        String nombre = "Angel Gabriel Rivas Arreola"; //aqui Guardo las variables para un cajero de una sola persona o datos fijos.
        double saldon = 1_000.00;
        double totaldepo = 0;
        int nc = 3017, pin = 2026;
        int comisionr = 10;
        int incorrecto = 0, depositoex = 0; //uso esta variable para datos o contadores
        int pint, opcion; // Guardo las opciones para guardar datos


            for (int i = 1; i <= 3; i++) {
                System.out.print("INGRESE PIN (Intento " + i + " de " + 3 + "): ");
                pint = entrada.nextInt();

                if (pint == pin) {
                    // Si el PIN es correcto,saldra anticipadamente.
                    break;
                } else {
                    System.out.println("Ese no es su PIN.");
                    if (i == 3) {
                        salida(0);
                    }
                }
            }

        do{
            System.out.println("--------------Menu--------------");
            System.out.println("1. Consultar saldo: ");
            System.out.println("2. Depositar dinero:");
            System.out.println("3. Realizar retiro normal: ");
            System.out.println("4. Realizar retiro con comisión: ");
            System.out.println("5. Mostrar resumen de la sesión: ");
            System.out.println("6. Salir: ");
            opcion = entrada.nextInt();

            switch (opcion) {

                case 1:
                    System.out.println("Nombre del titular: "+ nombre);
                    System.out.println("Numero de cuente: " + nc);
                    System.out.println("Saldo disponible: Q" +saldon + "0");

                    break;

                case 2:

                    System.out.println("Ingrese el monto a depositar.");
                    double deposito = entrada.nextDouble();


                    while ( deposito <= 0 || deposito > 5000){

                        System.out.println("El monto a depositar no debe ser menor a 0 ni mayor de 5000");


                        System.out.println("Ingrese el monto a depositar.");
                        deposito = entrada.nextDouble();

                    }
                    
                    depositoex++;
                    totaldepo += deposito;
                    System.out.println("Monto depositado: " + deposito);
                    System.out.println("Saldo anterior: " +saldon + "0");
                    saldon = saldon + deposito;
                    System.out.println("Saldo actualizado: " + saldon + "0");




                    break;

                case 3:
                    System.out.println("Hola");
                    break;

                case 4:
                    System.out.println("Hola");
                    break;

                case 5:
                    System.out.println("Hola");
                    break;

                default:
                    System.out.println("esa opcion no existe");
                    incorrecto++;
                    continue;
            }
        }

        while(opcion != 6);

    }
}
