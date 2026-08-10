package programacion;

import java.util.Scanner;


public class main {

    public static double pRetiro(Scanner entrada, double saldo) {// retiro sin comision
        double retiro;
        System.out.println("Ingrese el monto a retirar (Normal):");
        retiro = entrada.nextDouble();

        // Validaciones Retiro Normal
        if (retiro <= 0) { System.out.println("Rechazado: Monto inválido menor de 0."); return -1; }
        if (retiro > 2000) { System.out.println("Rechazado: Supera límite Q2000."); return -1; }
        if (retiro % 20 != 0) { System.out.println("Rechazado: Debe ser múltiplo de 20."); return -1; }
        if (retiro > saldo) { System.out.println("Rechazado: Fondos insuficientes."); return -1; }

        return retiro;
    }

    public static double pRetiro(Scanner entrada, double saldo, double comision) {// retiro con comision
        double retiro;
        System.out.println("Ingrese el monto a retirar (Red Externa):");
        retiro = entrada.nextDouble();


        if (retiro <= 0) { System.out.println("Rechazado: Monto inválido es menor de 0."); return -1; }
        if (retiro > 2000) { System.out.println("Rechazado: Supera límite Q2000."); return -1; }
        if (retiro % 20 != 0) { System.out.println("Rechazado: Debe ser múltiplo de 20."); return -1; }


        if (retiro + comision > saldo) {
            System.out.println("Rechazado: Fondos insuficientes para retiro + comisión.");
            return -1;
        }

        return retiro;
    }

    public static double vali(Scanner entrada) {

        double deposito;
        System.out.println("Ingrese el monto a depositar:");
        deposito = entrada.nextDouble();


        while (deposito <= 0 || deposito > 5000) {
            System.out.println("El monto a depositar no debe ser menor a 0 ni mayor de 5000");
            System.out.println("Ingrese el monto a depositar:");
            deposito = entrada.nextDouble();
        }

        return deposito; // 4. Retornamos 'deposito'
    }

    public static double vali(Scanner entrada, double saldo) {

            double retiro;
            System.out.println("Ingrese el monto a retirar:");
            retiro = entrada.nextDouble();

            if (retiro <= 0) {
                System.out.println("Rechazado: El monto debe ser mayor a Q0.00");
                return -1; // Valor especial para indicar error
            }
            if (retiro > 2000) {
                System.out.println("Rechazado: Supera el límite de Q2,000.00");
                return -1;
            }
            if (retiro % 20 != 0) {
                System.out.println("Rechazado: Debe ser múltiplo de Q20.00");
                return -1;
            }
            if (retiro > saldo) {
                System.out.println("Rechazado: Fondos insuficientes.");
                return -1;
            }

            return retiro; // Si llega aquí, es válido

    }

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
        double saldon = 1000.00, saldoInicial= 1000.00;
        double deposito = 0, retiro = 0; // datos de guardado
        double totaldepo = 0, totalr = 0, totalco = 0;
        int nc = 3017, pin = 2026;
        int comisionr = 10;
        int incorrecto = 0, depositoex = 0, retiroex = 0, retiroplus = 0; //uso esta variable para datos o contadores
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
                    System.out.println("Numero de cuenta: " + nc);
                    System.out.println("Saldo disponible: Q" +saldon + "0");

                    break;

                case 2:

                    deposito = vali(entrada); // uso de metodo para realizar el proceso usando el escaner para que lo use en base al pedir datos

                    depositoex++;
                    totaldepo += deposito;
                    System.out.println("Monto depositado: " + deposito);
                    System.out.println("Saldo anterior: " +saldon + "0");
                    saldon = saldon + deposito;
                    System.out.println("Saldo actualizado: " + saldon + "0");




                    break;

                case 3:
                    double montoRetiro = pRetiro(entrada, saldon);

