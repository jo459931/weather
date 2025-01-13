import requests

# Function to get the weather data
def get_weather(city_name, api_key):
    # OpenWeatherMap URL to get the weather data
    base_url = "http://api.openweathermap.org/data/2.5/weather?"
    complete_url = f"{base_url}q={city_name}&appid={api_key}&units=metric"
    
    # Send a GET request to fetch data from the API
    response = requests.get(complete_url)
    
    # Convert the response to JSON
    data = response.json()
    
    # Check if the request was successful
    if data["cod"] == 200:
        # Extract data from the response
        main_data = data["main"]
        weather_data = data["weather"][0]
        
        # Display the results
        print(f"Weather in {city_name}:")
        print(f"Temperature: {main_data['temp']}°C")
        print(f"Humidity: {main_data['humidity']}%")
        print(f"Description: {weather_data['description'].capitalize()}")
    else:
        print(f"City {city_name} not found, please try again.")

# Replace with your actual OpenWeatherMap API key
api_key = "your_api_key_here"

# Ask the user for the city name
city_name = input("Enter the city name: ")

# Get and display the weather information
get_weather(city_name, api_key)
