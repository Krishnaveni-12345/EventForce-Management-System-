
import json
import os

FILE_NAME = "events.json"

def load_events():
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, "r") as file:
            return json.load(file)
    return []

def save_events(events):
    with open(FILE_NAME, "w") as file:
        json.dump(events, file, indent=4)

events = load_events()

def create_event():
    event = {
        "id": len(events) + 1,
        "name": input("Enter event name: "),
        "date": input("Enter event date: "),
        "location": input("Enter location: "),
        "participants": []
    }
    events.append(event)
    save_events(events)
    print("Event created successfully!")

def register_participant():
    event_id = int(input("Enter event ID: "))
    for event in events:
        if event["id"] == event_id:
            name = input("Participant name: ")
            email = input("Participant email: ")
            event["participants"].append({
                "name": name,
                "email": email
            })
            save_events(events)
            print("Participant registered successfully!")
            return
    print("Event not found!")

def view_events():
    for event in events:
        print("\nEvent ID:", event["id"])
        print("Name:", event["name"])
        print("Date:", event["date"])
        print("Location:", event["location"])
        print("Participants:", len(event["participants"]))

def main():
    while True:
        print("\n===== EVENTFORCE MANAGEMENT SYSTEM =====")
        print("1. Create Event")
        print("2. Register Participant")
        print("3. View Events")
        print("4. Exit")

        choice = input("Enter choice: ")

        if choice == "1":
            create_event()
        elif choice == "2":
            register_participant()
        elif choice == "3":
            view_events()
        elif choice == "4":
            print("Thank you!")
            break
        else:
            print("Invalid choice!")

if __name__ == "__main__":
    main()