                    if (montoRetiro == -1) {
                        retiroex++; // Incrementa rechazados
                        System.out.println("Operación rechazada. No se modificó el saldo.");
                        break;
                    }

                    // --- ÉXITO: Actualizar datos ---
                    double saldoAnterior = saldon;
                    saldon -= montoRetiro;      // Descontar solo el monto
                    totalr += montoRetiro;      // Acumular dinero entregado
                    retiroplus++;               // Incrementar éxitos

                    // --- Reporte Obligatorio ---
                    System.out.println("--- Retiro Normal Exitoso ---");
                    System.out.println("Monto solicitado: Q" + montoRetiro);
                    System.out.println("Saldo anterior: Q" + saldoAnterior);
                    System.out.println("Saldo actualizado: Q" + saldon);
                    System.out.println("Cantidad de retiros exitosos: " + retiroplus);
                    System.out.println("Total de dinero entregado en retiros: Q" + totalr);
                    break;

                case 4:
                    // Llamada a la versión sobrecargada de 3 parámetros
                    double montoSolicitado = pRetiro(entrada, saldon, comisionr);

                    if (montoSolicitado == -1) {
                        retiroex++; // Incrementa rechazados
                        System.out.println("Operación rechazada. No se modificó el saldo.");
                        break;
                    }

                    // --- ÉXITO: Actualizar datos ---
                    double saldoAnteriorComision = saldon;
                    double totalDebitado = montoSolicitado + comisionr;

                    saldon -= totalDebitado;    // Descontar monto + comisión
                    totalco += comisionr;    // Acumular comisiones (NO es dinero entregado al usuario)
                    totalr += montoSolicitado;  // Acumular solo el dinero que recibió el usuario
                    retiroplus++;               // Incrementar éxitos

                    // --- Reporte Obligatorio ---
                    System.out.println("--- Retiro con Comisión Exitoso ---");
                    System.out.println("Monto solicitado: Q" + montoSolicitado);
                    System.out.println("Comisión: Q" + comisionr);
                    System.out.println("Total debitado: Q" + totalDebitado);
                    System.out.println("Saldo anterior: Q" + saldoAnteriorComision);
                    System.out.println("Saldo actualizado: Q" + saldon);
                    System.out.println("Total acumulado de comisiones cobradas: Q" + totalco);
                    break;
                case 5:
                    System.out.println("\n--- RESUMEN DE LA SESIÓN ---");
                    System.out.println("Saldo inicial: Q" + saldoInicial);
                    System.out.println("Depósitos exitosos: " + depositoex);
                    System.out.println("Total depositado: Q" + totaldepo);
                    System.out.println("Retiros exitosos: " + retiroplus);
                    System.out.println("Total entregado en retiros: Q" + totalr); // Solo dinero al usuario
                    System.out.println("Total cobrado en comisiones: Q" + totalco); // Acumulado separado
                    System.out.println("Operaciones rechazadas: " + retiroex);
                    System.out.println("Opciones inválidas: " + incorrecto);
                    System.out.println("Saldo actual: Q" + saldon);
                    System.out.println("-----------------------------\n");
                    break;
                case 6:

                    System.out.println("--- RESUMEN FINAL DE SESIÓN ---");
                    System.out.println("Saldo inicial: Q" + saldoInicial);
                    System.out.println("Depósitos exitosos: " + depositoex);
                    System.out.println("Total depositado: Q" + totaldepo);
                    System.out.println("Retiros exitosos: " + retiroplus);
                    System.out.println("Total entregado en retiros: Q" + totalr);
                    System.out.println("Total cobrado en comisiones: Q" + totalco);
                    System.out.println("Operaciones rechazadas: " + retiroex);
                    System.out.println("Opciones inválidas: " + incorrecto);
                    System.out.println("Saldo actual: Q" + saldon);

                    System.out.println("\nGracias por usar el cajero, " + nombre + ". ¡Hasta luego!");

                    // Truco para salir
                    opcion = 6;
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
