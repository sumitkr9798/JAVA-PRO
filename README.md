import java.util.Scanner;

    class Complaint {
        int id;
        String description;
        String status;
        String assignedTo;

        Complaint(int id, String description) {
            this.id = id;
            this.description = description;
            this.status = "Open";
            this.assignedTo = "Unassigned";
        }

        void display() {
            System.out.println("ID: " + id);
            System.out.println("Description: " + description);
            System.out.println("Status: " + status);
            System.out.println("Assigned To: " + assignedTo);
            System.out.println("-----------------------------------");
        }
    }

    public class ComplaintManagementSystem {
        static Complaint[] complaints = new Complaint[100];
        static int count = 0;

        public static void main(String[] args) {
            Scanner sc = new Scanner(System.in);
            int choice;

            do {
                System.out.println("\n--- Complaint Management System ---");
                System.out.println("1. Record New Complaint");
                System.out.println("2. Update Complaint Status");
                System.out.println("3. Assign Complaint to Staff");
                System.out.println("4. Search Complaint by ID");
                System.out.println("5. Display All Open Complaints");
                System.out.println("6. Exit");
                System.out.print("Enter your choice: ");
                choice = sc.nextInt();
                sc.nextLine();  // consume newline

                switch (choice) {
                    case 1:
                        addComplaint(sc);
                        break;
                    case 2:
                        updateStatus(sc);
                        break;
                    case 3:
                        assignComplaint(sc);
                        break;
                    case 4:
                        searchById(sc);
                        break;
                    case 5:
                        displayOpenComplaints();
                        break;
                    case 6:
                        System.out.println("Exiting system. Goodbye!");
                        break;
                    default:
                        System.out.println("Invalid choice!");
                }
            } while (choice != 6);

            sc.close();
        }

        static void addComplaint(Scanner sc) {
            System.out.print("Enter complaint description: ");
            String desc = sc.nextLine();
            complaints[count] = new Complaint(count + 1, desc);
            System.out.println("Complaint recorded with ID: " + (count + 1));
            count++;
        }

        static void updateStatus(Scanner sc) {
            System.out.print("Enter complaint ID to update status: ");
            int id = sc.nextInt();
            sc.nextLine();
            Complaint c = findById(id);
            if (c != null) {
                System.out.print("Enter new status (Open/In Progress/Resolved): ");
                c.status = sc.nextLine();
                System.out.println("Status updated.");
            } else {
                System.out.println("Complaint not found.");
            }
        }

        static void assignComplaint(Scanner sc) {
            System.out.print("Enter complaint ID to assign: ");
            int id = sc.nextInt();
            sc.nextLine();
            Complaint c = findById(id);
            if (c != null) {
                System.out.print("Enter staff name: ");
                c.assignedTo = sc.nextLine();
                System.out.println("Complaint assigned.");
            } else {
                System.out.println("Complaint not found.");
            }
        }

        static void searchById(Scanner sc) {
            System.out.print("Enter complaint ID to search: ");
            int id = sc.nextInt();
            Complaint c = findById(id);
            if (c != null) {
                System.out.println("--- Complaint Details ---");
                c.display();
            } else {
                System.out.println("Complaint not found.");
            }
        }

        static void displayOpenComplaints() {
            System.out.println("\n--- Open Complaints ---");
            boolean found = false;
            for (int i = 0; i < count; i++) {
                if (complaints[i].status.equalsIgnoreCase("Open")) {
                    complaints[i].display();
                    found = true;
                }
            }
            if (!found) {
                System.out.println("No open complaints.");
            }
        }

        static Complaint findById(int id) {
            for (int i = 0; i < count; i++) {
                if (complaints[i].id == id) {
                    return complaints[i];
                }
            }
            return null;
        }
    }
