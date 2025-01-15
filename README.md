# countdown-timer-calculator
import time
import threading

def countdown(seconds):
    while seconds > 0:
        mins, secs = divmod(int(seconds), 60)
        timer = f'{mins:02d}:{secs:02d}'
        print(f"\rTimer: {timer}", end='')
        time.sleep(1)
        seconds -= 1
    print("\nTime's up!")

def perform_arithmetic():
    print("\n--- Basic Arithmetic Operations ---")
    print("1. Addition")
    print("2. Subtraction")
    print("3. Multiplication")
    print("4. Division")
    try:
        choice = input("Select an operation (1-4): ")
        if choice not in ['1', '2', '3', '4']:
            print("Invalid operation selected.")
            return
        num1 = float(input("Enter the first number: "))
        num2 = float(input("Enter the second number: "))

        if choice == '1':
            result = num1 + num2
        elif choice == '2':
            result = num1 - num2
        elif choice == '3':
            result = num1 * num2
        elif choice == '4':
            if num2 != 0:
                result = num1 / num2
            else:
                print("Error: Division by zero is not allowed.")
                return
        print(f"Result: {result}")
    except ValueError:
        print("Invalid input. Please enter numeric values.")

def start_timer():
    while True:
        print("\n--- Countdown Timer & calculator ---")
        print("1. Start Timer")
        print("2.calculator")
        print("3. Exit")
        choice = input("Select an option: ")
        
        if choice == '1':
            try:
                user_input = float(input("Enter the countdown time in seconds: "))
                if user_input > 0:
                    timer_thread = threading.Thread(target=countdown, args=(int(user_input),))
                    timer_thread.start()
                else:
                    print("Please enter a positive number.")
            except ValueError:
                print("Invalid input. Please enter a valid number.")
        elif choice == '2':
            perform_arithmetic()
        elif choice == '3':
            print("Exiting the application. Goodbye!")
            break
        else:
            print("Invalid choice. Please select 1, 2, or 3.")

if __name__ == "__main__":
    start_timer()
