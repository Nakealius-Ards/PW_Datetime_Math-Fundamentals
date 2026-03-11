"""
Developer: Nakealius D. Ards
Date: 20 January 2026
Purpose: This application with prompt the user to select from a menu that serves multiple functions.
Based on the user's input, the application will perform a computation and prompt the user to return
to the main menu or exit the program
"""

# COMMUNITY PROJECT NOTE:
# - Avoid adding personal identifiers in comments or code.
# - Document new features clearly for contributors.
# - Keep functions modular so they can be reused or extended.

import math
import sys
from datetime import date

def generate_password():
    """Get the user input for a password that meet the following requirements:
    A uppercase letter, a lowercase letter, a number, a special character, and
    the string must be 12-18 characters long."""

    print("Please follow the below instructions to generate a secure password:\n"
           "The password must contain at least one uppercase letter, a lowercase letter, a number,"
          "and at least one special character. Finally,the password must be "
          "12-18 characters.\n")


    missed_input = 0 # Constant missed input variable for counting invalid entries

    while True:
        password_input = input("Please enter a password: ")

        uppercase_count = 0
        lowercase_count = 0
        special_count = 0
        numbers_count = 0
        char_list = ['!', '@', '#', '$', '%', '^', '&', '*', '(', ')', '-',
                     '_', '+', '=', '{', '[', ']', '}', ':', ';', ',', '/']

        for i in password_input:  # Check for all required password criteria
            if i.isupper():  # Check for an uppercase letter in the input
                uppercase_count += 1
            elif i.islower():  # Check for a lowercase letter in the input
                lowercase_count += 1
            elif i.isdigit():  # Check for a number in the input
                numbers_count += 1
            elif i in char_list:  # Check for a special character in the input
                special_count += 1

        # Throw an exception error if there are no uppercase letters, lowercase letters,
        # special characters, or numbers present in the password.
        if uppercase_count <= 0 or lowercase_count <= 0:
            print("Your password must contain at least one uppercase & one lowercase letter.")
            missed_input += 1
        elif special_count <= 0 or numbers_count <= 0:
            print("Your password must contain at least one special character & one number.")
            missed_input += 1
        # Check to see if the password is 12-18 characters
        elif len(password_input) < 12 or len(password_input) > 18:
            print("Password is either too short or too long. Please enter 12-18 characters.")
            missed_input += 1
            # print(missed_input) Check to make sure inputs are being counted
        else:
            print("Password Accepted!")
            break

        if missed_input >= 3:
            retry_prompt()


def percentage():
    """Get input from the user for number 1, number 2, and the numbers after the decimal place
    for the output. Then completes a computation to print the output."""
    missed_input = 0
    while True:
        try:
            num1 = float(input("Please enter your first number to calculate the percentage: "))
            num2 = float(input("Please enter your second number to calculate the percentage: "))
            decimal_nums = int(input("Please enter your decimal position to calculate "
                                     "the percentage: "))
            # Divide the two value to get the result prior to moving decimal place
            result = num1 / num2
            # Create a computation to move the decimal by the number specified by the user's input
            final_result = round((result * 100), decimal_nums)
            print(final_result)
            back_menu_option()

        except ValueError:
            print("Invalid Entry! Please try again.")
            missed_input += 1
            if missed_input >= 3:
                retry_prompt()

def day_countdown(): 
    """Get the date input from the user subtract the amount of days from the target date"""
    missed_input = 0
    # Get the user's target date
    today = date.today() # Get today's date
    while True:
        #Initiate a while loop to continue the cycle until the correct input is entered
        try: # Try to get the user date in a Month Day, Year format
            user_date = input("Please enter the date you would like to count down to "
                        "in (Month Day, Year) format: ")
            # Store the string as a date variable in a Month Day, Year format
            user_to_date = date.strptime(user_date, "%B %d, %Y")
            user_date_format = date.strftime(user_to_date, "%B %d, %Y")

            days_left = (user_to_date - today).days # Get the number of remaining days
            # Print days left from the date the user entered
            print(f"There are {days_left} days from today to {user_date_format}.")
            break
        except ValueError: # Throw error if the input in invalid
            print("Invalid Entry! Please try again.")
            missed_input += 1
            if missed_input >= 3:
                retry_prompt()

