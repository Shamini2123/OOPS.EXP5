# OOPS.EXP5
import java.util.*;
class Worker {
    protected String name;
    protected double salaryRate;
    protected double pay;

    public Worker(String name, double salaryRate) {
        this.name = name;
        this.salaryRate = salaryRate;
    }

   
    public void computePay(int hoursOrDays) {
        pay = 0;
    }

    public void displayPayDetails() {
        System.out.println("\n--- Worker Pay Details ---");
        System.out.println("Worker Name   : " + name);
        System.out.println("Salary Rate   : " + salaryRate);
        System.out.println("Pay           : " + pay);
    }
}

class DailyWorker extends Worker {
    public DailyWorker(String name, double salaryRate) {
        super(name, salaryRate);
    }

    @Override
    public void computePay(int no_of_days) {
        pay = no_of_days * salaryRate;
    }
}

class SalariedWorker extends Worker {
    public SalariedWorker(String name, double salaryRate) {
        super(name, salaryRate);
    }

    @Override
    public void computePay(int no_of_hours) {
      
        pay = 40 * salaryRate;
    }
}

public class WorkerAutomation {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Worker worker = null;

        System.out.println("Choose Worker Type:");
        System.out.println("1. Daily Worker");
        System.out.println("2. Salaried Worker");
        int choice = sc.nextInt();
        sc.nextLine(); // consume newline

        System.out.print("Enter Worker Name: ");
        String name = sc.nextLine();
        System.out.print("Enter Salary Rate: ");
        double rate = sc.nextDouble();

        if (choice == 1) {
            worker = new DailyWorker(name, rate);
        } else if (choice == 2) {
            worker = new SalariedWorker(name, rate);
        } else {
            System.out.println("Invalid Choice!");
            System.exit(0);
        }

        int option;
        do {
            System.out.println("\n--- Worker Pay Menu ---");
            System.out.println("1. Compute Pay");
            System.out.println("2. Display Pay Details");
            System.out.println("3. Exit");
            System.out.print("Enter choice: ");
            option = sc.nextInt();

            switch (option) {
                case 1:
                    if (worker instanceof DailyWorker) {
                        System.out.print("Enter No. of Days Worked: ");
                        int days = sc.nextInt();
                        worker.computePay(days);
                    } else if (worker instanceof SalariedWorker) {
                        System.out.print("Enter No. of Hours Worked: ");
                        int hours = sc.nextInt();
                        worker.computePay(hours);
                    }
                    System.out.println("Pay Computed Successfully!");
                    break;

                case 2:
                    worker.displayPayDetails();
                    break;

                case 3:
                    System.out.println("Exiting...");
                    break;

                default:
                    System.out.println("Invalid Option!");
            }
        } while (option != 3);

        sc.close();
    }
}
