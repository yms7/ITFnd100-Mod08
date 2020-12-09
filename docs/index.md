# Title
**Dev:** *YSon*
**Date:** *12.05.2020*

## Assignment 08
...

```
# ------------------------------------------------------------------------ #
# Title: Assignment 08 Yong Son
# Description: Working with classes
# ChangeLog (Who,When,What):
# RRoot,1.1.2030,Created started script
# RRoot,1.1.2030,Added pseudo-code to start assignment 8
# YSon,12.6.2020,Modified code to complete assignment 8
# YSon,12.8.2020,Modified code to fix comments field and add exception class
# ------------------------------------------------------------------------ #

# Data ------------------------------------------------------------------- #
strFileName = 'products.txt'
lstOfProductObjects = []
strChoice = ""  # Captures the user option selection
strStatus = ""  # Captures the status of an processing functions

class InvalidChoice(Exception):
    def __str__(self):
        return 'Please enter the valid menu options'

class Product:
    # -- Constructor --
    def __init__(self, product_name: str, product_value: int):
        """ Sets initial values and returns a Product object """
        # -- Attributes --
        self.__product_name = product_name
        self.__product_value = product_value
    """Stores data about a product:
    properties:
        product_name: (string) with the products's name
        product_price: (float) with the products's standard price
    """
    # --Properties--
    @property
    def product_name(self):  # (getter or accessor)
        return str(self.__product_name).title()  # Title case

    @product_name.setter  # The NAME MUST MATCH the property's!
    def product_name(self, value):  # (setter or mutator)
        if str(value).isnumeric() == False:
            self.__product_name = value
        else:
            raise Exception("Names cannot be numbers")

    @property  # DON'T USE NAME for this directive!
    def product_value(self):  # (getter or accessor)
        return str(self.__product_value).title()  # Title case

    @product_value.setter  # The NAME MUST MATCH the property's!
    def product_value(self, value):  # (setter or mutator)
        if int(value).isnumeric() == True:
            self.__product_value = value
        else:
            raise Exception("Product value must be numbers")
    pass
    # -- Methods --
    def __str__(self):
        return self.__str__()

    def __str__(self):
        return self.__product_name + ',' + self.__product_value

# Data -------------------------------------------------------------------- #

# Processing  ------------------------------------------------------------- #
class FileProcessor:
    """Processes data to and from a file and a list of product objects:
    methods:
        save_data_to_file(file_name, list_of_product_objects):
        read_data_from_file(file_name): -> (a list of product objects)
    """
    def write_data_to_file(file_name, list_of_product_objects):
        file = open(file_name, "w")
        for row in list_of_product_objects:
            file.write(row["Name"] + ',' + row["Value"] + '\n')
        file.close()
        return list_of_product_objects, 'Success'
    pass

    def read_data_from_file(file_name, list_of_product_objects):
        """ Reads data from a file into a list of dictionary rows
        :param file_name: (string) with name of file:
        :param list_of_product_objects: (list) you want filled with file data:
        :return: (list) of dictionary rows
        """
        list_of_product_objects.clear()  # clear current data
        file = open(file_name, "r")
        for line in file:
            name, value = line.split(",")
            row = {"Name": name.strip(), "Value": value.strip()}
            list_of_product_objects.append(row)
        file.close()
        return list_of_product_objects, 'Success'

    def add_data_to_list(name, value, list_of_product_objects):
        row = {"Name": name, "Value": value}
        list_of_product_objects.append(row)
        return list_of_product_objects, 'Success'

# Processing  ------------------------------------------------------------- #

# Presentation (Input/Output)  -------------------------------------------- #
class IO:
    # TODO: Add docstring
    def __doc__(self):
        return 'This class holds product data'
    def __str__(self):
        return self.__product_name + ',' + self.__product_value
    pass

    # TODO: Add code to show menu to user
    def print_menu():
        """  Display a menu of choices to the user
        :return: nothing
        """
        print('''
        Menu of Options
        1) Add a new product and value
        2) Save Data to File        
        3) Reload Data from File
        4) Exit Program
        ''')

    # TODO: Add code to get user's choice
    def input_menu_choice():
        """ Gets the menu choice from a user
        :return: string"""
        choice = str(input("Which option would you like to perform? [1 to 4] - ")).strip()
        return choice

    # TODO: Add code to show the current data from the file to user
    def print_current_Tasks_in_list(list_of_product_objects):
        print("******* The current products and values are: *******")
        for row in list_of_product_objects:
            print(row["Name"] + " (" + row["Value"] + ")")
        print("*******************************************")

    # TODO: Add code to get product data from user
    def input_new_task_and_priority():
        name = str(input("Please enter a new product name: ")).strip()
        value = str(input("What is the value of the product: ")).strip()
        return name, value

    def input_press_to_continue(optional_message=''):
        """ Pause program and show a message before continuing
        :param optional_message:  An optional message you want to display
        :return: nothing
        """
        print(optional_message)
        input('Press the [Enter] key to continue.')

    def input_yes_no_choice(message):
        """ Gets a yes or no choice from the user
        :return: string
        """
        return str(input(message)).strip().lower()

# Presentation (Input/Output)  -------------------------------------------- #

# Main Body of Script  ---------------------------------------------------- #
# TODO: Add Data Code to the Main body
# Load data from file into a list of product objects when script starts
# Step 1 - When the program starts, Load data from ToDoFile.txt.
FileProcessor.read_data_from_file(strFileName, lstOfProductObjects)  # read file data

# Step 2 - Display a menu of choices to the user
while True:
    # Step 3 Show current data
    IO.print_current_Tasks_in_list(lstOfProductObjects)  # Show current data in the list/table
# Show user a menu of options
    IO.print_menu()  # Shows menu
# Get user's menu option choice
    strChoice = IO.input_menu_choice()  # Get menu option
    # Show user current data in the list of product objects
    # Let user add data to the list of product objects
    # let user save current data to file and exit program
# Main Body of Script  ---------------------------------------------------- #
    # Step 4 - Process user's menu choice
    try:
        if strChoice.strip() == '1':  # Add a new Task
            strName, strValue = IO.input_new_task_and_priority()
            FileProcessor.add_data_to_list(strName, strValue, lstOfProductObjects)
            IO.print_current_Tasks_in_list(lstOfProductObjects)
            IO.input_press_to_continue(strStatus)
            continue  # to show the menu

        elif strChoice == '2':   # Save Data to File
            strChoice = IO.input_yes_no_choice("Save this data to file? (y/n) - ")
            if strChoice.lower() == "y":
                print("Following data will be save to a file: ")
                IO.print_current_Tasks_in_list(lstOfProductObjects)
                FileProcessor.write_data_to_file(strFileName, lstOfProductObjects)
                IO.input_press_to_continue(strStatus)
            else:
                IO.input_press_to_continue("Save Cancelled!")
            continue  # to show the menu

        elif strChoice == '3':  # Reload Data from File
            print("Warning: Unsaved Data Will Be Lost!")
            strChoice = IO.input_yes_no_choice("Are you sure you want to reload data from file? (y/n) -  ")
            if strChoice.lower() == 'y':
                FileProcessor.read_data_from_file(strFileName, lstOfProductObjects)
                IO.print_current_Tasks_in_list(lstOfProductObjects)
                IO.input_press_to_continue(strStatus)
            else:
                IO.input_press_to_continue("File Reload  Cancelled!")
            continue  # to show the menu

        elif strChoice == '4':  #  Exit Program
            print("Goodbye!")
            break   # and Exit
        else:
            raise InvalidChoice()

    except Exception as e:
        print("The Python error message: ")
        print(e, "\n")
```
