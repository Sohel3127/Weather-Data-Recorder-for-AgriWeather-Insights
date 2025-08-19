 # 📘 Weather Data Recorder for AgriWeather Insights
print('Hello from YBI Foundation 🚀')

import pandas as pd

# Global list to store weather data
weather_records = []

# Global set to store unique dates for validation
recorded_dates = set()

def is_date_unique(date):
    """Checks if a date has already been recorded."""
    return date not in recorded_dates

def add_weather_data():
    """Prompts the user for weather data and adds it to the records."""
    print("\n--- Add New Weather Record ---")
    while True:
        date = input("Enter date (YYYY-MM-DD): ")
        if is_date_unique(date):
            break
        else:
            print("Error: A record for this date already exists. Please enter a unique date.")

    try:
        temp = float(input("Enter temperature (°C): "))
    except ValueError:
        print("Invalid temperature. Please enter a number.")
        return

    condition = input("Enter weather condition (e.g., Sunny, Rainy, Cloudy): ")

    weather_record = {
        'date': date,
        'temperature': temp,
        'condition': condition
    }
    weather_records.append(weather_record)
    recorded_dates.add(date)
    print("Weather data added successfully!")

def view_weather_data():
    """Displays all recorded weather data."""
    print("\n--- All Weather Records ---")
    if not weather_records:
        print("No weather data recorded yet.")
        return

    for record in weather_records:
        print(f"Date: {record['date']}, Temp: {record['temperature']}°C, Condition: {record['condition']}")

def analyze_and_export_data():
    """Analyzes data using Pandas and exports it to a CSV file."""
    if not weather_records:
        print("\nNo data to analyze. Please add some weather records first.")
        return

    df = pd.DataFrame(weather_records)
    
    # Data visualization and insights
    print("\n--- Weather Data Analysis ---")
    print(df.describe())
    
    avg_temp = df['temperature'].mean()
    print(f"\nAverage Temperature: {avg_temp:.2f}°C")

    # Export to CSV
    try:
        df.to_csv('agriweather_data.csv', index=False)
        print("\nData exported to agriweather_data.csv successfully!")
    except Exception as e:
        print(f"Error exporting data to CSV: {e}")

def main():
    """Main function to run the application."""
    while True:
        print("\n--- AgriWeather Insights: Main Menu ---")
        print("1. Add Weather Data")
        print("2. View All Data")
        print("3. Analyze and Export Data")
        print("4. Exit")
        
        choice = input("Enter your choice (1-4): ")

        if choice == '1':
            add_weather_data()
        elif choice == '2':
            view_weather_data()
        elif choice == '3':
            analyze_and_export_data()
        elif choice == '4':
            print("Exiting application. Goodbye!")
            break
        else:
            print("Invalid choice. Please enter a number between 1 and 4.")

if __name__ == "__main__":
    main()
