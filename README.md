import datetime

vehicles = {
    1: ["Maruti Swift", 1500, True],
    2: ["Honda City", 2000, True],
    3: ["Royal Enfield", 1200, True],
    4: ["Activa 6G", 500, True]
}

rented = {}

def show_vehicles():
    print("\nAvailable Vehicles")
    for vid, v in vehicles.items():
        status = "Available" if v[2] else "Rented"
        print(vid, "-", v[0], "- ₹", v[1], "-", status)

def rent_vehicle():
    try:
        vid = int(input("Enter Vehicle ID: "))
        if vid in vehicles and vehicles[vid][2]:

            name = input("Customer Name: ")
            days = int(input("Rental Days: "))

            amount = vehicles[vid][1] * days
            vehicles[vid][2] = False

            rented[vid] = [name, days, amount, datetime.date.today()]

            print("Vehicle Rented")
            print("Amount = ₹", amount)

            save_data()

        else:
            print("Vehicle Not Available")

    except:
        print("Invalid Input")

def return_vehicle():
    try:
        vid = int(input("Enter Vehicle ID: "))

        if vid in rented:
            vehicles[vid][2] = True
            del rented[vid]
            save_data()
            print("Vehicle Returned")

        else:
            print("Vehicle Not Found")

    except:
        print("Invalid Input")

def show_rented():
    print("\nRented Vehicles")

    if not rented:
        print("No Vehicles Rented")

    for vid, d in rented.items():
        print(vid, d)

def save_data():
    with open("rental_data.txt", "w") as f:
        for vid, d in rented.items():
            f.write(f"{vid},{d}\n")

while True:

    print("""
1. Show Vehicles
2. Rent Vehicle
3. Return Vehicle
4. Show Rented Vehicles
5. Exit
""")

    choice = input("Enter Choice: ")

    if choice == "1":
        show_vehicles()

    elif choice == "2":
        rent_vehicle()

    elif choice == "3":
        return_vehicle()

    elif choice == "4":
        show_rented()

    elif choice == "5":
        break

    else:
        print("Invalid Choice")
