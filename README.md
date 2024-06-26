# Simple-task-list
A basic Java application that allows users to create a task list, where Users are able to add, remove, and list tasks.
import java.util.ArrayList;
import java.util.Scanner;

/**
 * This class implements a simple Task List application.
 * Users can add tasks, remove tasks, list all tasks, and quit the application.
 */
public class TaskListApp {
    private static final Scanner scanner = new Scanner(System.in);
    private static final TaskList taskList = new TaskList();

    /**
     * Main method to start the Task List application.
     * @param args Command-line arguments (not used)
     */
    public static void main(String[] args) {
        while (true) {
            displayMenu();
            int choice = getUserChoice();

            switch (choice) {
                case 1:
                    addTask();
                    break;
                case 2:
                    removeTask();
                    break;
                case 3:
                    listTasks();
                    break;
                case 4:
                    exitApp();
                    return;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }

    /**
     * Displays the menu options for the Task List application.
     */
    private static void displayMenu() {
        System.out.println("\nTask List Application");
        System.out.println("1. Add Task");
        System.out.println("2. Remove Task");
        System.out.println("3. List Tasks");
        System.out.println("4. Quit");
        System.out.print("Select an option: ");
    }

    /**
     * Gets the user's choice from the menu.
     * @return User's menu choice
     */
    private static int getUserChoice() {
        while (true) {
            try {
                return Integer.parseInt(scanner.nextLine());
            } catch (NumberFormatException e) {
                System.out.print("Invalid input. Please enter a number: ");
            }
        }
    }

    /**
     * Adds a new task to the task list.
     */
    private static void addTask() {
        System.out.print("Enter task name: ");
        String taskName = scanner.nextLine().trim();
        taskList.addTask(taskName);
    }

    /**
     * Removes a task from the task list.
     */
    private static void removeTask() {
        if (taskList.isEmpty()) {
            System.out.println("No tasks to remove.");
            return;
        }

        listTasks();
        int taskNumber = getTaskNumber("Enter the task number to remove: ");
        if (taskNumber != -1) {
            taskList.removeTask(taskNumber);
        }
    }

    /**
     * Lists all tasks currently in the task list.
     */
    private static void listTasks() {
        if (taskList.isEmpty()) {
            System.out.println("No tasks to list.");
        } else {
            taskList.listTasks();
        }
    }

    /**
     * Exits the Task List application.
     */
    private static void exitApp() {
        System.out.println("Exiting Task List Application. Goodbye!");
        scanner.close();
        System.exit(0);
    }

    /**
     * Helper method to get a valid task number from the user.
     * @param prompt Prompt message to display
     * @return Valid task number entered by the user
     */
    private static int getTaskNumber(String prompt) {
        while (true) {
            try {
                System.out.print(prompt);
                int taskNumber = Integer.parseInt(scanner.nextLine());
                if (taskList.isValidTaskNumber(taskNumber)) {
                    return taskNumber;
                } else {
                    System.out.println("Invalid task number. Please try again.");
                }
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a number.");
            }
        }
    }
}

/**
 * Represents a Task List that stores tasks and provides operations to manipulate them.
 */
class TaskList {
    private final ArrayList<String> tasks = new ArrayList<>();

    /**
     * Adds a task to the task list.
     * @param name Task name to add
     */
    public void addTask(String name) {
        tasks.add(name);
        System.out.println("Task added.");
    }

    /**
     * Removes a task from the task list.
     * @param taskNumber Index of the task to remove (1-based)
     */
    public void removeTask(int taskNumber) {
        String removedTask = tasks.remove(taskNumber - 1);
        System.out.println("Removed task: " + removedTask);
    }

    /**
     * Lists all tasks currently in the task list.
     */
    public void listTasks() {
        System.out.println("\nTasks:");
        for (int i = 0; i < tasks.size(); i++) {
            System.out.println((i + 1) + ". " + tasks.get(i));
        }
    }

    /**
     * Checks if the task list is empty.
     * @return true if the task list is empty, false otherwise
     */
    public boolean isEmpty() {
        return tasks.isEmpty();
    }

    /**
     * Checks if a given task number is valid (within range of current tasks).
     * @param taskNumber Task number to check
     * @return true if the task number is valid, false otherwise
     */
    public boolean isValidTaskNumber(int taskNumber) {
        return taskNumber >= 1 && taskNumber <= tasks.size();
    }
}