def law_of_cosines(): 
    """Gather the necessary input from the user and create a computation to
    calculate the leg of a triangle using the Law of Cosines"""
    missed_input = 0
    while True:
        try:
            a = float(input("Please enter side a to calculate side c: "))
            b = float(input("Please enter side b to calculate side c: "))
            c_degrees = float(input("Please enter angle C in degrees: "))

            # Convert degrees to radians
            c_radians = math.radians(c_degrees)

            # Computation to apply the law of cosine formula
            c = math.sqrt((a ** 2) + (b ** 2) -  (2 * (a * b) * math.cos(c_radians)))

            result = round(c, 2) # Round the result to 2 decimal places
            print(result) # Print the output
            back_menu_option()

        except ValueError:  # Throw error if the input in invalid
            print("Invalid Entry! Please try again.")
            missed_input += 1
            if missed_input >= 3:
                retry_prompt()

def cylinder():
    """Get the necessary input from the user and create a computation for
    determining the volume of a circular cylinder"""
    missed_input = 0

    while True:
        try:
            # Get the values of the cylinder from the user
            radius = float(input("Please enter the radius of the cylinder: "))
            height = float(input("Please enter the height of the cylinder: "))
            # Computation for determining the volume of the cylinder
            volume = round((math.pi * (radius ** 2)) * height, 2)
            # Print the result
            print(volume)
            back_menu_option()

        except ValueError:
            print("Invalid Entry! Please try again.")
            missed_input += 1
            if missed_input >= 3:
                retry_prompt()

def option_menu(): # Input way to go back to main menu
    """Display a menu for the user to select which application to use."""
    missed_input = 0

    while True:
        welcome_prompt = input("Welcome to the Lab 2 multi-menu python application. "
                                "Please select from the following menu to proceed:\n"
                                "A) For the Secure Password Generator\n"
                                "B) To calculate and format a percentage\n"
                                "C) To calculate how many days are in between another date\n"
                                "D) To calculate the leg of a triangle using the Law of Cosine\n"
                                "E) To calculate the volume of a Right Circular Cylinder\n"
                                "F) To exit the program\n"
                                "Enter your choice: ")

        # Options for the user to choose from
        if welcome_prompt.lower() == "a":
            generate_password()
            back_menu_option()
        elif welcome_prompt.lower() == "b":
            percentage()
            back_menu_option()
        elif welcome_prompt.lower() == "c":
            day_countdown()
            back_menu_option()
        elif welcome_prompt.lower() == "d":
            law_of_cosines()
            back_menu_option()
        elif welcome_prompt.lower() == "e":
            cylinder()
            back_menu_option()
        elif welcome_prompt.lower() == "f":
            thank_you_prompt()
            sys.exit()
        else:
            print("Invalid Input! Please try again.")
            missed_input += 1
            if missed_input >= 3:
                retry_prompt()

def back_menu_option():
    """Prompt the user to go back to the main menu."""
    while True:
        back2menu = input("Would you like to go back to the main menu? (Yes or No): ")
        if back2menu.lower() == "yes":
            option_menu()
        elif back2menu.lower() == "no":
            thank_you_prompt()
            sys.exit()
        else:
            print("Invalid Input! Please try again.")

def retry_prompt():
    """Prompt the user to go end or reattempt the application."""
    while True:
        missed_input_check = input("Would you like to try again? (Yes or No): ")
        if missed_input_check.lower() == "no":
            thank_you_prompt()
            sys.exit()
        elif missed_input_check.lower() == "yes":
            break
        else:
            print("Invalid input. Please enter Yes or No.")

def thank_you_prompt():
    """Thank the user for using the application."""
    print("Thank you for using the Lab 2 multi-menu python application. ")


def main():
    """Main function"""
    option_menu()

main()

# TODO (Community Ideas):
# - Add more math functions (e.g., quadratic solver, statistics).
# - Export results to a file (CSV/JSON).
# - Add error logging for invalid inputs.
