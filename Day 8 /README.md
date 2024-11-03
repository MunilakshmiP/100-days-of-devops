# Simple System Resource Monitor & Todo List Manager (  Bash Scripting Projects)



Hey there, fellow learners! Welcome to Day 8 of our 100 Days of DevOps journey. Today, I’m excited to share two beginner-friendly Bash scripting projects that will enhance your command line skills and help you automate some everyday tasks. Let’s dive in!

### Project 1: Simple System Resource Monitor

Have you ever wanted to keep an eye on your system’s performance without digging through complex tools? Well, our **Simple System Resource Monitor** is here to save the day!

#### What It Does

This handy script allows you to log and view essential system stats, like CPU usage, memory consumption, and disk space. It’s straightforward and runs smoothly in Git Bash, making it perfect for anyone starting with scripting.

#### Here’s How It Works:

1.  **Logging Stats**: The script logs the current date and time, CPU load, memory used, and disk usage to a file called `system_monitor.log`. Just think of it as a performance diary for your system!
    
2.  **Viewing Stats**: If you want to check what’s been logged, you can easily view the last 20 entries. It’s like having a quick snapshot of your system’s health!
    
3.  **User-Friendly Menu**: The script presents a simple menu where you can choose to log stats, view recent stats, or exit. It’s designed to be intuitive, even for those new to scripting.
    

#### Here’s the Code:

```plaintext
#!/bin/bash

# Simple System Resource Monitor (Git Bash Compatible)
LOG_FILE="$HOME/system_monitor.log"  # Log file to store resource usage

# Function to log current system stats
log_stats() {
    echo "---- $(date) ----" >> "$LOG_FILE"
    echo "CPU Usage:" >> "$LOG_FILE"
    top -bn1 | grep "Cpu(s)" | awk '{print "CPU Load: " $2 + $4 "%"}' >> "$LOG_FILE"  # Logs CPU load
    echo "Memory Usage:" >> "$LOG_FILE"
    top -bn1 | grep "Mem" | awk '{print "Memory Used: " $6 " / " $4}' >> "$LOG_FILE"  # Logs memory usage
    echo "Disk Usage:" >> "$LOG_FILE"
    df -h | grep "/$" | awk '{print "Disk Usage: " $5}' >> "$LOG_FILE"  # Logs disk usage of root
    echo "--------------------------" >> "$LOG_FILE"
    echo "Logged current stats."
}

# Function to display recent stats
view_stats() {
    tail -20 "$LOG_FILE"
}

# Main script logic
while true; do
    echo "System Resource Monitor"
    echo "1. Log Current Stats"
    echo "2. View Recent Stats"
    echo "3. Exit"
    read -p "Select an option [1-3]: " option
    case $option in
        1) log_stats ;;
        2) view_stats ;;
        3) echo "Exiting."; break ;;
        *) echo "Invalid option. Please select again." ;;
    esac
done
```

----------

### Project 2: Todo List Manager

Now, let’s shift gears to something a bit more personal and practical—the **Todo List Manager**.

#### Why You’ll Love It

If you’re anything like me, keeping track of tasks can sometimes feel overwhelming. This script is here to help you organize your tasks seamlessly.

#### How It Works:

1.  **Task Management**: You can view your current tasks, add new ones, mark them as complete, or delete them—all through a simple command line interface.
    
2.  **Task Tracking**: Each task is stored in a `todo.txt` file, allowing you to keep track of what you need to do without any complicated setup.
    
3.  **Interactive Menu**: Similar to our system monitor, this project features a user-friendly menu, making it easy for you to interact with your tasks.
    

#### Here’s the Code:

```plaintext
#!/bin/bash

# Todo List Manager Script

TODO_FILE="todo.txt"  # File to store tasks

# Function to display tasks
view_tasks() {
    echo "Your Tasks:"
    if [ ! -f "$TODO_FILE" ]; then
        echo "No tasks yet!"
        return
    fi
    nl -w 2 -s ". " "$TODO_FILE"  # Display tasks with line numbers
}

# Function to add a task
add_task() {
    read -p "Enter a new task: " task
    echo "[ ] $task" >> "$TODO_FILE"
    echo "Added task: $task"
}

# Function to mark a task as complete
complete_task() {
    view_tasks
    read -p "Enter the number of the task to mark as complete: " num
    sed -i "${num}s/\[ \]/[x]/" "$TODO_FILE"
    echo "Task $num marked as complete."
}

# Function to delete a task
delete_task() {
    view_tasks
    read -p "Enter the number of the task to delete: " num
    sed -i "${num}d" "$TODO_FILE"
    echo "Task $num deleted."
}

# Main script logic
while true; do
    echo "Todo List Manager"
    echo "1. View Tasks"
    echo "2. Add Task"
    echo "3. Complete Task"
    echo "4. Delete Task"
    echo "5. Exit"
    read -p "Select an option [1-5]: " option
    case $option in
        1) view_tasks ;;
        2) add_task ;;
        3) complete_task ;;
        4) delete_task ;;
        5) echo "Goodbye!"; break ;;
        *) echo "Invalid option. Please select again." ;;
    esac
done
```

----------

### Conclusion

Today, we’ve explored two practical Bash scripting projects: the **Simple System Resource Monitor** and the **Todo List Manager**. Each of these projects serves a unique purpose and can be expanded upon as you become more comfortable with Bash scripting.

These projects not only showcase the power of Bash but also help you develop skills that are incredibly useful in the world of DevOps and automation. I encourage you to try them out, tweak them, and maybe even expand their functionalities.

Remember, the journey of learning is all about experimentation and practice, so don’t hesitate to dive in and make these scripts your own. Happy scripting, and see you on Day  9 of our 100 Days journey!
